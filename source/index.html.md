---
title: APIGPT.Cloud文档服务

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - shell
  - python

toc_footers:
  -

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for APIGPT.CLOUD API
---

# 生成式 AI 云（APIGPT.CLOUD）用户手册



# 01 - 概述

## 关于APIGPT

生成式 AI 云（简称 APIGPT）是一款生成式 AI 云服务，旨在为开发者提供一站式集成多个 AIGC 服务商 API 的服务。只需开通一个 APIGPT.CLOUD 账号，开发者即可稳定访问包括 <b>OpenAI 官方</b>，<b>Azure OpenAI</b>、<b>Claude AI</b>、<b>Google Bard AI</b>、<b>百度文言一心</b>、<b>阿里通义大模型</b>和<b> APTGPT 自行构建的 Stable Diffusion</b> 在内的多项生成式 AI API，轻松集成生成式AI能力到自己的应用中。让 APIGPT.CLOUD 成为您的生成式AI云服务，将极大地提高您的开发效率。

此外，基于开发者的需求，我们开发了具备内容生成、图像生成的<b> AGIEditor 编辑器组件</b>，方便开发者使用；还有集合了所有 AIGC 服务商接口的 <b>AIGCCLOUD PYPI 包</b>，Python 开发者只需要安装一次后即可调用上述 AIGC 服务商的接口。


## APIGPT OpenAI

APIGPT 的 OpenAI 是基于 <a href='https://platform.openai.com/docs/models/gpt-4' target='_blank'>OpenAI 官方 GPT4</a> 和 <a href='https://learn.microsoft.com/zh-cn/azure/cognitive-services/openai/overview' target='_blank'>Azure OpenAI</a> 服务构建。

通过 APIGPT OpenAI 可使用很多不同模型，这些模型按系列和功能分组。 模型系列通常按其预期任务关联模型。 下表介绍了 Azure OpenAI 中当前可用的模型系列。 目前并非所有模型都可在所有区域中使用。

APIGPT OpenAI 目前支持的模型包括并不限于下列：

模型组 | 模型ID | 限制 | 描述
--------- | ------- | ----------- | -----------
GPT-4 | gpt-4 | 8192 | 与任何 OpenAI 以前的模型相比，GPT-4 可以更准确地解决难题，与 gpt-35-turbo 一样，GPT-4 针对聊天进行了优化，但适用于传统的完成任务。
GPT-3.5 | gpt-35-turbo | 4096 | ChatGPT 模型 (gpt-35-turbo) 是一种专为对话接口设计的语言模型
Embeddings | text-embedding-ada-002 | 8191 | 一组可以理解和使用嵌入的模型。 嵌入是一种特殊的数据表示格式，可由机器学习模型和算法轻松使用。 嵌入是一段文本的语义含义的信息密集表示。
Codex | code-davinci-002 | 8001 | Codex 模型是基模型 GPT-3 的子代，可以理解和生成代码。 它们的训练数据包含自然语言和来自 GitHub 的数十亿行公开代码。

## APIGPT ClaudeAI
APIGPT 的 ClaudeAI 是基于<a href='https://www.anthropic.com/product' target='_blank'>Anthropic ClaudeAI</a>而构建，它主要是用于对话的模型，用人工标注的对话数据集进行训练，Claude 的对话能力更强，能够进行更长更流畅的对话互动。它能一次处理最长长达9000个 Token 的内容。

## APIGPT BardAI

<a href='https://bard.google.com/' target='_blank'>BardAI</a> 是 Google 基于对话应用语言模型 LaMDA 来构建，可以更准确，全面地理解自然语言，并且为用户提供及时的信息。

APIGPT 基于 Google BardAI 构建了 API 服务。

## APIGPT 百度文言一心

待补充

## APIGPT 阿里通义大模型

待补充


## APIGPT StableDiffusion

基于 AI 画图 <a href='https://stablediffusionweb.com/' target='_blank'>Stable Diffusion 软件</a>，APIGPT 搭建了GPU 算力云，为用户提供了便捷的 Stable Diffusion API，开发者无需自行折腾繁琐的算力服务器，大大节省了时间和效率。


# 02 - 快速入门

您需要在<a href='' target='_blank'> APIGPT.CLOUD 官网</a>创建一个账号，无需审核，即拥有了方便访问各个 AIGC 服务 API 的权限。

## 注册账号

## 创建App

## 使用 Playgroud 来探索

## 获得接入到第三方应用的 Token

## 试用与充值

# 03 - API 文档

## APIGPT OpenAI

<img src="https://apigpt.cloud/wp-content/uploads/2023/05/OAI.png">

### 介绍
你可以通过任何语言的 HTTP 请求与 API 进行交互，可以使用OpenAI的官方 Python 绑定、官方 Node.js 库或其他社区维护的库。

要安装官方 Python 绑定，请运行以下命令：


`pip install openai`


要安装官方 Node.js 库，请在你的 Node.js 项目目录中运行以下命令：

`npm install openai`


### 认证
OpenAI API 使用 API 密钥进行身份验证。请访问你的 <a href=''>App 页面</a>，以获取你在请求中使用的 API 密钥。

请记住，你的 API 密钥是一个秘密！不要与他人分享它，也不要在任何客户端代码（浏览器、应用程序）中公开它。生产请求必须通过你自己的后端服务器路由，你的 API 密钥可以从环境变量或密钥管理服务中安全加载。

所有 API 请求都应该在 `API-KEY` HTTP 头中包含你的 API 密钥，如下所示：
`api-key: <替换成从APIGPT.CLOUD创建的OpenAI APP Key>`


### 发送请求
你可以将下面的命令粘贴到终端中以运行你的第一个 API 请求。请确保将 <API_KEY> 替换为你的秘密 API 密钥。


> 发送你的第一个 API 请求

```shell
## 发送请求 

curl https://openai.pgpt.cloud/openai/deployments/gpt-35-turbo/chat/completions \
-H "Content-Type: application/json" \
-H "api-key: <API_KEY>" \
-d '{
 "messages": [{"role": "user", "content": "Say this message is from apigpt.cloud!"}],
 "temperature": 0.7
}'

```

```python

```

这个请求查询了 gpt-3.5-turbo 模型，以完成以 "Say this message is from apigpt.cloud!" 为提示开始的文本。

> 如果你会收到类下面JSON格式的数据响应，这说明你的请求成功了

```json
## 请求返回
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


我们可以看到 finish_reason 是 stop，这意味着 API 返回了模型生成的完整完成。在上面的请求中，我们只生成了一条消息，但是你可以设置 n 参数来生成多个消息选项。



```python

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



## APIGPT ClaudeAI

待完善

## APIGPT BardAI

待完善

## APIGPT StableDiffusion


待完善

## APIGPT 百度文言一心

待补充

## APIGPT 阿里通义大模型

待补充

# 04 - 负责任的 AI

## 内容安全

## 隐私保护

# 05 - 参考

# 06 - 资源
