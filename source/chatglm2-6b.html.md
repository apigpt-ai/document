---
title: APIGPT.CLOUD - ChatGLM 开发文档

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
    content: Documentation for APIGPT.CLOUD ChatGLM API
---

# APIGPT.Cloud - ChatGLM 开发文档

你可以通过任何语言的 HTTP 请求与 API 进行交互，可以使用 APIGPT 的 Python 库或用 Python requests 库来调用来调用 ChatGLM 的 Chat 接口。


# 01 认证
ChatGLM 使用 API 密钥进行身份验证。请访问你的 <a href=''>App 页面</a>，以获取你在请求中使用的 API 密钥。

所有 API 请求都应该在 `API-KEY` HTTP 头中包含你的 API 密钥，如下所示：
`API-KEY: <替换成从APIGPT.CLOUD创建的SDAI APP Key>`

# 02 发送请求
你可以将下面的命令粘贴到终端中以运行你的第一个 API 请求。请确保将 <API_KEY> 替换为你的秘密 API 密钥。


> 发送你的第一个 API 请求

```shell
curl https://chatglm.pgpt.cloud/v1/chat/completions \
-H "Content-Type: application/json" \
-H "Authorization: Bearer <API_KEY>" \
-d '{
 "messages": [{"role": "user", "content": "Say this message is from apigpt.cloud!"}],
 "temperature": 0.7
}'
```

> 如果你会收到类下面JSON格式的数据响应，这说明你的请求成功了

```json
{
    "model":"chatglm2-6b",
    "object":"chat.completion",
    "choices":[
        {
            "index":0,
            "message":{
                "role":"assistant",
                "content":"Hello! This is from Apigpt.cloud, a platform for building and managing APIs. How can we help you today?"
            },
            "finish_reason":"stop"
        }
    ],
    "created":1691555321
}
```

# 03 Chat APIs

给定一个包含对话的消息列表，模型将返回一个响应。

## API - Create chat completion

`POST https://chatglm.pgpt.cloud/v1/chat/completions`

为给定的聊天对话创建一个模型响应。

### Request body

> Create chat completion 请求示范

```python

```

```shell
curl https://chatglm.pgpt.cloud/v1/chat/completions \
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
    "model":"chatglm2-6b",
    "object":"chat.completion",
    "choices":[
        {
            "index":0,
            "message":{
                "role":"assistant",
                "content":"Hello! This is from Apigpt.cloud, a platform for building and managing APIs. How can we help you today?"
            },
            "finish_reason":"stop"
        }
    ],
    "created":1691555321
}

```

#### 参数 - messages `array` Required
到目前为止，对话包含的消息列表


消息 `message` 的数据结构:

参数 | 类型 | 是否必须 | 描述
-----|------|----------|-------
role | `string` | `Required` | 消息作者的角色。其中之一是`system`、`user`、`assistant`。
content | `string` | `Optional` | 消息的内容。除了带有函数调用的`assistant`，所有消息都需要 `content`。
name | `string` | `Optional` | 此 `content` 作者的姓名。姓名可以包含a-z、A-Z、0-9和下划线，最长长度为64个字符。


#### 参数 - history `array` Optional
到目前为止，对话包含的历史消息列表，结构参考messages


#### 参数 - temperature `number` Optional Defaults to 1

要使用的采样温度，介于0和2之间。较高的值（如0.8）会使输出更加随机，而较低的值（如0.2）会使输出更加集中和确定性。

#### 参数 max_tokens `integer` Optional Defaults to inf

在聊天补全中生成的最大令牌数。
输入令牌和生成令牌的总长度受模型上下文长度的限制。

