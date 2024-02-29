---
title: APIGPT.CLOUD - GeminiAI 开发文档

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
    content: Documentation for APIGPT.CLOUD GeminiAI
---

# APIGPT.Cloud - GeminiAI 开发文档

# 01 创建APP集成

登录 <a href='https://app.pgpt.cloud/'>APIGPT企业版</a>，在AI集成页面，点击`创建AI集成`，AI供应商选择`GeminiAI`。


# 02 API请求

## 认证
GeminiAI API 使用 API 密钥进行身份验证。请访问你的 
<a href='https://app.pgpt.cloud/#/ai_integration'>App 页面</a>，以获取你在请求中使用的 API 密钥。

请记住，你的 API 密钥是一个秘密！不要与他人分享它，也不要在任何客户端代码（浏览器、应用程序）中公开它。生产请求必须通过你自己的后端服务器路由，你的 API 密钥可以从环境变量或密钥管理服务中安全加载。

所有 API 请求都应该在 `Authorization` HTTP 头中包含你的 API 密钥，如下所示：

`Authorization: Bearer <替换成从APIGPT.CLOUD创建的APP Key>`


## 发送请求

> gemini-pro 请求示范

```shell
curl https://ai.pgpt.cloud/gemini/v1/chat/completion \
-H "Content-Type: application/json" \
-H "Authorization: Bearer <API_KEY>" \
-d '{
    "model": "gemini-pro",
    "contents": [
        {
            "role": "user",
            "parts": [
                {
                    "text": "太阳系"
                },
            ]
        }
    ],
    "stream": false
}
'
```

```python
import requests

HOST = 'https://ai.pgpt.cloud/'
API_KEY = '<YOUR_API_KEY>'

url = f'{HOST}/gemini/v1/chat/completions'
headers = {
    'accept': 'application/json',
    "Authorization": f"Bearer {KEY}"
}
payload = {
    "model": "gemini-pro",
    "contents": [
        {
            "role": "user",
            "parts": [
                {
                    "text": "太阳系"
                },
            ]
        }
    ],
    "stream": False
}
response = requests.post(url, headers=headers, json=payload)
print(response.json())
```

> gemini-pro-vision 请求示范

```shell
echo '{
  "contents":[
    {
      "parts":[
        {"text": "What is this picture?"},
        {
          "inline_data": {
            "mime_type":"image/jpeg",
            "data": "'$(base64 -w0 image.jpg)'"
          }
        }
      ]
    }
  ]
}' > request.json

curl https://ai.pgpt.cloud/gemini/v1/chat/completion \
-H "Content-Type: application/json" \
-H "Authorization: Bearer <API_KEY>" \
-d @request.json
```

```python
import requests
from meutils.io.image import image_to_base64

HOST = 'https://ai.pgpt.cloud/'
API_KEY = '<YOUR_API_KEY>'

url = f'{HOST}/gemini/v1/chat/completions'
headers = {
    'accept': 'application/json',
    "Authorization": f"Bearer {KEY}"
}
image_data = image_to_base64('test-assets/test1.jpg', for_image_url=False)
payload = {
    "model": "gemini-pro-vision",
    "contents": [
        {
            "role": "user",
            "parts": [
                {
                    "text": "这个图上有什么"
                },
                {
                    "inline_data": {
                        "mime_type": "image/jpeg",
                        "data": image_data
                    }
                }
            ]
        }
    ],
    "stream": False
}
response = requests.post(url, headers=headers, json=payload)
print(response.json())
```

> 返回示范

```json
{
    "message": "太阳系是一个由太阳、八大行星、矮行星、卫星、彗星、小行星等天体组成的系统。太阳系位于银河系中，是银河系中已知唯一存在生命的行星系"
}
```

### Endpoint

`https://ai.pgpt.cloud/gemini/v1/chat/completions`

### Method

`POST`


### Request Body

#### 参数 model `string` required
指定要使用的模型，仅支持 `gemini-pro` 及  `gemini-pro-vision`.

 `gemini-pro` 仅支持文本聊天
 
  `gemini-pro-vision` 支持图片解析，使用该模型时传递的消息内容必须包含文件数据

#### 参数 contents `array[content]` required
聊天内容，包含对话历史+最新请求，`contents` 包含content对象列表，参数如下:

content字段 | 类型 | 描述
------ | ------- | -----------
parts | array[part] | 单个消息的有序部件，包含 part 对象
role | string | 用户角色，只能是 user 或者 model

part字段 | 类型 | 描述
------ | ------- | -----------
text | string | 文本消息
inline_data | object[blob] |  文件数据对象

blob字段 | 类型 | 描述
------ | ------- | -----------
mime_type | string | 文件类型，支持"image/png", "image/jpeg", "image/heic", "image/heif", "image/webp".
data | object[blob] |  文件base64数据

注意：parts参数中，`text` 与 `inline_data` 必须在独立的object中，不可放在一起。

#### 参数 stream `boolean` optional default to false
设置消息返回的形式，为 `true` 时，返回的是实时的流数据片段，为 `false` 时返回的是完整的消息

#### 参数 - temperature `number` Optional Defaults to 1

要使用的采样温度，介于0和2之间。较高的值（如0.8）会使输出更加随机，而较低的值（如0.2）会使输出更加集中和确定性。

#### 参数 max_tokens `integer` Optional Defaults to 4096

在聊天补全中生成的最大令牌数。
输入令牌和生成令牌的总长度受模型上下文长度的限制。

### Response

#### 参数 message  `string`
根据问题返回的消息

