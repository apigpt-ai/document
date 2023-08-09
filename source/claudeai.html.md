---
title: APIGPT.CLOUD - ClaudeAI 开发文档

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - shell
  - python
  - javascript

toc_footers:
  - <center><a href='index.html'>返回文档首页</a></center>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for APIGPT.CLOUD ClaudeAI API
---

# APIGPT.Cloud - ClaudeAI 开发文档

该 API 可通过我们的沙盒平台提供。这使您有机会在开始技术集成之前评估 Claude 的能力。


# 01 提示格式化

默认情况下，我们的沙盒将正确处理类似“天空为什么是蓝色的？”这样的直接问题。然而，当使用API时，您必须按照以下格式设置提示：

`\n\nHuman: Why is the sky blue?\n\nAssistant: `

请注意每个冒号后面的两个换行符和一个空格，除了最后一个冒号。例如，在代码中使用它：

```javascript
const userQuestion = "Why is the sky blue?";
const prompt = `\n\nHuman: ${userQuestion}\n\nAssistant:`;

// Send prompt to Claude via API

```

# 02 客户端库

我们提供了Python和Typescript（即将推出）的客户端库，使得使用API更加便捷。

Python 库: `https://github.com/apigptcloud/anthropic-sdk-python`

```python
import os
import anthropic

client = anthropic.Client(os.environ['ANTHROPIC_API_KEY'])
response = client.completion(
    prompt=f"{anthropic.HUMAN_PROMPT} How many toes do dogs have?{anthropic.AI_PROMPT}",
    model="claude-1",
    max_tokens_to_sample=100,
)
print(response)
```

Typescript 库: `https://github.com/apigptcloud/anthropic-sdk-typescript`


```javascript
import "dotenv/config";
import { AI_PROMPT, Client, HUMAN_PROMPT } from "@anthropic-ai/sdk";

const apiKey = process.env.ANTHROPIC_API_KEY;
if (!apiKey) {
  throw new Error("The ANTHROPIC_API_KEY environment variable must be set");
}

const client = new Client(apiKey);
client
  .complete({
    prompt: `${HUMAN_PROMPT} How many toes do dogs have?${AI_PROMPT}`,
    max_tokens_to_sample: 200,
    model: "claude-1",
  })
  .then((finalSample) => {
    console.log(finalSample.completion);
  })
  .catch((error) => {
    console.error(error);
  });
```

# 03 流式传输

在进行API请求时，您可以设置"stream": true，以使用服务器发送事件(SSE)逐步流式传输响应。如果您使用我们的客户端库，则这些事件的解析将自动处理。但是，如果您正在构建直接的API集成，您需要自己处理这些事件。


> 流式示范请求

```shell
curl --request POST \
     --url https://claude.pgpt.cloud/v1/complete \
     --header "content-type: application/json" \
     --header "x-api-key: $API_KEY" \
     --data '
{
  "model": "claude-1",
  "prompt": "\n\nHuman: Hello, world!\n\nAssistant:",
  "max_tokens_to_sample": 256,
  "stream": true
}
'
```

> 流式示范请求返回

```
event: completion
data: {"completion": " Hello", "stop_reason": null, "model": "claude-1.3"}

event: completion
data: {"completion": "!", "stop_reason": null, "model": "claude-1.3"}

event: ping
data: {}

event: completion
data: {"completion": " My", "stop_reason": null, "model": "claude-1.3"}

event: completion
data: {"completion": " name", "stop_reason": null, "model": "claude-1.3"}

event: completion
data: {"completion": " is", "stop_reason": null, "model": "claude-1.3"}

event: completion
data: {"completion": " Claude", "stop_reason": null, "model": "claude-1.3"}

event: completion
data: {"completion": ".", "stop_reason": null, "model": "claude-1.3"}

event: completion
data: {"completion": "", "stop_reason": "stop_sequence", "model": "claude-1.3"}

```

# 04 事件

每个事件都包括一个命名的事件类型和相关的JSON数据。


<aside class="notice">
`处理未知的事件类型`
目前我们发送完成、ping和错误事件类型，但是这个列表可能会随着时间的推移而扩展，您的集成必须忽略任何意外的事件类型。
</aside>

我们可能会偶尔在事件流中发送错误。例如，在高使用期间，您可能会收到一个overloaded_error，这通常对应于非流式上下文中的HTTP 529:

```
event: completion
data: {"completion": " Hello", "stop_reason": null, "model": "claude-1.3"}

event: error
data: {"error": {"type": "overloaded_error", "message": "Overloaded"}}
```

# 05 模型


我们目前提供两个模型系列，两者都支持10万个标记的上下文窗口：

- Claude-instant：低延迟，高吞吐量
- Claude：在需要复杂推理的任务中表现出色

在向我们的 Completions API 发送请求时，您必须使用模型参数指定要执行完成的模型。我们建议您指定最新的主要版本，这样您将在发布更新时自动获得模型的更新。或者，如果您依赖于精确的输出形状，您可以指定完整的模型版本。

有关模型更多详细信息，请参见<a href='/index.html#apigpt-claudeai'>模型</a>。

# 06 Completions API

ClaudeAI 目前只有一个补全API

## API - Create a completion

`POST https://claude.pgpt.cloud/v1/complete`

创建一个补全

### Request body

#### 参数 - model `string` Required

将会完成您的提示的模型。

随着我们改进 Claude，我们会开发新的版本供您查询。这个参数控制着 Claude 回答您请求的版本。目前我们提供两个模型系列：Claude 和 Claude-instant。您可以通过将模型设置为“claude-2”或“claude-instant-1”来使用它们。有关更多详细信息，请参见<a href='/index.html#apigpt-claudeai'>模型</a>。


#### 参数 - prompt `blob` Required

您想让Claude完成的提示。

为了生成适当的响应，您需要按照以下格式设置您的提示，就像我们在上面提示格式化章节介绍的一样：

```javascript
const userQuestion = r"Why is the sky blue?";
const prompt = `\n\nHuman: ${userQuestion}\n\nAssistant:`;
```

#### 参数 - max_tokens_to_sample `integer` required

在停止生成之前生成的最大标记数。

请注意，我们的模型可能在达到此最大值之前就停止。此参数仅指定要生成的绝对最大标记数。

#### 参数 - stop_sequences `array of strings`
会导致模型停止生成完整文本的序列。

我们的模型会在"\n\nHuman:"处停止，将来可能会包括其他内置的停止序列。通过提供stop_sequences参数，您可以包括其他字符串，这些字符串将导致模型停止生成。


#### 参数 - temperature `number`
注入响应中的随机性量。

默认为1。范围从0到1。将temp设置得更接近0可用于分析/多选题，而将其设置得更接近1可用于创造性和生成性任务。

#### 参数 - top_p `number`
使用核心采样。

在核心采样中，我们按减少的概率顺序计算每个后续标记的所有选项的累积分布，并在达到由top_p指定的特定概率时将其截断。您应该更改温度或top_p，但不能两者同时更改。

#### 参数 - top_k `integer`
只从每个后续标记的前K个选项中进行采样。

用于删除“长尾”低概率响应。在此处了解更多技术细节。

#### 参数 - metadata `object`

描述请求元数据的对象。

user_id字符串
与请求相关联的用户的外部标识符。

这应该是uuid、哈希值或其他不透明标识符。Anthropic可能使用此id来帮助检测滥用行为。不要包括任何识别信息，例如姓名、电子邮件地址或电话号码。


#### 参数 - stream `boolean`

是否使用服务器发送事件逐步流式传输响应，见上面流式传输章节。

