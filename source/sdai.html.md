---
title: APIGPT.CLOUD - Stable Diffusion 开发文档

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
    content: Documentation for APIGPT.CLOUD Stable Diffusion API
---

# APIGPT.Cloud - SDAI 开发文档


你可以通过任何语言的 HTTP 请求与 API 进行交互，可以使用 APIGPT 的 Python 库来调用 SDAI 的画图接口。

目前调用库正在开发中，可以先用 Python requests 库来调用。


# 01 认证
SDAI 使用 API 密钥进行身份验证。请访问你的 <a href=''>App 页面</a>，以获取你在请求中使用的 API 密钥。

所有 API 请求都应该在 `API-KEY` HTTP 头中包含你的 API 密钥，如下所示：
`API-KEY: <替换成从APIGPT.CLOUD创建的SDAI APP Key>`


# 02 发送请求
你可以将下面的命令粘贴到终端中以运行你的第一个 API 请求。请确保将 <API-KEY> 替换为你的秘密 API 密钥。


> 发送你的第一个 API 请求

```shell
curl https://sd.pgpt.cloud/v1/draw \
-H "Content-Type: application/json" \
-H "Authorization: Bearer <API-KEY>" \
-d '{
 "prompt": "cat"
}'
```

> 如果你会收到类下面JSON格式的数据响应，这说明你的请求成功了

```json
{
'urls': ['https:// ... img_url ...'],
'object': 'draw',
'prompt': 'cat',
'model': 'stable_diffusion_2_1',
'created': 1689738679,
'end_at': 1689738691
}
```


# 03 Draw APIs

给定一个提示，根据提示画出图

## API - Draw

`POST https://sd.pgpt.cloud/v1/draw`

根据提示来画图

### Request body

> Draw 请求示范

```python
```

```shell
curl https://sd.pgpt.cloud/v1/chat/completions \
-H "Content-Type: application/json" \
-H "Authorization: Bearer <API-KEY>" \
-d '{
 "prompt": "cat",
 "size": "16:9",
 "quantity": 2
}'
```


> Draw 请求示范打印结果

```json
{
'urls': ['https://... image_url1 ...', 'https://... image_url2 ...'],
'object': 'draw',
'prompt': 'cat',
'model': 'stable_diffusion_2_1',
'created': 1689738679,
'end_at': 1689738691
}
```

#### 参数 - prompt `string` Required
绘画的提示，Stable Diffusion 将根据 prompt 生成画

#### 参数 - size `quantity` Optional
生成图像的数量，可选参数，默认为1


#### 参数 - size `size` Optional
生成图像的长宽比，可选参数，支持以下：'16:9', '1:1', '9:16', '3:4', '4:3'



<aside class="notice">
目前仅支持文生图接口，StableDiffusion 其他特性正在开发中，如有您迫切需要我们添加支持的，请通过左方二维码联系我们
</aside>
