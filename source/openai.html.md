---
title: APIGPT.CLOUD - OpenAI 开发文档

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - shell
  - python

toc_footers:
  - <center><a href='index.html'>返回文档首页</a></center>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for APIGPT.CLOUD OpenAI API
---

# APIGPT.Cloud - OpenAI 开发文档


你可以通过任何语言的 HTTP 请求与 API 进行交互，可以使用OpenAI的官方 Python 绑定、官方 Node.js 库或其他社区维护的库。

要安装官方 Python 绑定，请运行以下命令：


`pip install openai`


要安装官方 Node.js 库，请在你的 Node.js 项目目录中运行以下命令：

`npm install openai`

当您在API中需要开启使用stream模式时，推荐用OpenAI官方的SDK来调用接口，避免繁琐的数据解析问题。


# 01 认证
OpenAI API 使用 API 密钥进行身份验证。请访问你的 <a href=''>App 页面</a>，以获取你在请求中使用的 API 密钥。

请记住，你的 API 密钥是一个秘密！不要与他人分享它，也不要在任何客户端代码（浏览器、应用程序）中公开它。生产请求必须通过你自己的后端服务器路由，你的 API 密钥可以从环境变量或密钥管理服务中安全加载。

所有 API 请求都应该在 `API-KEY` HTTP 头中包含你的 API 密钥，如下所示：
`api-key: <替换成从APIGPT.CLOUD创建的OpenAI APP Key>`


# 02 发送请求
你可以将下面的命令粘贴到终端中以运行你的第一个 API 请求。请确保将 <API_KEY> 替换为你的秘密 API 密钥。


> 发送你的第一个 API 请求

```shell
curl https://openai.pgpt.cloud/v1/chat/completions \
-H "Content-Type: application/json" \
-H "Authorization: Bearer <API_KEY>" \
-d '{
 "messages": [{"role": "user", "content": "Say this message is from apigpt.cloud!"}],
 "temperature": 0.7
}'
```

```python
#你也可以用Python代码来发送第一个 API 请求
import openai
openai.api_key = '<API_KEY>'
openai.api_base = 'https://openai.pgpt.cloud/v1'
res = openai.ChatCompletion.create(
    model="gpt-3.5-turbo",
    messages=[{"role": "user", "content": "Hello world"}],
    temperature=1,
    max_tokens=1000,
)
print(res)
```


这个请求查询了 gpt-3.5-turbo 模型，以完成以 "Say this message is from apigpt.cloud!" 为提示开始的文本。

> 如果你会收到类下面JSON格式的数据响应，这说明你的请求成功了

```json
{
    "id":"chatcmpl-7SKQgp3ry5w9ZB0A3mMcvYOFB1VYG",
    "object":"chat.completion",
    "created":1686986070,
    "model":"gpt-35-turbo",
    "choices":[
        {
            "index":0,
            "finish_reason":"stop",
            "message":{
                "role":"assistant",
                "content":"Hello, this message is from apigpt.cloud! How may I assist you today?"
            }
        }
    ],
    "usage":{
        "completion_tokens":18,
        "prompt_tokens":18,
        "total_tokens":36
    }
}
```


我们可以在收到的请求里看到 finish_reason 是 stop，这意味着 API 返回了模型生成的完整完成。在上面的请求中，我们只生成了一条消息，但是你可以设置 n 参数来生成多个消息选项。

# 03 Chat APIs

给定一个包含对话的消息列表，模型将返回一个响应。

## API - Create chat completion

`POST https://openai.pgpt.cloud/v1/chat/completions`

为给定的聊天对话创建一个模型响应。

### Request body

> Create chat completion 请求示范

```python
import openai
openai.api_key = "<API_KEY>"
openai.api_base = 'https://openai.pgpt.cloud/v1'
res = openai.ChatCompletion.create(
  model="gpt-3.5-turbo",
  messages=[
    {"role": "system", "content": "You are a helpful assistant."},
    {"role": "user", "content": "Hello!"}
  ]
)
print(res)
```

```shell
curl https://openai.pgpt.cloud/v1/chat/completions \
-H "Content-Type: application/json" \
-H "Authorization: Bearer <API_KEY>" \
-d '{
 "messages": [{"role": "user", "content": "You are a helpful assistant."}],
 "temperature": 0.7
}'
```


> Create chat completion 请求示范打印结果

```json
{
    "id":"chatcmpl-7Tl47vuq1rKS4XlcV7IihageYc514",
    "object":"chat.completion",
    "created":1687326787,
    "model":"gpt-35-turbo",
    "choices":[
        {
            "index":0,
            "finish_reason":"stop",
            "message":{
                "role":"assistant",
                "content":"Thank you! How may I assist you today?"
            }
        }
    ],
    "usage":{
        "completion_tokens":10,
        "prompt_tokens":14,
        "total_tokens":24
    }
}
```

#### 参数 - model `string` Required

要使用的模型ID。目前我们支持并推荐用 `gpt-3.5-turbo`, `gpt-3.5-turbo-16k`, `gpt-4`,`gpt-4-32k`

#### 参数 - messages `array` Required

到目前为止，对话包含的消息列表

消息 `message` 的数据结构:

参数 | 类型 | 是否必须 | 描述
-----|------|----------|-------
role | `string` | `Required` | 消息作者的角色。其中之一是`system`、`user`、`assistant`。
content | `string` | `Optional` | 消息的内容。除了带有函数调用的`assistant`，所有消息都需要 `content`。
name | `string` | `Optional` | 此 `content` 作者的姓名。姓名可以包含a-z、A-Z、0-9和下划线，最长长度为64个字符。


#### 参数 - temperature `number` Optional Defaults to 1

要使用的采样温度，介于0和2之间。较高的值（如0.8）会使输出更加随机，而较低的值（如0.2）会使输出更加集中和确定性。

#### 参数 stream `boolean` Optional Defaults to false

如果设置了此选项，将发送部分消息增量，就像在 ChatGPT 中一样。令牌将作为数据类型的服务器发送的事件逐步发送，一旦可用，流将以 data: [DONE] 消息终止。


#### 参数 max_tokens `integer` Optional Defaults to inf

在聊天补全中生成的最大令牌数。
输入令牌和生成令牌的总长度受模型上下文长度的限制。


<aside class="notice">
暂未支持 ChatGPT 官方的 function 调用特性及相关参数。
此外为简化使用，官方 Create chat completion 函数下列可选参数也未被支持：top_p, n, stop, presence_penalty, frequency_penalty, logit_bias, user, 如您需要，请通过左方二维码联系我们
</aside>

# 04 Completions APIs

根据提示，模型将返回一个或多个预测完成，并且还可以返回每个位置替代标记的概率。

## API - Create completion

`POST https://openai.pgpt.cloud/v1/completions`

### Request body

> Create completion 请求示范

```python
import openai
openai.api_key = '<API_KEY>'
openai.api_base = 'https://openai.pgpt.cloud/v1'
res = openai.Completion.create(
  model="gpt-3.5-turbo",
  prompt="I am a",
  max_tokens=7,
  temperature=0
)
print(res)
```

```shell
curl https://openai.pgpt.cloud/v1/completions \
-H "Content-Type: application/json" \
-H "Authorization: Bearer <APK_KEY>" \
-d '{
    "model": "gpt-3.5-turbo",
    "prompt": "I am a",
    "max_tokens": 7,
    "temperature": 0
  }'
```

> Create completion 请求示范打印结果

```json
{
  "id": "cmpl-7TkgRTfjrz80goegsOC2nrkzi1WPm",
  "object": "text_completion",
  "created": 1687325319,
  "model": "gpt-35-turbo",
  "choices": [
    {
      "text": " 20 year old female and I",
      "index": 0,
      "finish_reason": "length",
      "logprobs": null
    }
  ],
  "usage": {
    "completion_tokens": 7,
    "prompt_tokens": 3,
    "total_tokens": 10
  }
}
```

#### 参数 - model `string` Required

要使用的模型ID。目前我们支持并推荐用 `gpt-3.5-turbo`, `gpt-3.5-turbo-16k`, `gpt-4`,`gpt-4-32k`

#### 参数 - prompt `string or array` Required

要为其生成完成（completions）的提示，可以以字符串、字符串数组、标记数组或标记数组的数组形式进行编码。

请注意，在训练期间，模型所看到的文档分隔符为 "<|endoftext|>"

#### 参数 max_tokens `integer` Optional Defaults to inf

在文本补全中生成的最大令牌数。
输入令牌和生成令牌的总长度受模型上下文长度的限制。


#### 参数 - temperature `number` Optional Defaults to 1

要使用的采样温度，介于0和2之间。较高的值（如0.8）会使输出更加随机，而较低的值（如0.2）会使输出更加集中和确定性。

#### 参数 stream `boolean` Optional Defaults to false

如果设置了此选项，将发送部分消息增量，就像在 ChatGPT 中一样。令牌将作为数据类型的服务器发送的事件逐步发送，一旦可用，流将以 data: [DONE] 消息终止。


<aside class="notice">
为简化使用，官方 Create completion 函数下列可选参数也未被支持：suffix, top_p, n, logprobs, echo, stop, presence_penalty, frequency_penalty, best_of, logit_bias, user。如您需要，请通过左方二维码联系我们
</aside>

# 05 Embeddings APIs

获取给定输入的矢量表示，以便机器学习模型和算法可以轻松处理。

## API - Create embeddings

`POST https://openai.pgpt.cloud/v1/embeddings`

创建一个表示输入文本的嵌入向量。

### Request body

> Create embeddings 示范请求

```python
import openai
openai.api_key = '<API_KEY>'
openai.api_base = 'https://openai.pgpt.cloud/v1'
res = openai.Embedding.create(
  model="text-embedding-ada-002",
  input="The food was delicious and the waiter..."
)
print(res)
```

```shell
curl https://openai.pgpt.cloud/v1/embeddings \
-H "Content-Type: application/json" \
-H "Authorization: Bearer <API_KEY>" \
-d '{
    "input": "The food was delicious and the waiter...",
    "model": "text-embedding-ada-002"
  }'
```

> Create embeddings 示范请求打印结果

```json
{
  "object": "list",
  "data": [
    {
      "object": "embedding",
      "embedding": [
        0.0023064255,
        -0.009327292,
        .... (1536 floats total for ada-002)
        -0.0028842222,
      ],
      "index": 0
    }
  ],
  "model": "text-embedding-ada-002",
  "usage": {
    "prompt_tokens": 8,
    "total_tokens": 8
  }
}
```

#### 参数 - model `string` Required

要使用的模型ID。目前我们支持并推荐用 `text-embedding-ada-002`

#### 参数 - input `string or array` `Required`

要嵌入的输入文本，可以以字符串或标记数组的形式进行编码。要在单个请求中嵌入多个输入，请传递字符串数组或标记数组的数组。每个输入的标记数不能超过模型的最大输入标记数（对于text-embedding-ada-002模型，最大输入标记数为8191个）。

<aside class="notice">
为简化使用，官方 Create embeddings 函数下列可选参数也未被支持：user, 如您需要，请通过左方二维码联系我们
</aside>

# 06 其他 APIs

`ChatGPT 官方`支持的其他 API 支持情况如下，如果你有需要，请扫描左方二维码来联系我们。

## Fine-tunes

在规划中

## Edits

暂未支持

## Images

暂未支持

## Audio

暂未支持

## Files

暂未支持

## Moderations

暂未支持
