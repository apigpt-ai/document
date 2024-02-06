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
```python
import requests

headers = {
  "Content-Type": "application/json",
  "Authorization": "Bearer <API_KEY>"
}
url = "https://app.pgpt.cloud/api/open/app/"
app_data = {
    "name": "may app by usage 14",
    "desc": "may first app",
    "ai_type": "OpenAI",
    "plan": 1000,  # 选填指端: 1000, 2000, 5000, 10000 不填字段为不限额,
    "plan_type": "BY_USAGE"
}

res = requests.post(url, json=app_data, headers=headers)
print(res.json())
```

#### 参数 - name `string` Required

App的名字

#### 参数 - desc `string` Required

App的描述

#### 参数 - ai_type `string` Required

App的类型，可选类型有["OpenAI", "Claude"]

# 03 获得 APIGPT App 列表
`GET https://app.pgpt.cloud/api/open/app/`

>请求示范

```shell
curl https://app.pgpt.cloud/api/open/app/ \
-H "Content-Type: application/json" \
-H "Authorization: Bearer <API_KEY>"
```
```python
import requests

headers = {
  "Content-Type": "application/json",
  "Authorization": "Bearer <API_KEY>"
}
url = "https://app.pgpt.cloud/api/open/app/"
res = requests.get(url, headers=headers)
print(res)
```

>返回示例

```json
{
    "errno": 0,
    "data": [
        {
            "id": 181,
            "name": "rl的AI助手",
            "desc": null,
            "ai_type": "OpenAI",
            "key": "AG-OTgzZDYTc4YThhOGQTI2NTM5MzgxY2RhNzUxMTc=",
            "is_enabled": true,
            "created_at": "2023-12-21T02:24:35.070520Z",
            "plan": -1,
            "current_month_usage": "1.26"
        }
    ],
    "msg": "success"
}
```

### Request Params

#### 参数 - page `int` Optional Default to 1
指定的页码数

#### 参数 - page_size `int` Optional Default to 20
每页显示数据条数

#### 参数 - name `string` Optional
要查找的APP应用名称

### Response body

#### 参数 - errno `int`
错误码，0为成功

#### 参数 - data `array`
包含APP列表

data内各objects参数如下：

参数 | 类型       | 描述
-----|----------|-----------
id | `int`    | app id
name | `string` | app 名称
desc | `string` | app 描述
ai_type | `string` | app 供应商类型
key | `string` | app key
is_enabled | `bool`   | app 是否启用
created_at | `string` | app 创建时间
current_month_usage | `float` | 已花费的点数

#### 参数 - msg `string`
错误信息

# 04 获得 APIGPT App 详情
`GET https://app.pgpt.cloud/api/open/app/<App ID>/`

>请求示范

```shell
curl https://app.pgpt.cloud/api/open/app/ \
-H "Content-Type: application/json" \
-H "Authorization: Bearer <API_KEY>" \
```
```python
import requests

headers = {
  "Content-Type": "application/json",
  "Authorization": "Bearer <API_KEY>"
}
url = "https://app.pgpt.cloud/api/open/app/225/"
res = requests.get(url, headers=headers)
print(res.json())
```

>返回示范

```json
{
    "errno": 0,
    "data": {
        "id": 225,
        "name": "may app by usage 14",
        "desc": "may first app",
        "ai_type": "OpenAI",
        "key": "AG-NmFlOTdkMDBhNzhhNDY0ZDRjYmU5M2E4NWZhZjQ=",
        "is_enabled": true,
        "created_at": "2024-02-06T02:05:43.454699Z",
        "plan": null,
        "plan_type": "BY_USAGE",
        "balance": 0.0,
        "current_month_usage": "0.00",
        "total_usage": "0.00"
    },
    "msg": "success"
}
```

# 05 更新 APIGPT App
`PATCH https://app.pgpt.cloud/api/open/app/<App ID>/`

>请求示范

```shell
curl https://app.pgpt.cloud/api/open/app/<App ID>/ \
-H "Content-Type: application/json" \
-H "Authorization: Bearer <API_KEY>" \
-d '{
 "name": "TestOpenAI",
 "desc": "This is a test App for OpenAI",
 "is_enabled": false,
 "plan": 1000
}'
```
```python
import requests

headers = {
  "Content-Type": "application/json",
  "Authorization": "Bearer <API_KEY>"
}
url = "https://app.pgpt.cloud/api/open/app/225/"

update_data = {
    "name": "TestOpenAI",
    "desc": "This is a test App for OpenAI",
    "is_enabled": False,
    "plan": 1000
  }
res = requests.patch(url, json=update_data, headers=headers)
print(res.json())
```

### Request body

#### 参数 - name `string` Optional
app 名称

#### 参数 - desc `string` Optional
app 描述

#### 参数 - is_enabled `string` Optional
是否启用app，true-启用, false-禁用

#### 参数 - plan `int` Optional
使用限额，仅支持 1000, 2000, 5000, 10000

