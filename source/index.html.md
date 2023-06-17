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



# 01 - 概述

## 关于APIGPT

生成式 AI 云（简称 APIGPT）是一款生成式 AI 云服务，旨在为开发者提供一站式集成多个 AIGC 服务商 API 的服务。只需开通一个 APIGPT.CLOUD 账号，开发者即可稳定访问包括 <b>OpenAI 官方</b>，<b>Azure OpenAI</b>、<b>Claude AI</b>、<b>Google Bard AI</b>、<b>百度文言一心</b>、<b>阿里通义大模型</b>和<b> APTGPT 自行构建的 Stable Diffusion</b> 在内的多项生成式 AI API，轻松集成生成式AI能力到自己的应用中。让 APIGPT.CLOUD 成为您的生成式AI云服务，将极大地提高您的开发效率。

此外，基于开发者的需求，我们开发了具备内容生成、图像生成的<b> AGIEditor 编辑器组件</b>，方便开发者使用；还有集合了所有 AIGC 服务商接口的 <b>AIGCCLOUD PYPI 包</b>，Python 开发者只需要安装一次后即可调用上述 AIGC 服务商的接口。


## APIGPT OpenAI
<img src="https://apigpt.cloud/wp-content/uploads/2023/05/OAI.png">

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
<img src="https://apigpt.cloud/wp-content/uploads/2023/06/claudeai.png">

APIGPT 的 ClaudeAI 是基于<a href='https://www.anthropic.com/product' target='_blank'>Anthropic ClaudeAI</a>而构建，它主要是用于对话的模型，用人工标注的对话数据集进行训练，Claude 的对话能力更强，能够进行更长更流畅的对话互动。它能一次处理最长长达9000个 Token 的内容。

## APIGPT BardAI
<img src="https://apigpt.cloud/wp-content/uploads/2023/05/600X3005.png">

<a href='https://bard.google.com/' target='_blank'>BardAI</a> 是 Google 基于对话应用语言模型 LaMDA 来构建，可以更准确，全面地理解自然语言，并且为用户提供及时的信息。

APIGPT 基于 Google BardAI 构建了 API 服务。

## APIGPT 百度文言一心

待补充

## APIGPT 阿里通义大模型

待补充


## APIGPT StableDiffusion
<img src="https://apigpt.cloud/wp-content/uploads/2023/05/600X3003.png">

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

在 APIGPT 中建立了一个 OpenAI App 后，你可以在你的应用程序中使用 OpenAI 的接口。

<a href='openai.html'>阅读 APIGPT.CLOUD - OpenAI 开发文档 >></a>

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
