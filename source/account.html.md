---
title: APIGPT.CLOUD - 应用管理接口

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
    content: Documentation for APIGPT.CLOUD Account Management API
---

# APIGPT.Cloud - 应用管理接口


# 01 认证
所有 账号管理API 请求都应该在 `ACCOUNT-KEY` HTTP 头中包含你的 账号密钥，如下所示：
`ACCOUNT-KEY: <替换成从APIGPT.CLOUD获得的账号密钥>`

你可以从以下地方获得账号密钥:

登录 -> 控制面板 -> 设置 -> 企业API -> 账号密钥

# 02 创建 APIGPT App

## API - Create App

`POST https://app.pgpt.cloud/api/open/app/`

创建一个App

### Request body

```shell
curl https://app.pgpt.cloud/api/open/app/ \
-H "Content-Type: application/json" \
-H "Authorization: Bearer <API_KEY>" \
-d '{
 "name": "TestOpenAI",
 "desc": "This is a test App for OpenAI",
 "ai_type": "OpenAI"
}'
```


#### 参数 - name `string` Required

App的名字

#### 参数 - desc `string` Required

App的描述

#### 参数 - ai_type `string` Required

App的类型，可选类型有["OpenAI", "Claude"]

# 03 获得 APIGPT App 列表
`GET https://app.pgpt.cloud/api/open/app/`

# 04 获得 APIGPT App 详情
`GET https://app.pgpt.cloud/api/open/app/<App ID>`

# 05 更新 APIGPT App
`PATCH https://app.pgpt.cloud/api/open/app/`
