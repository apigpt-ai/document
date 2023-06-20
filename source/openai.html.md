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


# 01 认证
OpenAI API 使用 API 密钥进行身份验证。请访问你的 <a href=''>App 页面</a>，以获取你在请求中使用的 API 密钥。

请记住，你的 API 密钥是一个秘密！不要与他人分享它，也不要在任何客户端代码（浏览器、应用程序）中公开它。生产请求必须通过你自己的后端服务器路由，你的 API 密钥可以从环境变量或密钥管理服务中安全加载。

所有 API 请求都应该在 `API-KEY` HTTP 头中包含你的 API 密钥，如下所示：
`api-key: <替换成从APIGPT.CLOUD创建的OpenAI APP Key>`


# 02 发送请求
你可以将下面的命令粘贴到终端中以运行你的第一个 API 请求。请确保将 <API_KEY> 替换为你的秘密 API 密钥。


> 发送你的第一个 API 请求

```shell
curl https://openai.pgpt.cloud/openai/deployments/gpt-35-turbo/chat/completions \
-H "Content-Type: application/json" \
-H "api-key: <API_KEY>" \
-d '{
 "messages": [{"role": "user", "content": "Say this message is from apigpt.cloud!"}],
 "temperature": 0.7
}'
```

```python
#你也可以用Python代码来发送第一个 API 请求

import openai
openai.api_key = '<API_KEY>'
openai.api_base = 'https://openai.pgpt.cloud'
openai.api_type = 'azure'
openai.api_version = 'version'
engine = 'gpt-35-turbo'

completion = openai.ChatCompletion.create(
    engine=engine,
    messages=[{"role": "user", "content": "Say this message is from apigpt.cloud!"}],
)
print(completion.choices[0].message.content)

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

# 03 Chat API

给定一个包含对话的消息列表，模型将返回一个响应。

## API - Create chat completion

`POST https://openai.pgpt.cloud/openai/deployments/gpt-35-turbo/chat/completions`

为给定的聊天对话创建一个模型响应。

### Request body

#### 参数 - messages `array` Required

到目前为止，对话包含的消息列表

消息 `message` 的数据结构:

参数 | 类型 | 是否必须 | 描述
-----|------|----------|-------
role | `string` | `Required` | 消息作者的角色。其中之一是`system`、`user`、`assistant`或`function`。
content | `string` | `Optional` | 消息的内容。除了带有函数调用的`assistant`，所有消息都需要 `content`。
name | `string` | `Optional` | 此 `content` 作者的姓名。如果 `role` 是 `function`，则需要 `name`，并且应该是响应 `content` 的函数的名称。名称可以包含a-z、A-Z、0-9和下划线，最长长度为64个字符。
function_call | `object` | `Optional` | 由模型生成的应调用的 `function` 的名称和参数。

#### 参数 - functions `array` `Optional`

模型可能为其生成JSON输入的函数列表。

参数 | 类型 | 是否必须 | 描述
-----|------|----------|-------
name | `string` | `Required` | 要调用的函数的名称。名称必须是a-z、A-Z、0-9或包含下划线和破折号，并且最长长度为64个字符。
description | `string` | `Optional` | 函数的描述，说明其功能。
parameters | `object` | `Optional` | 函数接受的参数，以JSON Schema对象的形式描述。有关格式的文档，请参见指南中的示例和JSON Schema参考。


















# 04 Completions API

# 05 Embeddings API
