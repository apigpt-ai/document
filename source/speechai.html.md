---
title: APIGPT.CLOUD - SpeechAI 开发文档

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
    content: Documentation for APIGPT.CLOUD SpeechAI
---

# APIGPT.Cloud - SpeechAI 开发文档

# 01 创建APP集成

登录 <a href='https://app.pgpt.cloud/'>APIGPT企业版</a>，在AI集成页面，点击`创建AI集成`，AI供应商选择`SpeechAI`。


# 02 API请求

## 认证
Speech API 使用 API 密钥进行身份验证。请访问你的 
<a href='https://app.pgpt.cloud/#/ai_integration'>App 页面</a>，以获取你在请求中使用的 API 密钥。

请记住，你的 API 密钥是一个秘密！不要与他人分享它，也不要在任何客户端代码（浏览器、应用程序）中公开它。生产请求必须通过你自己的后端服务器路由，你的 API 密钥可以从环境变量或密钥管理服务中安全加载。

所有 API 请求都应该在 `Authorization` HTTP 头中包含你的 API 密钥，如下所示：

`Authorization: Bearer <替换成从APIGPT.CLOUD创建的APP Key>`


## 语音转文本

> speech2text 请求示范

```shell
curl https://ai.pgpt.cloud/v1/speech/speech2text \
-H "Content-Type: application/json" \
-H "Authorization: Bearer <API_KEY>" \
-d '{
    'lang': 'en-US',
}'
-F "audio=@/path/to/audio.wav"
```

```python
import request

HOST = 'https://ai.pgpt.cloud/'
API_KEY = '<YOUR_API_KEY>'

url = f'{HOST}/v1/speech/speech2text'
headers = {
    'accept': 'application/json',
    "Authorization": f"Bearer {API_KEY}"
}
data = {
    'lang': 'en-US',
}
files = [
    ('audio', ('en-US_0.wav', open('../en-US_0.wav', 'rb'), 'audio/wav')),
]
response = requests.request("POST", url, headers=headers, data=data, files=files)
print(response.json())
```

>response

```json
{
    "text": "Today was a beautiful day. We had a great time taking along Long walk In the morning. The county slide was in full bloom, yet the air was crisp and cold. Towards the end of the day, clouds came in forecasting much needed rain."
}
```

### Endpoint

`https://ai.pgpt.cloud/v1/speech/speech2text`

### Method

`POST`

### Request Body

#### 参数 audio `file` required
上传语音文件，仅支持 `audio/amr` 及 `audio/wav` 两种格式的音频

#### 参数 lang `string` required
语音文件所用的语言，默认使用`en-US`，常用的语言代码如下

区域设置 | 语言 
-----|----------
de-DE | 德语（德国）
en-GB | 英语（英国）
en-US | 英语（美国）
es-ES | 西班牙语（西班牙）
js-JP | 日语（日本）
ko-KR | 韩语（韩国）
pt-PT | 葡萄牙语（葡萄牙）
ru-RU | 俄语（俄罗斯）
th-TH | 泰语（泰国）
wuu-CN | 中文（吴语）
yue-CN | 中文（粤语）
zh-CN | 中文（普通话）

### Response

#### 参数 text `string`
语音识别出来的文本数据


## 文本转语音

> text2speech 请求示范

```shell
curl https://ai.pgpt.cloud/v1/speech/text2speech \
-H "Content-Type: application/json" \
-H "Authorization: Bearer <API_KEY>" \
-d '{
    'voice_name': 'en-US-JennyNeural',
    'text': 'The inquiry examined accusations of potential links between drug traffickers and close confidants of President Andrés Manuel López Obrador while he governed the country.',
}'
```

```python
import requests

HOST = 'https://ai.pgpt.cloud/'
API_KEY = '<YOUR_API_KEY>'

url = f'{HOST}/v1/speech/text2speech'
headers = {
    'accept': 'application/json',
    "Authorization": f"Bearer {KEY}"
}
data = {
    'voice_name': 'en-US-JennyNeural',
    'text': 'The inquiry examined accusations of potential links between drug traffickers and close confidants of President Andrés Manuel López Obrador while he governed the country.',
}
response = requests.post(url, headers=headers, json=data)
print(response.json())
```

>response

```json
{
    "text": "The inquiry examined accusations of potential links between drug traffickers and close confidants of President Andrés Manuel López Obrador while he governed the country.",
    "url": "https://silkroadtech.oss-cn-shenzhen.aliyuncs.com/pgpt-ai/speech/202402/589cfed33ed97e5707a672f16d8150ef.wav",
    "duration": 10.45
}
```

### Endpoint

`https://ai.pgpt.cloud/v1/speech/text2speech`

### Method

`POST`


### Request Body

#### 参数 voice_name `string` required
指定音频要使用的声音，可使用获取语言api查找支持的语言

#### 参数 text `string` required
要转换成语音的文本

### Rsponse

#### 参数 text `string`
转换的文本

#### 参数 url `string`
生成的音频文件链接，可通过链接下载到音频文件

#### 参数 duration `float`
音频时长，按秒计


## 获取支持的语言

> get voices 请求示范

```shell
curl https://ai.pgpt.cloud/v1/speech/text2speech/voices \
-H "Content-Type: application/json" \
-H "Authorization: Bearer <API_KEY>" \
```

```python
import requests

HOST = 'https://ai.pgpt.cloud/'
API_KEY = '<YOUR_API_KEY>'

url = f'{HOST}/v1/speech/text2speech/voices'
headers = {
    'accept': 'application/json',
    "Authorization": f"Bearer {KEY}"
}
response = requests.post(url, headers=headers)
print(response.json())
```

> 返回示范

```json
[
    {
        "Name": "Microsoft Server Speech Text to Speech Voice (af-ZA, AdriNeural)",
        "DisplayName": "Adri",
        "LocalName": "Adri",
        "ShortName": "af-ZA-AdriNeural",
        "Gender": "Female",
        "Locale": "af-ZA",
        "LocaleName": "Afrikaans (South Africa)",
        "SampleRateHertz": "48000",
        "VoiceType": "Neural",
        "Status": "GA",
        "WordsPerMinute": "147"
    }
]
```

### Endpoint

`https://ai.pgpt.cloud/v1/speech/text2speech/voices`

### Method

`POST`


### Request Body
Null

### Response
包含所支持的所有声音列表，需要将所选择的声音的 `ShortName` 参数值放入请求的 `voice_name` 中

