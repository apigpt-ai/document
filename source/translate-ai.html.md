---
title: APIGPT.CLOUD - TranslateAI 开发文档

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
    content: Documentation for APIGPT.CLOUD TranslateAI
---

# APIGPT.Cloud - TranslateAI 开发文档

# 01 创建APP集成

登录 <a href='https://app.pgpt.cloud/'>APIGPT企业版</a>，在AI集成页面，点击`创建AI集成`，AI供应商选择`TranslateAI`。


# 02 API请求

## 认证
Translate API 使用 API 密钥进行身份验证。请访问你的 
<a href='https://app.pgpt.cloud/#/ai_integration'>App 页面</a>，以获取你在请求中使用的 API 密钥。

请记住，你的 API 密钥是一个秘密！不要与他人分享它，也不要在任何客户端代码（浏览器、应用程序）中公开它。生产请求必须通过你自己的后端服务器路由，你的 API 密钥可以从环境变量或密钥管理服务中安全加载。

所有 API 请求都应该在 `Authorization` HTTP 头中包含你的 API 密钥，如下所示：

`Authorization: Bearer <替换成从APIGPT.CLOUD创建的APP Key>`

## 获取支持语言

> language请求示范

```shell
curl https://ai.pgpt.cloud/v1/language/ \
-H "Content-Type: application/json" \
-H "Authorization: Bearer <API_KEY>" \
```

```python
import request

HOST = 'https://ai.pgpt.cloud/'
API_KEY = '<YOUR_API_KEY>'

header = {
    "Content-Type": "application/json",
    "Authorization": f"Bearer {API_KEY}",
}

res = requests.post(
    url=f"{HOST}/v1/language/",
    headers=headers,
)
print(res.json())

```

> 返回示范

```json
{
    "af": {
        "name": "Afrikaans",
        "nativeName": "Afrikaans",
        "dir": "ltr"
    },
    "am": {
        "name": "Amharic",
        "nativeName": "አማርኛ",
        "dir": "ltr"
    },
    "ar": {
        "name": "Arabic",
        "nativeName": "العربية",
        "dir": "rtl"
    },
    // ...
}
```

### Endpoint

`https://ai.pgpt.cloud/v1/language/`

### Method

`POST`

### Request Body
Null

### Response
返回所有支持的语言对象，key为请求翻译时传递的参数

## Translate

> translate请求示范

```shell
curl https://ai.pgpt.cloud/v1/translate/ \
-H "Content-Type: application/json" \
-H "Authorization: Bearer <API_KEY>" \
-d '{
    "to_lang": ['zh-Hans', 'pt', 'en'],
    "text": "下qqqqq表列出了国际语音字母 (IPA) 音素、扩展语音评估方法语音字母 (X-SAMPA) 符号以及亚马逊 Polly 支持的巴西葡萄牙语语音的相应变量。",
}'
```

```python
import request

HOST = 'https://ai.pgpt.cloud/'
API_KEY = '<YOUR_API_KEY>'

header = {
    "Content-Type": "application/json",
    "Authorization": f"Bearer {API_KEY}",
}
payload = {
    "to_lang": ['zh-Hans', 'pt', 'en'],
    "text": "下qqqqq表列出了国际语音字母 (IPA) 音素、扩展语音评估方法语音字母 (X-SAMPA) 符号以及亚马逊 Polly 支持的巴西葡萄牙语语音的相应变量。",
}

res = requests.post(
    url=f"{HOST}/v1/translate/",
    headers=headers,
    json=payload,
)
print(res.json())

```

> 返回示例

```json
{
    "translations": [
        [
            {
                "text": "下qqqqq表列出了国际语音字母 (IPA) 音素、扩展语音评估方法语音字母 (X-SAMPA) 符号以及亚马逊 Polly 支持的巴西葡萄牙语语音的相应变量。",
                "to": "zh-Hans"
            },
            {
                "text": "A tabela qqqqq a seguir lista as variáveis correspondentes para os fonemas do Alfabeto Internacional da Fala (IPA), os símbolos do Alfabeto Fonético do Método de Avaliação da Fala Estendida (X-SAMPA) e as vozes do Português Brasileiro suportadas pelo Amazon Polly.",
                "to": "pt"
            },
            {
                "text": "The following qqqqq table lists the corresponding variables for the International Speech Alphabet (IPA) phonemes, the Extended Speech Assessment Method Phonetic Alphabet (X-SAMPA) symbols, and the Brazilian Portuguese voices supported by Amazon Polly.",
                "to": "en"
            }
        ]
    ]
}
```

### Endpoint

`https://ai.pgpt.cloud/v1/translate/`

### Method

`POST`

### Request Body

#### 参数 text `string | array` required
要翻译的文本内容

#### 参数 to_lang `array` required
文本要翻译成哪种语言

### Response

#### 参数 translations `array`
根据请求参数 `to_lang` 中指定的翻译语言返回所有翻译完成的文本列表，包含翻译完成的文本内容及语言

参数 | 描述 
-----|----------
text | 翻译完成的文本
to | 翻译语言

