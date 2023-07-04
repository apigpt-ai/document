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

# 05 Completions API

ClaudeAI 目前只有一个补全API

## API - Create a completion

`POST https://claude.pgpt.cloud/v1/complete`

创建一个补全

### Request body

#### 参数 - model `string` Required

将完成您提示的模型。

随着我们不断改进Claude，我们会开发新版本的Claude供您查询。这控制了哪个版本的Claude回答您的请求。现在我们提供两个模型系列：Claude和Claude Instant。

指定以下任何一个模型，都将自动切换到最新的兼容模型：

- "claude-1": 我们的最大模型，适用于各种更复杂的任务。
- "claude-1-100k": 一个增强版的claude-1，具有10万个标记（大约75,000个单词）的上下文窗口。非常适合于对长文档和对话进行摘要、分析和查询，以获得对复杂主题和跨非常长文本范围内的关系的细致理解。
- "claude-instant-1": 一个更小的模型，具有远低于最新claude-1模型的延迟，大约每秒采样40个单词！它的输出质量比最新的claude-1模型略低，特别是对于复杂的任务。然而，它的价格便宜得多，速度非常快。我们相信，这个模型在一系列任务上提供了足够的性能，包括文本分类、摘要和轻量级聊天应用，以及搜索结果摘要。
- "claude-instant-1-100k": 一个增强版的claude-instant-1，具有10万个标记的上下文窗口，保持了其性能。非常适合需要速度和额外上下文的高吞吐量用例，从长时间对话和文档中获得更深入的理解。

`您也可以选择上述模型的特定子版本：`

- "claude-1.3": 与claude-1.2相比，它对于来自红队的输入更加强大，更擅长精确的指令跟随，更擅长处理代码和非英语对话和写作。
- "claude-1.3-100k": 一个增强版的claude-1.3，具有10万个标记（大约7.5万个单词）的上下文窗口。
- "claude-1.2": 一个改进版的claude-1。它在一般的帮助性、指令跟随、编码和其他任务方面略有改善。它在处理非英语语言方面也有相当大的进步。此模型还具有更一致地（以无害的方式）扮演角色的能力，并且默认情况下会写出略长且更详尽的回复。
- "claude-1.0": claude-1的早期版本。
- "claude-instant-1.1": 我们的最新版claude-instant-1。它在许多任务上比claude-instant-1.0更好，包括写作、编码和指令跟随。它在学术基准测试中表现更好，包括数学、阅读理解和编码测试。它还对来自红队的输入更加强大。
- "claude-instant-1.1-100k": 一个增强版的claude-instant-1.1，具有10万个标记的上下文窗口，同时保持其每秒40个单词的闪电般的快速性能。
- "claude-instant-1.0": claude-instant-1的早期版本。

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

