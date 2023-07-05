---
title: APIGPT.CLOUD 用户文档

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - shell
  - python

toc_footers:
  - <center><a href='https://apigpt.cloud'>访问 APIGPT.CLOUD</a></center>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for APIGPT.CLOUD API
---

# 生成式 AI 云（APIGPT.CLOUD）用户手册



# 01 - 关于APIGPT

## 服务介绍
生成式 AI 云（简称 APIGPT）是一款生成式 AI 云服务，旨在为开发者提供一站式集成多个 AIGC 服务商 API 的服务。只需开通一个 APIGPT.CLOUD 账号，开发者即可稳定访问包括 <b>OpenAI 官方</b>，<b>Azure OpenAI</b>、<b>ChatGLM</b>、<b>Claude AI</b>、<b>Google Bard AI</b>、<b>Stable Diffusion</b> 在内的多项生成式 AI API，轻松集成生成式AI能力到自己的应用中。让 APIGPT.CLOUD 成为您的生成式AI云服务，将极大地提高您的开发效率。

此外，基于开发者的需求，我们开发了具备内容生成、图像生成的<b> AGIEditor 编辑器组件</b>，方便开发者使用；还有集合了所有 AIGC 服务商接口的 <b>AIGCCLOUD PYPI 包</b>，Python 开发者只需要安装一次后即可调用上述 AIGC 服务商的接口。


## 为什么应该选择 APIGPT
和原 AIGC 官方的 API 相比，APIGPT 的 API 服务有以下优势：

- 无前置审核流程，注册完成账号即可使用，充值方式简单且多样
- 对官方接口进行了必要的优化和简化，让开发者使用更方便
- 提供跨 AIGC 服务整合的能力，能让用户方便地使用最有方案
- 提供及时的真人响应支持服务



# 02 - 快速入门

您只要在 <a href='https://apigpt.cloud' target='_blank'>APIGPT.CLOUD 官网</a> 创建一个账号，无需审核，即拥有了方便访问各个 AIGC 服务 API 的权限。

## 注册账号
点击 <a href='https://apigpt.cloud' target='_blank'> APIGPT.CLOUD 官网</a> 右上角的“开始按钮”，即可进入注册流程。

<img src='https://apigpt.cloud/wp-content/uploads/2023/05/1-1.png' />

提交账号信息后进入到资料填写页面，在此处选择 APIGPT 服务，最后提交，无需审核，即可马上开通账号。

## 创建App
注册成功后，点击后即可进入到控制面板，通过左侧菜单的 API Integration 即可通过创建 App 的方式获得 API Integration，新建一个 App 后点击提交，即可获得访问对应 AIGC 服务的 API Key。

<img src='https://apigpt.cloud/wp-content/uploads/2023/05/2-1.png'>


## 获得接入到第三方应用的 Token

获得上述 API Key 后，即可在各 AIGC App 中使用。

<img src='https://apigpt.cloud/wp-content/uploads/2023/05/3-1.png' />

APIGPT.CLOUD 针对各个 AIGC 服务商提供的 API 绝大部分都兼容于原 AIGC 官方 APII，可以无缝切换。


## 试用与充值

默认注册后，我们都会免费赠送 5000P 额度供你使用，使用完毕后，您可以随时通过充值购买额度。

# 03 - AIGC API 文档

## APIGPT OpenAI

<img src="https://apigpt.cloud/wp-content/uploads/2023/05/OAI.png">

APIGPT 的 OpenAI 是基于 <a href='https://platform.openai.com/docs/models/gpt-4' target='_blank'>OpenAI 官方 GPT4</a> 和 <a href='https://learn.microsoft.com/zh-cn/azure/cognitive-services/openai/overview' target='_blank'>Azure OpenAI</a> 服务构建。

通过 APIGPT OpenAI 可使用很多不同模型，这些模型按系列和功能分组。 模型系列通常按其预期任务关联模型。 下表介绍了 Azure OpenAI 中当前可用的模型系列。 目前并非所有模型都可在所有区域中使用。

APIGPT OpenAI 目前支持的模型包括并不限于下列：

模型组 | 模型ID | 限制 | 描述
--------- | ------- | ----------- | -----------
GPT-4 | gpt-4 | 8192 | 与任何 OpenAI 以前的模型相比，GPT-4 可以更准确地解决难题，与 gpt-35-turbo 一样，GPT-4 针对聊天进行了优化，但适用于传统的完成任务。
GPT-3.5 | gpt-35-turbo | 4096 | ChatGPT 模型 (gpt-35-turbo) 是一种专为对话接口设计的语言模型
GPT-3.5 | gpt-35-turbo-16k | 16k | ChatGPT 模型 (gpt-35-turbo-16k) 是gpt-35-turbo的增强版，可以支持高达16k的 Token输入
Embeddings | text-embedding-ada-002 | 8191 | 一组可以理解和使用嵌入的模型。 嵌入是一种特殊的数据表示格式，可由机器学习模型和算法轻松使用。 嵌入是一段文本的语义含义的信息密集表示。
Codex | code-davinci-002 | 8001 | Codex 模型是基模型 GPT-3 的子代，可以理解和生成代码。 它们的训练数据包含自然语言和来自 GitHub 的数十亿行公开代码。


在 APIGPT 中建立了一个 OpenAI App 后，你可以在你的应用程序中使用 OpenAI 的接口。

<a href='openai.html'>阅读 APIGPT.CLOUD - OpenAI 开发文档 >></a>

## APIGPT ClaudeAI

<img src="https://apigpt.cloud/wp-content/uploads/2023/06/claudeai.png">

APIGPT 的 ClaudeAI 是基于<a href='https://www.anthropic.com/product' target='_blank'>Anthropic ClaudeAI</a>而构建，它主要是用于对话的模型，用人工标注的对话数据集进行训练，Claude 的对话能力更强，能够进行更长更流畅的对话互动。它能一次处理最长长达9000个 Token 的内容。

在 APIGPT 中建立了一个 ClaudeAI App 后，你可以在你的应用程序中使用 ClaudeAI 的接口。

<a href='claudeai.html'>阅读 APIGPT.CLOUD - ClaudeAI 开发文档 >></a>

## APIGPT BardAI

<img src="https://apigpt.cloud/wp-content/uploads/2023/05/600X3005.png">

<a href='https://bard.google.com/' target='_blank'>BardAI</a> 是 Google 基于对话应用语言模型 LaMDA 来构建，可以更准确，全面地理解自然语言，并且为用户提供及时的信息。

APIGPT 基于 Google BardAI 构建了 API 服务。


<a href='#'>APIGPT.CLOUD - BardAI 接口在完善中... >></a>

## APIGPT StableDiffusion


<img src="https://apigpt.cloud/wp-content/uploads/2023/05/600X3003.png">

基于 AI 画图 <a href='https://stablediffusionweb.com/' target='_blank'>Stable Diffusion 软件</a>，APIGPT 搭建了GPU 算力云，为用户提供了便捷的 Stable Diffusion API，开发者无需自行折腾繁琐的算力服务器，大大节省了时间和效率。


在 APIGPT 中建立了一个 SDAI App 后，你可以在你的应用程序中使用 SDAI 的接口。

<a href='sdai.html'>阅读 APIGPT.CLOUD - SDAI 开发文档 >></a>

## APIGPT ChatGLM


<img src="https://apigpt.cloud/wp-content/uploads/2023/06/ChatGLM-logo.png">

ChatGLM 使用类似于 ChatGPT 的技术，专门针对中文问答和对话进行了优化。经过约1T标识符的中英双语训练，结合监督微调、反馈自助、人类反馈强化学习等技术的加持，拥有62亿参数的 ChatGLM-6B 已经能够生成与人类偏好相当符合的回答。

在 APIGPT 中建立一个 ChatGLM2-6B App后，你就可以在你的应用程序中使用 ChatGLM-6B 的接口。


<a href='chatglm2-6b.html'>阅读 APIGPT.CLOUD - ChatGLM2-6B 开发文档 >></a>

# 04 - AIGC Chat 文档

# 05 - 负责任的 AIGC

## 内容安全

## 隐私保护


# 06 - 资源
