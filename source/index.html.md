---
title: APIGPT CLOUD 用户文档

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
    content: Documentation for APIGPT CLOUD API
---

# 生成式 AI 云（APIGPT CLOUD）用户手册



# 01 - 关于APIGPT

## 服务介绍
生成式 AI 云（简称 APIGPT）是一款生成式 AI 云服务，旨在为开发者提供一站式集成多个 AIGC 服务商 API 的服务。只需开通一个 APIGPT.CLOUD 账号，开发者即可稳定访问包括 <b>OpenAI 官方</b>，<b>Azure OpenAI</b>、<b>ChatGLM</b>、<b>Claude AI</b>、<b>Google PaLM AI</b>、<b>Stable Diffusion</b> 在内的多项生成式 AI API，轻松集成生成式AI能力到自己的应用中。让 APIGPT.CLOUD 成为您的生成式AI云服务，将极大地提高您的开发效率。

此外，基于开发者的需求，我们开发了具备内容生成、图像生成的<b> AGIEditor 编辑器组件</b>，方便开发者使用；还有集合了所有 AIGC 服务商接口的 <b>AIGCCLOUD PYPI 包</b>，Python 开发者只需要安装一次后即可调用上述 AIGC 服务商的接口。


## 为什么应该选择 APIGPT
和原 AIGC 官方的 API 相比，APIGPT 的 API 服务有以下优势：

- 无前置审核流程，注册完成账号即可使用，充值方式简单且多样
- 对官方接口进行了必要的优化和简化，让开发者使用更方便
- 提供跨 AIGC 服务整合的能力，能让用户方便地使用最有方案
- 提供及时的技术专家支持服务



# 02 - 快速入门


## 注册账号
通过和我方的客户经理沟通后，经由客户经理提供的注册链接注册后，即可拥有了方便访问各个 AIGC 服务 API 的权限。

<img src='https://apigpt.cloud/wp-content/uploads/2023/07/apply-for-apigpt.png' />

在注册页面提交账号信息后进入到资料填写页面，在此处选择 APIGPT 服务，最后提交，无需审核，即可马上开通账号。

## 创建App
注册成功后，点击后即可进入到控制面板，通过左侧菜单的 API Integration 即可通过创建 App 的方式获得 API Integration，新建一个 App 后点击提交，即可获得访问对应 AIGC 服务的 API Key。（如App处于审核状态通，则可以联系我方项目经理沟通审核后开通，企业版的用户创建的App是自动通过审核状态）

<img src='https://apigpt.cloud/wp-content/uploads/2023/05/2-1.png'>


## 获得接入到第三方应用的 Token

获得上述 API Key 后，即可在各 AIGC App 中使用。

<img src='https://apigpt.cloud/wp-content/uploads/2023/05/3-1.png' />

APIGPT.CLOUD 针对各个 AIGC 服务商提供的 API 绝大部分都兼容于原 AIGC 官方 APII，可以无缝切换。


## 试用与充值

默认注册后，我们都会免费赠送 5000P 额度供你使用，使用完毕后，您可以随时通过充值购买额度。

# 03 - AIGC AI集成

AIGC 的 AI集成模块主要为开发者提供了直接接入各个常见大语言模型（主要是文字模型）能力的接口。
对于一些需要部署的大预言模型，如ChatGLM等，我们也都自行搭建了对应的运算集群，开发者只需要调用接口即可使用。

## APIGPT OpenAI

<img src="https://apigpt.cloud/wp-content/uploads/2023/05/OAI.png">

APIGPT 的 OpenAI 是基于 <a href='https://learn.microsoft.com/zh-cn/azure/cognitive-services/openai/overview' target='_blank'>Azure OpenAI</a> 的服务构建。

通过 APIGPT OpenAI 可使用很多不同模型，这些模型按系列和功能分组。 模型系列通常按其预期任务关联模型。 下表介绍了 Azure OpenAI 中当前可用的模型系列。 目前并非所有模型都可在所有区域中使用。

APIGPT OpenAI 目前支持的模型包括并不限于下列：

模型组 | 模型ID | 限制 | 描述
--------- | ------- | ----------- | -----------
GPT-4 | gpt-4 | 8192 | 与任何 OpenAI 以前的模型相比，GPT-4 可以更准确地解决难题，与 GPT-35-TURBO 一样，GPT-4 针对聊天进行了优化，但适用于传统的完成任务。
GPT-4 | gpt-4-32k | 32k | 支持32k Token传输的GPT-4模型
GPT-4 | gpt-4-turbo | 128k | GPT-4-Turbo支持长达128K的Token输入，同时知识库更新为2023年3月。
GPT-4 | gpt-4-turbo-vision     | 128k | GPT-4-TURBO-VISION 是多模态模型，融合了自然语言处理和视觉理解，能够分析图像并对相关问题提供文字回答。
GPT-3.5 | gpt-3.5-turbo | 4096 | GPT-35-TURBO 是一种专为对话接口设计的语言模型
GPT-3.5 | gpt-3.5-turbo-16k | 16k | GPT-35-TURBO-16K 是 GPT-35-TURBO 的增强版，可以支持高达16k的 Token输入
GPT-3.5 | gpt-3.5-turbo-instruct | 4097 | GPT-35-TURBO-INSTRUCT 是为了给予特定的指令而设计的，可以根据指令来分析和处理相关资料。
Embeddings | text-embedding-ada-002 | 8191 | 一组可以理解和使用嵌入的模型。 嵌入是一种特殊的数据表示格式，可由机器学习模型和算法轻松使用。 嵌入是一段文本的语义含义的信息密集表示。
Codex | code-davinci-002 | 8001 | Codex 模型是基模型 GPT-3 的子代，可以理解和生成代码。 它们的训练数据包含自然语言和来自 GitHub 的数十亿行公开代码。


在 APIGPT 中建立了一个 OpenAI App 后，你可以在你的应用程序中使用 OpenAI 的接口。

<a href='openai.html'>阅读 APIGPT CLOUD - OpenAI 开发文档 >></a>

## APIGPT ClaudeAI

<img src="https://apigpt.cloud/wp-content/uploads/2023/06/claudeai.png">

APIGPT 的 ClaudeAI 是基于<a href='https://www.anthropic.com/product' target='_blank'> Anthropic Claude </a>而构建，它主要是用于对话的模型，用人工标注的对话数据集进行训练，Claude 的对话能力更强，能够进行更长更流畅的对话互动。我们目前提供两个系列的模型，它们都支持100000个令牌上下文窗口：

APIGPT ClaudeAI 目前支持的模型包括并不限于下列：

家族 | 最新主要版本 | 最新完整版本 | 描述
--------- | ------- | ----------- | -----------
Claude Instant | claude-instant-1 | claude-instant-1.2 | 低延迟、高吞吐量
Claude | claude-2 | claude-2.0 | 在需要复杂推理的任务上表现出色


在 APIGPT 中建立了一个 ClaudeAI App 后，你可以在你的应用程序中使用 ClaudeAI 的接口。

<a href='claudeai.html'>阅读 APIGPT CLOUD - ClaudeAI 开发文档 >></a>

## APIGPT ChatGLM

<img src="https://apigpt.cloud/wp-content/uploads/2023/06/ChatGLM-logo.png">

ChatGLM 使用类似于 ChatGPT 的技术，专门针对中文问答和对话进行了优化。经过约1T标识符的中英双语训练，结合监督微调、反馈自助、人类反馈强化学习等技术的加持，拥有62亿参数的 ChatGLM-6B 已经能够生成与人类偏好相当符合的回答。

在 APIGPT 中建立一个 ChatGLM2-6B App后，你就可以在你的应用程序中使用 ChatGLM-6B 的接口。


<a href='chatglm2-6b.html'>阅读 APIGPT CLOUD - ChatGLM2-6B 开发文档 >></a>


## APIGPT PaLM

<img src="https://apigpt.cloud/wp-content/uploads/2023/09/PaLM-AI.png">

PaLM AI 是 Google 用于构建 <a href='https://bard.google.com/' target='_blank'>Bard</a> 的大语言模型，基于Google的技术和积累，它准确全面地理解自然语言，能为用户提供及时有效的信息。

APIGPT 基于 Google PaLM 构建了 API 服务。


<a href='#'>APIGPT CLOUD - PaLM 接口在完善中... >></a>


# 04 - AIGC AI画图

AIGC 的 API画图模块主要为开发者提供了直接调用各个AI画图系统能力的接口，目前我们主要提供了Stable Diffusion系统的能力输出，开发者无需自行搭建，通过接口即可调用相关AI作图的能力。

## APIGPT StableDiffusion

<img src="https://apigpt.cloud/wp-content/uploads/2023/05/SD.png">

<a href='https://stablediffusionweb.com/' target='_blank'>Stable Diffusion</a> 是AI画图领域中的一种潜在扩散模型方案（Latent Diffusion Model），它能够从文本描述中生成详细的图像。它还可以用于图像修复、图像绘制、文本到图像和图像到图像等任务。简单地说，我们只要给出想要的图片的文字描述在提 Stable Diffusion 就能生成符合你要求的逼真的图像！

而现在对于很多开发者而言，如何快速获得一个可以立即上手的 Stable Diffusion 环境是最大的门槛，基于此，APIGPT 搭建了GPU 算力云，为用户提供了便捷的 Stable Diffusion API，开发者无需自行折腾繁琐的算力服务器，大大节省了时间和效率。


你只需要在 APIGPT 中建立了一个 SDAI App 后，就可以在你的应用程序中使用 SDAI 的接口。

<a href='sdai.html'>阅读 APIGPT CLOUD - SDAI 开发文档 >></a>




# 05 - AIGC AI问答

现有的大预言模型提供了很强大的语言处理能力，但并未对各种应用场景提供信息存储、便捷工具等方案。APIGPT 通过集成了向量存储等周边服务的能力，扩展出了 APIGPT AI问答 服务，方便开发者获得一种开箱即用的服务对接能力。

<a href='aiqa.html'>阅读 APIGPT CLOUD - AI问答 开发文档 >></a>

# 06 - AIGC 应用管理

为方便服务整合，我们同时提供了应用管理接口（企业级用户可以开启使用），方便您直接使用 API 接口来管理 AIGC APP。


<a href='account.html'>阅读 APIGPT CLOUD - 应用管理接口 >></a>

# 07 - 负责任的 AIGC

## 内容安全

根据国家法律，我们应用了基础的安全规则，避免非法信息的生成。也需要开发者再使用时需要注意不让非法内容进入，我们会给予监督和管理。

## 隐私保护

