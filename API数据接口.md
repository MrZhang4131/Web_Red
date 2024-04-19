---
title: J2EE课设 v1.0.0
language_tabs:
  - shell: Shell
  - http: HTTP
  - javascript: JavaScript
  - ruby: Ruby
  - python: Python
  - php: PHP
  - java: Java
  - go: Go
toc_footers: []
includes: []
search: true
code_clipboard: true
highlight_theme: darkula
headingLevel: 2
generator: "@tarslib/widdershins v4.0.17"

---

# J2EE课设

> v1.0.0

Base URLs:

# 登录

## POST 普通用户登录

POST /user/userLogin

发送完短信验证码，后端将短信验证码存储到redis，到Redis中查看短信验证码，并提交以下json参数，后端对用户名，密码，短信验证码进行登录校验，登录成功将返回用户信息和token，token包含了部分用户信息和加密的校验信息用于登录后访问时后端进行校验，判断当前访问者是否为当前用户。

> Body 请求参数

```json
{
  "username": "xm",
  "password": "123456",
  "phone": "13850429387",
  "code": "135518"
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|body|body|object| 否 ||none|
|» username|body|string| 是 ||none|
|» password|body|string| 是 ||none|
|» phone|body|string| 是 ||none|
|» code|body|string| 是 | 短信验证码|none|
|» userType|body|string| 是 | 用户类型|admin为管理员用户，normal为普通用户|

> 返回示例

> 成功

```json
{
  "user": {
    "created": "2023-04-24T12:22:55.000+00:00",
    "updated": "2023-05-04T07:17:47.000+00:00",
    "id": 1,
    "username": "xm",
    "password": "123456",
    "phone": "13850429386",
    "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/4.jpg",
    "gender": 1,
    "age": 22,
    "introduction": "无",
    "userType": "admin"
  },
  "token": "eyJhbGciOiJIUzUxMiJ9.eyJwYXNzd29yZCI6IjEyMzQ1NiIsImlkIjoxLCJleHAiOjE2ODUwNDMyMzUsInVzZXJuYW1lIjoieG0ifQ.u8825pLXjMhBmj6BWMP1hEieL0t6ifckJqhBPgy_v6pGhz98HExqNnQSBObaJtWuKgMROuzXmyo-9TNtpSHrUg"
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» user|object|true|none||none|
|»» created|string|true|none||none|
|»» updated|string|true|none||none|
|»» id|integer|true|none||none|
|»» username|string|true|none||none|
|»» password|string|true|none||none|
|»» phone|string|true|none||none|
|»» headphoto|string|true|none||none|
|»» gender|integer|true|none||none|
|»» age|integer|true|none||none|
|»» introduction|string|true|none||none|
|» token|string|true|none||none|

## POST 用户注册

POST /user/register

提交以下参数和头像上传时返回的图片URL地址进行用户注册

> Body 请求参数

```json
{
  "username": "string",
  "password": "string",
  "headphoto": "string",
  "gender": 0,
  "age": 0,
  "introduction": "string",
  "phone": "string"
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|body|body|object| 否 ||none|
|» username|body|string| 是 ||none|
|» password|body|string| 是 ||none|
|» headphoto|body|string| 是 | 头像|none|
|» gender|body|integer| 是 | 性别|男1，女0|
|» age|body|integer| 是 ||none|
|» introduction|body|string| 是 | 简介|none|
|» phone|body|string| 是 ||none|

> 返回示例

> 成功

```json
"注册成功"
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|null|

## POST 头像上传

POST /user/headphoto

用户注册时进行头像上传，后端将文件解析上传到阿里云并返回图片的URL地址

> Body 请求参数

```yaml
headphoto: string

```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|body|body|object| 否 ||none|
|» headphoto|body|string(binary)| 是 ||none|

> 返回示例

> 成功

```json
"https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/2023/04/27/a9be04f3-f969-46bf-acce-6f5a1426a31a.jpg"
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» headphotoUrl|string|true|none|用户头像url|none|

## POST 发送短信验证码

POST /user/smsLogin

发送短信验证码，并提交手机号码

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|phone|query|string| 是 ||none|

> 返回示例

> 成功

```json
465384
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

## POST 管理员后台登录

POST /user/adminLogin

发送完短信验证码，后端将短信验证码存储到redis，到Redis中查看短信验证码，并提交以下json参数，后端对用户名，密码，短信验证码进行登录校验，登录成功将返回用户信息和token，token包含了部分用户信息和加密的校验信息用于登录后访问时后端进行校验，判断当前访问者是否为当前用户。

> Body 请求参数

```json
{
  "username": "xm",
  "password": "123456",
  "phone": "13850429387",
  "code": "135518"
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|body|body|object| 否 ||none|
|» username|body|string| 是 ||none|
|» password|body|string| 是 ||none|
|» phone|body|string| 是 ||none|
|» code|body|string| 是 | 短信验证码|none|
|» userType|body|string| 是 | 用户类型|admin为管理员用户，normal为普通用户|

> 返回示例

> 成功

```json
{
  "user": {
    "created": "2023-04-24T12:22:55.000+00:00",
    "updated": "2023-05-04T07:17:47.000+00:00",
    "id": 1,
    "username": "xm",
    "password": "123456",
    "phone": "13850429386",
    "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/4.jpg",
    "gender": 1,
    "age": 22,
    "introduction": "无",
    "userType": "admin"
  },
  "token": "eyJhbGciOiJIUzUxMiJ9.eyJwYXNzd29yZCI6IjEyMzQ1NiIsImlkIjoxLCJleHAiOjE2ODUwNDMyMzUsInVzZXJuYW1lIjoieG0ifQ.u8825pLXjMhBmj6BWMP1hEieL0t6ifckJqhBPgy_v6pGhz98HExqNnQSBObaJtWuKgMROuzXmyo-9TNtpSHrUg"
}
```

```json
{
  "errorCode": "000003",
  "errMessage": "验证码无效"
}
```

```json
{
  "errorCode": "000002",
  "errMessage": "密码错误"
}
```

```json
{
  "errorCode": "000001",
  "errMessage": "用户不存在"
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» user|object|true|none||none|
|»» created|string|true|none||none|
|»» updated|string|true|none||none|
|»» id|integer|true|none||none|
|»» username|string|true|none||none|
|»» password|string|true|none||none|
|»» phone|string|true|none||none|
|»» headphoto|string|true|none||none|
|»» gender|integer|true|none||none|
|»» age|integer|true|none||none|
|»» introduction|string|true|none||none|
|» token|string|true|none||none|

# 发现

## GET 发现首页面

GET /found

提交登录时，后端响应的token，后端响应一个map集合，包含推荐笔记和所有笔记，笔记包含note和user对象

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|Authorization|header|string| 是 ||none|

> 返回示例

> 成功

```json
{
  "推荐笔记": [
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-29T03:45:09.000+00:00",
        "id": 24,
        "userId": 1,
        "username": "xm",
        "title": "真实经历，这些坑希望你在平潭千万不要踩",
        "content": "血泪教训，想近期平潭环岛游的uu们请收下这份环岛拍照/路线攻略和避坑指南！",
        "tag": "旅行",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%97%85%E8%A1%8C/%E5%9B%BE%E7%89%87/1/28eb92a6ea0dcfa9819da74027fb81f.png",
        "praisenum": 433,
        "collectionnum": 456,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-24T12:22:55.000+00:00",
        "updated": "2023-05-04T07:17:47.000+00:00",
        "id": 1,
        "username": "xm",
        "password": "123456",
        "phone": "13850429386",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/4.jpg",
        "gender": 1,
        "age": 22,
        "introduction": "无",
        "userType": "admin"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 31,
        "userId": 24,
        "username": "驰名",
        "title": "第一次来长沙玩的姐妹进来",
        "content": "长沙好吃的真的太多啦！一条视频根本讲不完",
        "tag": "美食",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%BE%8E%E9%A3%9F/%E8%A7%86%E9%A2%91/1/%E5%B0%81%E9%9D%A2.png",
        "praisenum": 458,
        "collectionnum": 56,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:41:00.000+00:00",
        "updated": null,
        "id": 24,
        "username": "驰名",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/4.jpg",
        "gender": 1,
        "age": 30,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 33,
        "userId": 26,
        "username": "Vanessa",
        "title": "breakfast蒜香芝士厚吐司",
        "content": "早餐不知道吃什么的姐们快试试这款蒜香吐司 口感真的绝了！外脆里嫩搭配芝士好吃到停不下来",
        "tag": "美食",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%BE%8E%E9%A3%9F/%E8%A7%86%E9%A2%91/3/%E5%B0%81%E9%9D%A2.png",
        "praisenum": 356,
        "collectionnum": 546,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:41:02.000+00:00",
        "updated": null,
        "id": 26,
        "username": "Vanessa",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/41.jpg",
        "gender": 1,
        "age": 32,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 13,
        "userId": 12,
        "username": "麻豆同学",
        "title": "双矮子乐时髦又百搭的厚底鞋 无痛增高",
        "content": "你们期待已久的增高鞋分享来咯\r\n都是比较时髦又有点复古味道的厚底鞋\r\n在我这里出镜率也是超高的！\r\n这几款不论是配色上还是舒适度都没话说\r\n主要真的显高又显瘦",
        "tag": "穿搭",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%A9%BF%E6%90%AD/%E8%A7%86%E9%A2%91/2/2.png",
        "praisenum": 3547,
        "collectionnum": 897,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:40:33.000+00:00",
        "updated": null,
        "id": 12,
        "username": "麻豆同学",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/27.jpg",
        "gender": 0,
        "age": 18,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 41,
        "userId": 31,
        "username": "票",
        "title": "拍烂片？败名声？到底图什么？",
        "content": "3楼跳下来 背摔没有任何措施，别催牛逼 我不信。什么概念 ",
        "tag": "其它",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E5%85%B6%E5%AE%83/%E8%A7%86%E9%A2%91/1/%E5%B0%81%E9%9D%A2.png",
        "praisenum": 6543,
        "collectionnum": 6,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:41:06.000+00:00",
        "updated": null,
        "id": 31,
        "username": "票",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/47.jpg",
        "gender": 1,
        "age": 37,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 9,
        "userId": 8,
        "username": "吴",
        "title": "Tequila Sunrise",
        "content": "夏天就是积攒美好回忆的",
        "tag": "家居",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%8E%A8%E8%8D%90/%E5%9B%BE%E7%89%87/6/270ca884eb1950ec1a652ca3765ba4f.png",
        "praisenum": 3333,
        "collectionnum": 568,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:40:21.000+00:00",
        "updated": "2023-04-25T11:40:23.000+00:00",
        "id": 8,
        "username": "吴",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/22.jpg",
        "gender": 1,
        "age": 14,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 44,
        "userId": 34,
        "username": "阿棒的觅食计划",
        "title": "愿每个去长沙的人都能刷到",
        "content": "马上五一假期了，好多朋友来长沙旅游！作为在长沙学习生活7年的土著，给大家整理了「2天1夜的自由行线路攻略」，有需要的宝子可以参考我的行程哦！一点不会踩雷！",
        "tag": "其它",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E5%85%B6%E5%AE%83/%E5%9B%BE%E7%89%87/1/0e4e98e85cac442efe792e7a7330a88.png",
        "praisenum": 673,
        "collectionnum": 486,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:41:09.000+00:00",
        "updated": null,
        "id": 34,
        "username": "阿棒的觅食计划",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/50.jpg",
        "gender": 1,
        "age": 40,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 21,
        "userId": 17,
        "username": "日空山",
        "title": "风景",
        "content": "当然蓝玫瑰坠入克莱因蓝的海，未曾谋面也终会相遇",
        "tag": "旅行",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%97%85%E8%A1%8C/%E8%A7%86%E9%A2%91/1/8.png",
        "praisenum": 236,
        "collectionnum": 435,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:40:48.000+00:00",
        "updated": null,
        "id": 17,
        "username": "日空山",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/32.jpg",
        "gender": 1,
        "age": 23,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 35,
        "userId": 28,
        "username": "菠萝派",
        "title": "再发一遍！这个巨巨巨下饭！！",
        "content": "奶奶做的几十年的酱油手撕鸡腿好好吃，一星期做了好多吃呢",
        "tag": "美食",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%BE%8E%E9%A3%9F/%E5%9B%BE%E7%89%87/2/c66fb62cbcd24f8dd1a568f0dcdc61a.png",
        "praisenum": 4567,
        "collectionnum": 546,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:41:04.000+00:00",
        "updated": null,
        "id": 28,
        "username": "菠萝派",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/43.jpg",
        "gender": 1,
        "age": 34,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-29T03:45:09.000+00:00",
        "id": 40,
        "userId": 1,
        "username": "xm",
        "title": "今天喝19.9，的椰奶星冰乐",
        "content": "星巴克奶油星冰乐换巴旦木奶，椰浆，可可碎片",
        "tag": "美食",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%BE%8E%E9%A3%9F/%E5%9B%BE%E7%89%87/7/ab53ff3630fb1cec529500bf4f518c2.png",
        "praisenum": 654,
        "collectionnum": 846,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-24T12:22:55.000+00:00",
        "updated": "2023-05-04T07:17:47.000+00:00",
        "id": 1,
        "username": "xm",
        "password": "123456",
        "phone": "13850429386",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/4.jpg",
        "gender": 1,
        "age": 22,
        "introduction": "无",
        "userType": "admin"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 11,
        "userId": 10,
        "username": "阿泽爱吃面",
        "title": "三步让你窄干衣服饭价值",
        "content": "这条视频不看真的能让你后悔一年",
        "tag": "穿搭",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%A9%BF%E6%90%AD/%E8%A7%86%E9%A2%91/1/1.jpg",
        "praisenum": 467,
        "collectionnum": 86,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:40:28.000+00:00",
        "updated": null,
        "id": 10,
        "username": "阿泽爱吃面",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/24.jpg",
        "gender": 1,
        "age": 16,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-29T03:45:09.000+00:00",
        "id": 2,
        "userId": 1,
        "username": "xm",
        "title": "巴黎世家特卖会",
        "content": "开心看看买了啥",
        "tag": "家居",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%8E%A8%E8%8D%90/%E8%A7%86%E9%A2%91/2/%E5%B0%81%E9%9D%A2.png",
        "praisenum": 1423,
        "collectionnum": 68,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-24T12:22:55.000+00:00",
        "updated": "2023-05-04T07:17:47.000+00:00",
        "id": 1,
        "username": "xm",
        "password": "123456",
        "phone": "13850429386",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/4.jpg",
        "gender": 1,
        "age": 22,
        "introduction": "无",
        "userType": "admin"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 6,
        "userId": 5,
        "username": "安仔",
        "title": "一个男生挚爱的6瓶香水",
        "content": "分享春夏喜欢的6支香水，都是偏清爽的气味，口碑和市场接受度都蛮高的。个人觉得还蛮适合春夏的，基本男女都可，也都是之前都陆续分享过的",
        "tag": "家居",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%8E%A8%E8%8D%90/%E5%9B%BE%E7%89%87/6/4aee29f3fedda7ba36e9ab9115e96af.png",
        "praisenum": 456,
        "collectionnum": 564,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-28T11:25:39.000+00:00",
        "updated": "2023-04-25T11:25:42.000+00:00",
        "id": 5,
        "username": "安仔",
        "password": "123456",
        "phone": "345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/9.jpg",
        "gender": 1,
        "age": 23,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 27,
        "userId": 20,
        "username": "Matt带你游世界",
        "title": "我飘了，竟然想去富士山下的罗森",
        "content": "罗森便利店（富士河口湖町店)",
        "tag": "旅行",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%97%85%E8%A1%8C/%E5%9B%BE%E7%89%87/4/02bcf9650ef09af88636de412cd358f.png",
        "praisenum": 3677,
        "collectionnum": 96,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:40:54.000+00:00",
        "updated": null,
        "id": 20,
        "username": "Matt带你游世界",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/36.jpg",
        "gender": 0,
        "age": 26,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 36,
        "userId": 29,
        "username": "雅雅饿了",
        "title": "奶奶传下来的配方，自制阿达子好吃绝了",
        "content": "手工阿达子真的太好吃啦，晶莹剔透、Q Q弹弹超级有嚼劲、Q弹爽口，糯叽叽比珍珠还好吃，夏天必备哦！！！",
        "tag": "美食",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%BE%8E%E9%A3%9F/%E5%9B%BE%E7%89%87/3/1f31c8eeb972627a42bad21445ad0ce.png",
        "praisenum": 345,
        "collectionnum": 846,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:41:05.000+00:00",
        "updated": null,
        "id": 29,
        "username": "雅雅饿了",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/45.jpg",
        "gender": 1,
        "age": 35,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-29T03:38:18.000+00:00",
        "id": 3,
        "userId": 2,
        "username": "足球张雨绮",
        "title": "贴地斩练习",
        "content": "新手足球练习正脚背，就要反复用30.40%的力量重复刻意的练习，慢慢你会拥有自己的射门风格",
        "tag": "家居",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%8E%A8%E8%8D%90/%E8%A7%86%E9%A2%91/3/%E5%B0%81%E9%9D%A2.png",
        "praisenum": 432,
        "collectionnum": 648,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:21:44.000+00:00",
        "updated": "2023-04-25T11:21:47.000+00:00",
        "id": 2,
        "username": "足球张雨绮",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/6.jpg",
        "gender": 0,
        "age": 23,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 7,
        "userId": 6,
        "username": "Jerry",
        "title": "看电影",
        "content": "希望我和樱木的伤快快好哈哈哈哈",
        "tag": "家居",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%8E%A8%E8%8D%90/%E5%9B%BE%E7%89%87/6/270ca884eb1950ec1a652ca3765ba4f.png",
        "praisenum": 874,
        "collectionnum": 456,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:40:11.000+00:00",
        "updated": "2023-04-25T11:40:14.000+00:00",
        "id": 6,
        "username": "Jerry",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/20.jpg",
        "gender": 1,
        "age": 12,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 42,
        "userId": 32,
        "username": "Dille",
        "title": "荷尔蒙爆棚的凯文哥",
        "content": "无耻之徒",
        "tag": "其它",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E5%85%B6%E5%AE%83/%E8%A7%86%E9%A2%91/2/%E5%B0%81%E9%9D%A2.png",
        "praisenum": 456,
        "collectionnum": 6,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:41:07.000+00:00",
        "updated": null,
        "id": 32,
        "username": "Dille",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/48.jpg",
        "gender": 1,
        "age": 38,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 35,
        "userId": 28,
        "username": "菠萝派",
        "title": "再发一遍！这个巨巨巨下饭！！",
        "content": "奶奶做的几十年的酱油手撕鸡腿好好吃，一星期做了好多吃呢",
        "tag": "美食",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%BE%8E%E9%A3%9F/%E5%9B%BE%E7%89%87/2/c66fb62cbcd24f8dd1a568f0dcdc61a.png",
        "praisenum": 4567,
        "collectionnum": 546,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:41:04.000+00:00",
        "updated": null,
        "id": 28,
        "username": "菠萝派",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/43.jpg",
        "gender": 1,
        "age": 34,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-29T03:45:09.000+00:00",
        "id": 16,
        "userId": 1,
        "username": "xm",
        "title": "变回21年卷毛偷米咯",
        "content": "期待一下罗鼠准备筹备巡演啦！",
        "tag": "穿搭",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%A9%BF%E6%90%AD/%E5%9B%BE%E7%89%87/3/fa48205a52d4656ae5ba2c0442ee281.png",
        "praisenum": 4562,
        "collectionnum": 9,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-24T12:22:55.000+00:00",
        "updated": "2023-05-04T07:17:47.000+00:00",
        "id": 1,
        "username": "xm",
        "password": "123456",
        "phone": "13850429386",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/4.jpg",
        "gender": 1,
        "age": 22,
        "introduction": "无",
        "userType": "admin"
      }
    }
  ],
  "所有笔记": [
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-29T03:49:38.000+00:00",
        "id": 1,
        "userId": 1,
        "username": "xm",
        "title": "趁天还没热再来叠穿下",
        "content": "不然就来不及了",
        "tag": "家居",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%8E%A8%E8%8D%90/%E8%A7%86%E9%A2%91/1/%E5%B0%81%E9%9D%A2.png",
        "praisenum": 34244,
        "collectionnum": 564,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-24T12:22:55.000+00:00",
        "updated": "2023-05-04T07:17:47.000+00:00",
        "id": 1,
        "username": "xm",
        "password": "123456",
        "phone": "13850429386",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/4.jpg",
        "gender": 1,
        "age": 22,
        "introduction": "无",
        "userType": "admin"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-29T03:45:09.000+00:00",
        "id": 2,
        "userId": 1,
        "username": "xm",
        "title": "巴黎世家特卖会",
        "content": "开心看看买了啥",
        "tag": "家居",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%8E%A8%E8%8D%90/%E8%A7%86%E9%A2%91/2/%E5%B0%81%E9%9D%A2.png",
        "praisenum": 1423,
        "collectionnum": 68,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-24T12:22:55.000+00:00",
        "updated": "2023-05-04T07:17:47.000+00:00",
        "id": 1,
        "username": "xm",
        "password": "123456",
        "phone": "13850429386",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/4.jpg",
        "gender": 1,
        "age": 22,
        "introduction": "无",
        "userType": "admin"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-29T03:38:18.000+00:00",
        "id": 3,
        "userId": 2,
        "username": "足球张雨绮",
        "title": "贴地斩练习",
        "content": "新手足球练习正脚背，就要反复用30.40%的力量重复刻意的练习，慢慢你会拥有自己的射门风格",
        "tag": "家居",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%8E%A8%E8%8D%90/%E8%A7%86%E9%A2%91/3/%E5%B0%81%E9%9D%A2.png",
        "praisenum": 432,
        "collectionnum": 648,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:21:44.000+00:00",
        "updated": "2023-04-25T11:21:47.000+00:00",
        "id": 2,
        "username": "足球张雨绮",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/6.jpg",
        "gender": 0,
        "age": 23,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-29T03:38:47.000+00:00",
        "id": 4,
        "userId": 3,
        "username": "21克",
        "title": "cozyfit",
        "content": "穿搭",
        "tag": "家居",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%8E%A8%E8%8D%90/%E5%9B%BE%E7%89%87/1/e4bbe164ac25a3cfb12d6ed53938383.png",
        "praisenum": 123,
        "collectionnum": 56,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-12T11:23:32.000+00:00",
        "updated": "2023-04-25T11:23:37.000+00:00",
        "id": 3,
        "username": "21克",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/7.jpg",
        "gender": 1,
        "age": 54,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 5,
        "userId": 4,
        "username": "8lackk",
        "title": "厦利福尼亚",
        "content": "厦门",
        "tag": "家居",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%8E%A8%E8%8D%90/%E5%9B%BE%E7%89%87/2/7d999823ca52488a5b2e316ea7abe14.png",
        "praisenum": 123,
        "collectionnum": 886,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:24:53.000+00:00",
        "updated": "2023-04-25T11:24:56.000+00:00",
        "id": 4,
        "username": "8lackk",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/8.jpg",
        "gender": 1,
        "age": 47,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 6,
        "userId": 5,
        "username": "安仔",
        "title": "一个男生挚爱的6瓶香水",
        "content": "分享春夏喜欢的6支香水，都是偏清爽的气味，口碑和市场接受度都蛮高的。个人觉得还蛮适合春夏的，基本男女都可，也都是之前都陆续分享过的",
        "tag": "家居",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%8E%A8%E8%8D%90/%E5%9B%BE%E7%89%87/6/4aee29f3fedda7ba36e9ab9115e96af.png",
        "praisenum": 456,
        "collectionnum": 564,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-28T11:25:39.000+00:00",
        "updated": "2023-04-25T11:25:42.000+00:00",
        "id": 5,
        "username": "安仔",
        "password": "123456",
        "phone": "345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/9.jpg",
        "gender": 1,
        "age": 23,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 7,
        "userId": 6,
        "username": "Jerry",
        "title": "看电影",
        "content": "希望我和樱木的伤快快好哈哈哈哈",
        "tag": "家居",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%8E%A8%E8%8D%90/%E5%9B%BE%E7%89%87/6/270ca884eb1950ec1a652ca3765ba4f.png",
        "praisenum": 874,
        "collectionnum": 456,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:40:11.000+00:00",
        "updated": "2023-04-25T11:40:14.000+00:00",
        "id": 6,
        "username": "Jerry",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/20.jpg",
        "gender": 1,
        "age": 12,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 8,
        "userId": 7,
        "username": "泡芙味的女孩子",
        "title": "独一无二属于自己的小螃蟹",
        "content": "肉蟹煲",
        "tag": "家居",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%8E%A8%E8%8D%90/%E5%9B%BE%E7%89%87/5/c4287c1f3ac5d8e6054cf48c7c824f5.png",
        "praisenum": 3456,
        "collectionnum": 864,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:40:16.000+00:00",
        "updated": "2023-04-25T11:40:18.000+00:00",
        "id": 7,
        "username": "泡芙味的女孩子",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/21.jpg",
        "gender": 0,
        "age": 13,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 9,
        "userId": 8,
        "username": "吴",
        "title": "Tequila Sunrise",
        "content": "夏天就是积攒美好回忆的",
        "tag": "家居",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%8E%A8%E8%8D%90/%E5%9B%BE%E7%89%87/6/270ca884eb1950ec1a652ca3765ba4f.png",
        "praisenum": 3333,
        "collectionnum": 568,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:40:21.000+00:00",
        "updated": "2023-04-25T11:40:23.000+00:00",
        "id": 8,
        "username": "吴",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/22.jpg",
        "gender": 1,
        "age": 14,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 10,
        "userId": 9,
        "username": "HushOfficial",
        "title": "Rick Owens DRKSHDW VANS",
        "content": "这双实物还是值得推荐",
        "tag": "家居",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%8E%A8%E8%8D%90/%E5%9B%BE%E7%89%87/7/35c05e49a21ccf4559df03efa3d2c83.png",
        "praisenum": 5674,
        "collectionnum": 56,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:40:26.000+00:00",
        "updated": null,
        "id": 9,
        "username": "HushOfficial",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/23.jpg",
        "gender": 1,
        "age": 15,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 11,
        "userId": 10,
        "username": "阿泽爱吃面",
        "title": "三步让你窄干衣服饭价值",
        "content": "这条视频不看真的能让你后悔一年",
        "tag": "穿搭",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%A9%BF%E6%90%AD/%E8%A7%86%E9%A2%91/1/1.jpg",
        "praisenum": 467,
        "collectionnum": 86,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:40:28.000+00:00",
        "updated": null,
        "id": 10,
        "username": "阿泽爱吃面",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/24.jpg",
        "gender": 1,
        "age": 16,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 12,
        "userId": 11,
        "username": "迷人布",
        "title": "最近要分享的T恤",
        "content": "衣服",
        "tag": "穿搭",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%A9%BF%E6%90%AD/%E8%A7%86%E9%A2%91/1/1.jpg",
        "praisenum": 467,
        "collectionnum": 789,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:40:31.000+00:00",
        "updated": null,
        "id": 11,
        "username": "迷人布",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/25.jpg",
        "gender": 1,
        "age": 17,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 13,
        "userId": 12,
        "username": "麻豆同学",
        "title": "双矮子乐时髦又百搭的厚底鞋 无痛增高",
        "content": "你们期待已久的增高鞋分享来咯\r\n都是比较时髦又有点复古味道的厚底鞋\r\n在我这里出镜率也是超高的！\r\n这几款不论是配色上还是舒适度都没话说\r\n主要真的显高又显瘦",
        "tag": "穿搭",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%A9%BF%E6%90%AD/%E8%A7%86%E9%A2%91/2/2.png",
        "praisenum": 3547,
        "collectionnum": 897,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:40:33.000+00:00",
        "updated": null,
        "id": 12,
        "username": "麻豆同学",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/27.jpg",
        "gender": 0,
        "age": 18,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-29T03:45:09.000+00:00",
        "id": 14,
        "userId": 1,
        "username": "xm",
        "title": "让我看看到底有啥不一样",
        "content": "ererer",
        "tag": "穿搭",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%A9%BF%E6%90%AD/%E5%9B%BE%E7%89%87/1/4.png",
        "praisenum": 963,
        "collectionnum": 89,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-24T12:22:55.000+00:00",
        "updated": "2023-05-04T07:17:47.000+00:00",
        "id": 1,
        "username": "xm",
        "password": "123456",
        "phone": "13850429386",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/4.jpg",
        "gender": 1,
        "age": 22,
        "introduction": "无",
        "userType": "admin"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-29T03:45:09.000+00:00",
        "id": 15,
        "userId": 1,
        "username": "xm",
        "title": "小高最近 ",
        "content": "看到自己在商场里啦！开心嘿嘿",
        "tag": "穿搭",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%A9%BF%E6%90%AD/%E5%9B%BE%E7%89%87/2/5.png",
        "praisenum": 6433,
        "collectionnum": 7898,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-24T12:22:55.000+00:00",
        "updated": "2023-05-04T07:17:47.000+00:00",
        "id": 1,
        "username": "xm",
        "password": "123456",
        "phone": "13850429386",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/4.jpg",
        "gender": 1,
        "age": 22,
        "introduction": "无",
        "userType": "admin"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-29T03:45:09.000+00:00",
        "id": 16,
        "userId": 1,
        "username": "xm",
        "title": "变回21年卷毛偷米咯",
        "content": "期待一下罗鼠准备筹备巡演啦！",
        "tag": "穿搭",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%A9%BF%E6%90%AD/%E5%9B%BE%E7%89%87/3/fa48205a52d4656ae5ba2c0442ee281.png",
        "praisenum": 4562,
        "collectionnum": 9,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-24T12:22:55.000+00:00",
        "updated": "2023-05-04T07:17:47.000+00:00",
        "id": 1,
        "username": "xm",
        "password": "123456",
        "phone": "13850429386",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/4.jpg",
        "gender": 1,
        "age": 22,
        "introduction": "无",
        "userType": "admin"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 17,
        "userId": 13,
        "username": "Round15",
        "title": "跟我去村口耍帅吧",
        "content": "太帅了",
        "tag": "穿搭",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%A9%BF%E6%90%AD/%E5%9B%BE%E7%89%87/4/7abd389d552401d7296f85ff21db3bc.png",
        "praisenum": 345,
        "collectionnum": 654,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:40:36.000+00:00",
        "updated": null,
        "id": 13,
        "username": "Round15",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/28.jpg",
        "gender": 1,
        "age": 19,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 18,
        "userId": 14,
        "username": "JezZzZ",
        "title": "重庆什么天气啊一会儿冷一会儿热",
        "content": "六天课 杀了我",
        "tag": "穿搭",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%A9%BF%E6%90%AD/%E5%9B%BE%E7%89%87/5/0733f8d4665325bc729dcae05a3de51.png",
        "praisenum": 667,
        "collectionnum": 546,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:40:38.000+00:00",
        "updated": null,
        "id": 14,
        "username": "JezZzZ",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/29.jpg",
        "gender": 1,
        "age": 20,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 19,
        "userId": 15,
        "username": "蒋鹏",
        "title": "我这身没戴饼确实缺了点精华",
        "content": "来711当店员啰",
        "tag": "穿搭",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%A9%BF%E6%90%AD/%E5%9B%BE%E7%89%87/6/6.png",
        "praisenum": 457,
        "collectionnum": 8,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:40:40.000+00:00",
        "updated": null,
        "id": 15,
        "username": "蒋鹏",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/30.jpg",
        "gender": 0,
        "age": 21,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 20,
        "userId": 16,
        "username": "Kalevon",
        "title": "跟咖啡一个色",
        "content": "这一身还蛮搭这个庭院和咖啡",
        "tag": "穿搭",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%A9%BF%E6%90%AD/%E5%9B%BE%E7%89%87/7/7.png",
        "praisenum": 479,
        "collectionnum": 9978,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:40:43.000+00:00",
        "updated": null,
        "id": 16,
        "username": "Kalevon",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/31.jpg",
        "gender": 1,
        "age": 22,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 21,
        "userId": 17,
        "username": "日空山",
        "title": "风景",
        "content": "当然蓝玫瑰坠入克莱因蓝的海，未曾谋面也终会相遇",
        "tag": "旅行",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%97%85%E8%A1%8C/%E8%A7%86%E9%A2%91/1/8.png",
        "praisenum": 236,
        "collectionnum": 435,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:40:48.000+00:00",
        "updated": null,
        "id": 17,
        "username": "日空山",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/32.jpg",
        "gender": 1,
        "age": 23,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 22,
        "userId": 18,
        "username": "苏沫",
        "title": "这个夏天总要去一趟屏山吧",
        "content": "国风",
        "tag": "旅行",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%97%85%E8%A1%8C/%E8%A7%86%E9%A2%91/2/9.png",
        "praisenum": 8999,
        "collectionnum": 45,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:40:49.000+00:00",
        "updated": null,
        "id": 18,
        "username": "苏沫",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/34.jpg",
        "gender": 1,
        "age": 24,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 23,
        "userId": 19,
        "username": "小五",
        "title": "厦门的日落看一万次还是会心动",
        "content": "厦门",
        "tag": "旅行",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%97%85%E8%A1%8C/%E8%A7%86%E9%A2%91/3/10.png",
        "praisenum": 3456,
        "collectionnum": 453,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:40:53.000+00:00",
        "updated": null,
        "id": 19,
        "username": "小五",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/35.jpg",
        "gender": 1,
        "age": 25,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-29T03:45:09.000+00:00",
        "id": 24,
        "userId": 1,
        "username": "xm",
        "title": "真实经历，这些坑希望你在平潭千万不要踩",
        "content": "血泪教训，想近期平潭环岛游的uu们请收下这份环岛拍照/路线攻略和避坑指南！",
        "tag": "旅行",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%97%85%E8%A1%8C/%E5%9B%BE%E7%89%87/1/28eb92a6ea0dcfa9819da74027fb81f.png",
        "praisenum": 433,
        "collectionnum": 456,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-24T12:22:55.000+00:00",
        "updated": "2023-05-04T07:17:47.000+00:00",
        "id": 1,
        "username": "xm",
        "password": "123456",
        "phone": "13850429386",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/4.jpg",
        "gender": 1,
        "age": 22,
        "introduction": "无",
        "userType": "admin"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-29T07:54:06.000+00:00",
        "id": 25,
        "userId": 1,
        "username": "xm",
        "title": "上海City walk 陆家嘴",
        "content": "陆家嘴网红三件套云朵书店震旦博物馆浦东美术馆东方明珠\r\n全程步行：3km，需要花费一天时间 7-8H\r\n路线包括：拍照+博物馆+艺术展+东方明珠\r\n沿途风景：很多地标性建筑，只要来上海必走路线，相比外滩人山人海，陆家嘴不拥挤的美景更值得",
        "tag": "旅行",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%97%85%E8%A1%8C/%E5%9B%BE%E7%89%87/2/29e232bd30e6b22787a7351a0126e95.png",
        "praisenum": 7864,
        "collectionnum": 786,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-24T12:22:55.000+00:00",
        "updated": "2023-05-04T07:17:47.000+00:00",
        "id": 1,
        "username": "xm",
        "password": "123456",
        "phone": "13850429386",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/4.jpg",
        "gender": 1,
        "age": 22,
        "introduction": "无",
        "userType": "admin"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-29T03:45:09.000+00:00",
        "id": 26,
        "userId": 1,
        "username": "xm",
        "title": "大二学生穷游威海",
        "content": "总要去一次威海吧",
        "tag": "旅行",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%97%85%E8%A1%8C/%E5%9B%BE%E7%89%87/3/f7228ecc01bb58ea03b9098e3732050.png",
        "praisenum": 346,
        "collectionnum": 456,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-24T12:22:55.000+00:00",
        "updated": "2023-05-04T07:17:47.000+00:00",
        "id": 1,
        "username": "xm",
        "password": "123456",
        "phone": "13850429386",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/4.jpg",
        "gender": 1,
        "age": 22,
        "introduction": "无",
        "userType": "admin"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 27,
        "userId": 20,
        "username": "Matt带你游世界",
        "title": "我飘了，竟然想去富士山下的罗森",
        "content": "罗森便利店（富士河口湖町店)",
        "tag": "旅行",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%97%85%E8%A1%8C/%E5%9B%BE%E7%89%87/4/02bcf9650ef09af88636de412cd358f.png",
        "praisenum": 3677,
        "collectionnum": 96,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:40:54.000+00:00",
        "updated": null,
        "id": 20,
        "username": "Matt带你游世界",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/36.jpg",
        "gender": 0,
        "age": 26,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 28,
        "userId": 21,
        "username": "胖胖的熊大",
        "title": "长沙旅游回来了！最需要注意的就是…",
        "content": "长沙好多人！！不想排队的话！最需要注意的是要提前做好攻略！该预约的及时预约！！该提前准备的都要准备！！\r\n1做了长沙景点介绍和预约开放时间",
        "tag": "旅行",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%97%85%E8%A1%8C/%E5%9B%BE%E7%89%87/5/096bdd918bc1a315e11af1dd50aec3e.png",
        "praisenum": 5455,
        "collectionnum": 54,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:40:55.000+00:00",
        "updated": null,
        "id": 21,
        "username": "胖胖的熊大",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/37.jpg",
        "gender": 0,
        "age": 27,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 29,
        "userId": 22,
        "username": "Pentaki",
        "title": "坐落在澳洲深处的宇宙之镜",
        "content": "夜幕降临，星空如诗如画地铺陈在头顶。天空之镜犹如一个宇宙之镜，将璀璨星辰、浩渺银河倒映其中，这一刻，仿佛成为了天地间独一无二的旅者。仰望星空，感受到宇宙的浩瀚无垠；俯瞰盐湖，能触摸到星辰的温度。",
        "tag": "旅行",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%97%85%E8%A1%8C/%E5%9B%BE%E7%89%87/6/12cba05802734b7dbdd3d59d1c1dd93.png",
        "praisenum": 4572,
        "collectionnum": 56,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:40:56.000+00:00",
        "updated": null,
        "id": 22,
        "username": "Pentaki",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/38.jpg",
        "gender": 1,
        "age": 28,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 30,
        "userId": 23,
        "username": "西行西藏Qon",
        "title": "川西的美是靠滤镜吗？",
        "content": "美是需要去发现的\r\n去过那么多次，每次都能发现不一样的美\r\n一年四季各有千秋\r\n雪山巍峨壮观\r\n草甸青翠欲滴\r\n湖泊清爽秀丽\r\n滤镜会让美景更好看，但是不可否认川西本身就很美\r\n所以，川西一直是值得所有人去一次的\r\n相信我你会爱上这个秘境",
        "tag": "旅行",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%97%85%E8%A1%8C/%E5%9B%BE%E7%89%87/7/b28f840cd8ffbe6792d498d7b6b7b7e.png",
        "praisenum": 633,
        "collectionnum": 5456,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:40:59.000+00:00",
        "updated": null,
        "id": 23,
        "username": "西行西藏Qon",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/39.jpg",
        "gender": 1,
        "age": 29,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 31,
        "userId": 24,
        "username": "驰名",
        "title": "第一次来长沙玩的姐妹进来",
        "content": "长沙好吃的真的太多啦！一条视频根本讲不完",
        "tag": "美食",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%BE%8E%E9%A3%9F/%E8%A7%86%E9%A2%91/1/%E5%B0%81%E9%9D%A2.png",
        "praisenum": 458,
        "collectionnum": 56,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:41:00.000+00:00",
        "updated": null,
        "id": 24,
        "username": "驰名",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/4.jpg",
        "gender": 1,
        "age": 30,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 32,
        "userId": 25,
        "username": "热爱生活的黄同学",
        "title": "春天不让女朋友出去浪的方法就是给她吃",
        "content": "给嘴馋的女朋友做了口水鸡，麻辣鲜香，肉嫩味美，还有外酥里嫩的椒盐虾仁，配上一锅荷包蛋焖面美滋滋    ",
        "tag": "美食",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%BE%8E%E9%A3%9F/%E8%A7%86%E9%A2%91/2/%E5%B0%81%E9%9D%A2.png",
        "praisenum": 4578,
        "collectionnum": 86,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:41:01.000+00:00",
        "updated": null,
        "id": 25,
        "username": "热爱生活的黄同学",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/40.jpg",
        "gender": 1,
        "age": 31,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 33,
        "userId": 26,
        "username": "Vanessa",
        "title": "breakfast蒜香芝士厚吐司",
        "content": "早餐不知道吃什么的姐们快试试这款蒜香吐司 口感真的绝了！外脆里嫩搭配芝士好吃到停不下来",
        "tag": "美食",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%BE%8E%E9%A3%9F/%E8%A7%86%E9%A2%91/3/%E5%B0%81%E9%9D%A2.png",
        "praisenum": 356,
        "collectionnum": 546,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:41:02.000+00:00",
        "updated": null,
        "id": 26,
        "username": "Vanessa",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/41.jpg",
        "gender": 1,
        "age": 32,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 34,
        "userId": 27,
        "username": "椰汁波波",
        "title": "我爸尝了一口…让我原地开店",
        "content": "这个酸辣凉面真的泰适合夏天啦",
        "tag": "美食",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%BE%8E%E9%A3%9F/%E5%9B%BE%E7%89%87/1/7f67277bf4753e3bce4491a6d0ac22d.png",
        "praisenum": 6565,
        "collectionnum": 846,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:41:03.000+00:00",
        "updated": null,
        "id": 27,
        "username": "椰汁波波",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/42.jpg",
        "gender": 0,
        "age": 33,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 35,
        "userId": 28,
        "username": "菠萝派",
        "title": "再发一遍！这个巨巨巨下饭！！",
        "content": "奶奶做的几十年的酱油手撕鸡腿好好吃，一星期做了好多吃呢",
        "tag": "美食",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%BE%8E%E9%A3%9F/%E5%9B%BE%E7%89%87/2/c66fb62cbcd24f8dd1a568f0dcdc61a.png",
        "praisenum": 4567,
        "collectionnum": 546,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:41:04.000+00:00",
        "updated": null,
        "id": 28,
        "username": "菠萝派",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/43.jpg",
        "gender": 1,
        "age": 34,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 36,
        "userId": 29,
        "username": "雅雅饿了",
        "title": "奶奶传下来的配方，自制阿达子好吃绝了",
        "content": "手工阿达子真的太好吃啦，晶莹剔透、Q Q弹弹超级有嚼劲、Q弹爽口，糯叽叽比珍珠还好吃，夏天必备哦！！！",
        "tag": "美食",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%BE%8E%E9%A3%9F/%E5%9B%BE%E7%89%87/3/1f31c8eeb972627a42bad21445ad0ce.png",
        "praisenum": 345,
        "collectionnum": 846,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:41:05.000+00:00",
        "updated": null,
        "id": 29,
        "username": "雅雅饿了",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/45.jpg",
        "gender": 1,
        "age": 35,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 37,
        "userId": 30,
        "username": "神奇妈妈的料理",
        "title": "猫里狗气的虾排堡太可爱了吧！",
        "content": "第一眼看上去还以为是粘土捏的……",
        "tag": "美食",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%BE%8E%E9%A3%9F/%E5%9B%BE%E7%89%87/4/3f41c567052c9a529ec3d05e7e0202b.png",
        "praisenum": 768,
        "collectionnum": 56,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:41:06.000+00:00",
        "updated": null,
        "id": 30,
        "username": "神奇妈妈的料理",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/46.jpg",
        "gender": 0,
        "age": 36,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-29T03:45:09.000+00:00",
        "id": 38,
        "userId": 1,
        "username": "xm",
        "title": "分享近期在厦门吃到的...（非常好次的合集）",
        "content": "厦门美食，我的美食日记",
        "tag": "美食",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%BE%8E%E9%A3%9F/%E5%9B%BE%E7%89%87/5/5f3870abfd29bc015a91db365085d9b.png",
        "praisenum": 45,
        "collectionnum": 96,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-24T12:22:55.000+00:00",
        "updated": "2023-05-04T07:17:47.000+00:00",
        "id": 1,
        "username": "xm",
        "password": "123456",
        "phone": "13850429386",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/4.jpg",
        "gender": 1,
        "age": 22,
        "introduction": "无",
        "userType": "admin"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-29T03:45:09.000+00:00",
        "id": 39,
        "userId": 1,
        "username": "xm",
        "title": "1r多早餐店倒闭有它一半责任！",
        "content": "往外直透油的肉包子！谁懂啊啊啊！！",
        "tag": "美食",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%BE%8E%E9%A3%9F/%E5%9B%BE%E7%89%87/6/7246eb9b57ee9a4e7c2d91bd37901df.png",
        "praisenum": 665,
        "collectionnum": 864,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-24T12:22:55.000+00:00",
        "updated": "2023-05-04T07:17:47.000+00:00",
        "id": 1,
        "username": "xm",
        "password": "123456",
        "phone": "13850429386",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/4.jpg",
        "gender": 1,
        "age": 22,
        "introduction": "无",
        "userType": "admin"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-29T03:45:09.000+00:00",
        "id": 40,
        "userId": 1,
        "username": "xm",
        "title": "今天喝19.9，的椰奶星冰乐",
        "content": "星巴克奶油星冰乐换巴旦木奶，椰浆，可可碎片",
        "tag": "美食",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%BE%8E%E9%A3%9F/%E5%9B%BE%E7%89%87/7/ab53ff3630fb1cec529500bf4f518c2.png",
        "praisenum": 654,
        "collectionnum": 846,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-24T12:22:55.000+00:00",
        "updated": "2023-05-04T07:17:47.000+00:00",
        "id": 1,
        "username": "xm",
        "password": "123456",
        "phone": "13850429386",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/4.jpg",
        "gender": 1,
        "age": 22,
        "introduction": "无",
        "userType": "admin"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 41,
        "userId": 31,
        "username": "票",
        "title": "拍烂片？败名声？到底图什么？",
        "content": "3楼跳下来 背摔没有任何措施，别催牛逼 我不信。什么概念 ",
        "tag": "其它",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E5%85%B6%E5%AE%83/%E8%A7%86%E9%A2%91/1/%E5%B0%81%E9%9D%A2.png",
        "praisenum": 6543,
        "collectionnum": 6,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:41:06.000+00:00",
        "updated": null,
        "id": 31,
        "username": "票",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/47.jpg",
        "gender": 1,
        "age": 37,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 42,
        "userId": 32,
        "username": "Dille",
        "title": "荷尔蒙爆棚的凯文哥",
        "content": "无耻之徒",
        "tag": "其它",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E5%85%B6%E5%AE%83/%E8%A7%86%E9%A2%91/2/%E5%B0%81%E9%9D%A2.png",
        "praisenum": 456,
        "collectionnum": 6,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:41:07.000+00:00",
        "updated": null,
        "id": 32,
        "username": "Dille",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/48.jpg",
        "gender": 1,
        "age": 38,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 43,
        "userId": 33,
        "username": "云宝儿",
        "title": "虚假的穷人VS真实的穷人",
        "content": "张颂文",
        "tag": "其它",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E5%85%B6%E5%AE%83/%E8%A7%86%E9%A2%91/3/%E5%B0%81%E9%9D%A2.png",
        "praisenum": 866,
        "collectionnum": 89,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:41:07.000+00:00",
        "updated": null,
        "id": 33,
        "username": "云宝儿",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/49.jpg",
        "gender": 0,
        "age": 39,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 44,
        "userId": 34,
        "username": "阿棒的觅食计划",
        "title": "愿每个去长沙的人都能刷到",
        "content": "马上五一假期了，好多朋友来长沙旅游！作为在长沙学习生活7年的土著，给大家整理了「2天1夜的自由行线路攻略」，有需要的宝子可以参考我的行程哦！一点不会踩雷！",
        "tag": "其它",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E5%85%B6%E5%AE%83/%E5%9B%BE%E7%89%87/1/0e4e98e85cac442efe792e7a7330a88.png",
        "praisenum": 673,
        "collectionnum": 486,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:41:09.000+00:00",
        "updated": null,
        "id": 34,
        "username": "阿棒的觅食计划",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/50.jpg",
        "gender": 1,
        "age": 40,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 45,
        "userId": 35,
        "username": "NASA-探索",
        "title": "从太空视角看喜马拉雅山",
        "content": "人类的纷争并不重要，看看远处的雪山吧",
        "tag": "其它",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E5%85%B6%E5%AE%83/%E5%9B%BE%E7%89%87/2/b08bb40bc93b6e214236057c66be87d.png",
        "praisenum": 6757,
        "collectionnum": 486,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:41:10.000+00:00",
        "updated": null,
        "id": 35,
        "username": "NASA-探索",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/10.jpg",
        "gender": 1,
        "age": 41,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 46,
        "userId": 36,
        "username": "Maxxx",
        "title": "釜山行",
        "content": "咱们去釜山尊的是去拍釜山行3的 落地大暴雨\r\n天气巨差 釜山的食物店把犬妹气哭",
        "tag": "其它",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E5%85%B6%E5%AE%83/%E5%9B%BE%E7%89%87/3/12a4b2452df24057d083211955eafd0.png",
        "praisenum": 457,
        "collectionnum": 546,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:41:11.000+00:00",
        "updated": null,
        "id": 36,
        "username": "Maxxx",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/11.jpg",
        "gender": 0,
        "age": 42,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-25T12:14:30.000+00:00",
        "id": 47,
        "userId": 37,
        "username": "王内个科",
        "title": "无眉大侠踹你三脚",
        "content": "眉毛漂太浅了！\r\n前面的照片用了朋友给的深棕色染眉膏\r\n最后一张是洗下来的样子……\r\n不过还行\r\n倒是挺特别的……",
        "tag": "其它",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E5%85%B6%E5%AE%83/%E5%9B%BE%E7%89%87/4/0fcf2471e8370d638562ac66a12f82f.png",
        "praisenum": 457,
        "collectionnum": 68,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:41:12.000+00:00",
        "updated": null,
        "id": 37,
        "username": "王内个科",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/12.jpg",
        "gender": 1,
        "age": 43,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-29T03:45:09.000+00:00",
        "id": 48,
        "userId": 1,
        "username": "xm",
        "title": "只会画眉毛",
        "content": "画眉毛",
        "tag": "其它",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E5%85%B6%E5%AE%83/%E5%9B%BE%E7%89%87/5/625c3269603a46a3fc88a7e5ebccded.png",
        "praisenum": 846,
        "collectionnum": 5468,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-24T12:22:55.000+00:00",
        "updated": "2023-05-04T07:17:47.000+00:00",
        "id": 1,
        "username": "xm",
        "password": "123456",
        "phone": "13850429386",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/4.jpg",
        "gender": 1,
        "age": 22,
        "introduction": "无",
        "userType": "admin"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-29T03:45:09.000+00:00",
        "id": 49,
        "userId": 1,
        "username": "xm",
        "title": "当大学生三年赚了三千万",
        "content": "千万要开心 千万要幸福 千万要健康",
        "tag": "其它",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E5%85%B6%E5%AE%83/%E5%9B%BE%E7%89%87/6/0926d84349f2696613745b2491f66ec.png",
        "praisenum": 535,
        "collectionnum": 4865,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-24T12:22:55.000+00:00",
        "updated": "2023-05-04T07:17:47.000+00:00",
        "id": 1,
        "username": "xm",
        "password": "123456",
        "phone": "13850429386",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/4.jpg",
        "gender": 1,
        "age": 22,
        "introduction": "无",
        "userType": "admin"
      }
    },
    {
      "note": {
        "created": "2023-04-25T12:14:30.000+00:00",
        "updated": "2023-04-29T07:53:52.000+00:00",
        "id": 50,
        "userId": 1,
        "username": "xm",
        "title": "水肿是我一生的痛 除非让我化妆后去出道…..",
        "content": ":谁能懂睡到下午一点后整张脸变成发面馒头的痛",
        "tag": "其它",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E5%85%B6%E5%AE%83/%E5%9B%BE%E7%89%87/7/0c4802cd41042f2d6d443a6b276e8b1.png",
        "praisenum": 345,
        "collectionnum": 486,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-24T12:22:55.000+00:00",
        "updated": "2023-05-04T07:17:47.000+00:00",
        "id": 1,
        "username": "xm",
        "password": "123456",
        "phone": "13850429386",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/4.jpg",
        "gender": 1,
        "age": 22,
        "introduction": "无",
        "userType": "admin"
      }
    },
    {
      "note": {
        "created": "2023-05-22T06:39:43.000+00:00",
        "updated": null,
        "id": 51,
        "userId": 27,
        "username": "Vanessa",
        "title": "今天喝19.9，的椰奶星冰乐",
        "content": "星巴克奶油星冰乐换巴旦木奶，椰浆，可可碎片",
        "tag": "美食",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%BE%8E%E9%A3%9F/%E5%9B%BE%E7%89%87/7/ab53ff3630fb1cec529500bf4f518c2.png",
        "praisenum": 45,
        "collectionnum": 45,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:41:03.000+00:00",
        "updated": null,
        "id": 27,
        "username": "椰汁波波",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/42.jpg",
        "gender": 0,
        "age": 33,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-05-22T06:39:46.000+00:00",
        "updated": null,
        "id": 52,
        "userId": 28,
        "username": "菠萝派",
        "title": "1r多早餐店倒闭有它一半责任！",
        "content": "往外直透油的肉包子！谁懂啊啊啊！",
        "tag": "美食",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%BE%8E%E9%A3%9F/%E5%9B%BE%E7%89%87/6/7246eb9b57ee9a4e7c2d91bd37901df.png",
        "praisenum": 456,
        "collectionnum": 756,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:41:04.000+00:00",
        "updated": null,
        "id": 28,
        "username": "菠萝派",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/43.jpg",
        "gender": 1,
        "age": 34,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-05-22T09:36:10.000+00:00",
        "updated": null,
        "id": 53,
        "userId": 1,
        "username": "xm",
        "title": "阳光下草地上的书本",
        "content": "阳光下，草地上，打开书本，感悟人生。\r\n夏日炎炎，时不时的觉着自己没有了力气，\r\n需要找个清凉的地方，好好静一静，",
        "tag": "书籍",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E4%B9%A6%E7%B1%8D/%E8%A7%86%E9%A2%91/1/%E5%B0%81%E9%9D%A2.png",
        "praisenum": 45,
        "collectionnum": 24,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-24T12:22:55.000+00:00",
        "updated": "2023-05-04T07:17:47.000+00:00",
        "id": 1,
        "username": "xm",
        "password": "123456",
        "phone": "13850429386",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/4.jpg",
        "gender": 1,
        "age": 22,
        "introduction": "无",
        "userType": "admin"
      }
    },
    {
      "note": {
        "created": "2023-05-22T09:36:15.000+00:00",
        "updated": null,
        "id": 54,
        "userId": 1,
        "username": "xm",
        "title": "荐书|《自卑与超越》 阿德勒 心理学经典",
        "content": "好书推荐，暴躁解读，长期主义，一起学习。\r\n看完视频就去看书，学会自律，缓解焦虑。",
        "tag": "书籍",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E4%B9%A6%E7%B1%8D/%E8%A7%86%E9%A2%91/2/%E5%B0%81%E9%9D%A2.png",
        "praisenum": 678,
        "collectionnum": 463,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-24T12:22:55.000+00:00",
        "updated": "2023-05-04T07:17:47.000+00:00",
        "id": 1,
        "username": "xm",
        "password": "123456",
        "phone": "13850429386",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/4.jpg",
        "gender": 1,
        "age": 22,
        "introduction": "无",
        "userType": "admin"
      }
    },
    {
      "note": {
        "created": "2023-05-22T09:36:16.000+00:00",
        "updated": null,
        "id": 55,
        "userId": 1,
        "username": "xm",
        "title": "一个翻书视频",
        "content": "《我们看什么，我们就成为什么》",
        "tag": "书籍",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E4%B9%A6%E7%B1%8D/%E8%A7%86%E9%A2%91/3/%E5%B0%81%E9%9D%A2.png",
        "praisenum": 3525,
        "collectionnum": 567,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-24T12:22:55.000+00:00",
        "updated": "2023-05-04T07:17:47.000+00:00",
        "id": 1,
        "username": "xm",
        "password": "123456",
        "phone": "13850429386",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/4.jpg",
        "gender": 1,
        "age": 22,
        "introduction": "无",
        "userType": "admin"
      }
    },
    {
      "note": {
        "created": "2023-05-22T09:36:18.000+00:00",
        "updated": null,
        "id": 56,
        "userId": 3,
        "username": "21克",
        "title": "书籍设计",
        "content": "之前书籍项目的视频版本",
        "tag": "书籍",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E4%B9%A6%E7%B1%8D/%E8%A7%86%E9%A2%91/4/%E5%B0%81%E9%9D%A2.png",
        "praisenum": 678,
        "collectionnum": 23,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-12T11:23:32.000+00:00",
        "updated": "2023-04-25T11:23:37.000+00:00",
        "id": 3,
        "username": "21克",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/7.jpg",
        "gender": 1,
        "age": 54,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-05-22T09:36:20.000+00:00",
        "updated": null,
        "id": 57,
        "userId": 5,
        "username": "安仔",
        "title": "云边有个小卖部",
        "content": "微视频 超治愈的好书 任何人没看过我都会伤心",
        "tag": "书籍",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E4%B9%A6%E7%B1%8D/%E8%A7%86%E9%A2%91/5/%E5%B0%81%E9%9D%A2.png",
        "praisenum": 123,
        "collectionnum": 5747,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-28T11:25:39.000+00:00",
        "updated": "2023-04-25T11:25:42.000+00:00",
        "id": 5,
        "username": "安仔",
        "password": "123456",
        "phone": "345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/9.jpg",
        "gender": 1,
        "age": 23,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-05-22T09:36:22.000+00:00",
        "updated": null,
        "id": 58,
        "userId": 6,
        "username": "Jerry",
        "title": "自出版摄影书",
        "content": "录制了一个翻书视频，这本50页的摄影书",
        "tag": "书籍",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E4%B9%A6%E7%B1%8D/%E8%A7%86%E9%A2%91/6/%E5%B0%81%E9%9D%A2.png",
        "praisenum": 234,
        "collectionnum": 346,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:40:11.000+00:00",
        "updated": "2023-04-25T11:40:14.000+00:00",
        "id": 6,
        "username": "Jerry",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/20.jpg",
        "gender": 1,
        "age": 12,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-05-22T09:36:23.000+00:00",
        "updated": null,
        "id": 59,
        "userId": 10,
        "username": "迷人布",
        "title": "好书",
        "content": "《活着》讲述了农村人福贵悲惨的人生遭遇。福贵本是个阔少爷，可他嗜赌如命，终于赌光了家业，一贫如洗。",
        "tag": "书籍",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E4%B9%A6%E7%B1%8D/%E8%A7%86%E9%A2%91/7/%E5%B0%81%E9%9D%A2.png",
        "praisenum": 35,
        "collectionnum": 45,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:40:28.000+00:00",
        "updated": null,
        "id": 10,
        "username": "阿泽爱吃面",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/24.jpg",
        "gender": 1,
        "age": 16,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-05-22T09:36:25.000+00:00",
        "updated": null,
        "id": 60,
        "userId": 18,
        "username": "苏沫",
        "title": "富士VLOG",
        "content": "富士直出日常小视频，这次是亲子阅读主题，也适合图书馆，书店，读书的视频拍摄！可以互相参考找找分镜灵感！",
        "tag": "书籍",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E4%B9%A6%E7%B1%8D/%E8%A7%86%E9%A2%91/8/%E5%B0%81%E9%9D%A2.png",
        "praisenum": 356,
        "collectionnum": 343,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:40:49.000+00:00",
        "updated": null,
        "id": 18,
        "username": "苏沫",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/34.jpg",
        "gender": 1,
        "age": 24,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-05-22T09:36:26.000+00:00",
        "updated": null,
        "id": 61,
        "userId": 25,
        "username": "热爱生活的黄同学",
        "title": "翻书视频啦！我的第一本手工影集",
        "content": "翻书视频来啦！！\r\n我的第一本手工影集\r\nThe wind in the trees",
        "tag": "书籍",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E4%B9%A6%E7%B1%8D/%E8%A7%86%E9%A2%91/9/%E5%B0%81%E9%9D%A2.png",
        "praisenum": 237,
        "collectionnum": 346,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:41:01.000+00:00",
        "updated": null,
        "id": 25,
        "username": "热爱生活的黄同学",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/40.jpg",
        "gender": 1,
        "age": 31,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-05-22T09:36:29.000+00:00",
        "updated": null,
        "id": 62,
        "userId": 27,
        "username": "椰汁波波",
        "title": "NO.122 《Fahrenheit 451》-热敏书籍实验",
        "content": "《Heat》《Fahrenheit 451》两本书籍的热敏书籍实验视频",
        "tag": "书籍",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E4%B9%A6%E7%B1%8D/%E8%A7%86%E9%A2%91/10/%E5%B0%81%E9%9D%A2.png",
        "praisenum": 343,
        "collectionnum": 375,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:41:03.000+00:00",
        "updated": null,
        "id": 27,
        "username": "椰汁波波",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/42.jpg",
        "gender": 0,
        "age": 33,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-05-22T09:36:32.000+00:00",
        "updated": null,
        "id": 63,
        "userId": 28,
        "username": "菠萝派",
        "title": "《非神剩的爱》李翰原｜摄影书翻阅",
        "content": "这学期的手工书大作业终于做完啦，来看看翻书视频吧",
        "tag": "书籍",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E4%B9%A6%E7%B1%8D/%E8%A7%86%E9%A2%91/11/%E5%B0%81%E9%9D%A2.png",
        "praisenum": 36,
        "collectionnum": 3573,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:41:04.000+00:00",
        "updated": null,
        "id": 28,
        "username": "菠萝派",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/43.jpg",
        "gender": 1,
        "age": 34,
        "introduction": "无",
        "userType": "normal"
      }
    },
    {
      "note": {
        "created": "2023-05-22T09:36:34.000+00:00",
        "updated": null,
        "id": 64,
        "userId": 29,
        "username": "雅雅饿了",
        "title": "每日设计打卡",
        "content": "巜恶意》封面设计的制作过程视频",
        "tag": "书籍",
        "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E4%B9%A6%E7%B1%8D/%E8%A7%86%E9%A2%91/12/%E5%B0%81%E9%9D%A2.png",
        "praisenum": 577,
        "collectionnum": 346,
        "deleted": 0
      },
      "user": {
        "created": "2023-04-25T11:41:05.000+00:00",
        "updated": null,
        "id": 29,
        "username": "雅雅饿了",
        "password": "123456",
        "phone": "12345678910",
        "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/45.jpg",
        "gender": 1,
        "age": 35,
        "introduction": "无",
        "userType": "normal"
      }
    }
  ]
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» 推荐笔记|[object]|true|none||none|
|»» note|object|true|none||none|
|»»» created|string|true|none||none|
|»»» updated|string|true|none||none|
|»»» id|integer|true|none||none|
|»»» userId|integer|true|none||none|
|»»» username|string|true|none||none|
|»»» title|string|true|none||none|
|»»» content|string|true|none||none|
|»»» tag|string|true|none||none|
|»»» surfacePicture|string|true|none||none|
|»»» praisenum|integer|true|none||none|
|»»» collectionnum|integer|true|none||none|
|»»» deleted|integer|true|none||none|
|»» user|object|true|none||none|
|»»» created|string|true|none||none|
|»»» updated|string¦null|true|none||none|
|»»» id|integer|true|none||none|
|»»» username|string|true|none||none|
|»»» password|string|true|none||none|
|»»» phone|string|true|none||none|
|»»» headphoto|string|true|none||none|
|»»» gender|integer|true|none||none|
|»»» age|integer|true|none||none|
|»»» introduction|string|true|none||none|
|»»» userType|string|true|none||none|
|» 所有笔记|[object]|true|none||none|
|»» note|object|true|none||none|
|»»» created|string|true|none||none|
|»»» updated|string¦null|true|none||none|
|»»» id|integer|true|none||none|
|»»» userId|integer|true|none||none|
|»»» username|string|true|none||none|
|»»» title|string|true|none||none|
|»»» content|string|true|none||none|
|»»» tag|string|true|none||none|
|»»» surfacePicture|string|true|none||none|
|»»» praisenum|integer|true|none||none|
|»»» collectionnum|integer|true|none||none|
|»»» deleted|integer|true|none||none|
|»» user|object|true|none||none|
|»»» created|string|true|none||none|
|»»» updated|string¦null|true|none||none|
|»»» id|integer|true|none||none|
|»»» username|string|true|none||none|
|»»» password|string|true|none||none|
|»»» phone|string|true|none||none|
|»»» headphoto|string|true|none||none|
|»»» gender|integer|true|none||none|
|»»» age|integer|true|none||none|
|»»» introduction|string|true|none||none|
|»»» userType|string|true|none||none|

## GET 笔记内容

GET /found/content/{noteId}

提交笔记id和token，后端响应笔记内容的业务对象

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|noteId|path|integer| 是 ||none|
|Authorization|header|string| 是 ||token|

> 返回示例

> 成功

```json
{
  "created": null,
  "updated": null,
  "username": "xm",
  "content": "看到自己在商场里啦！开心嘿嘿",
  "comment": [
    {
      "created": "2023-04-25T12:19:49.000+00:00",
      "updated": null,
      "id": null,
      "userId": null,
      "noteId": null,
      "comment": "小高宝宝爬树中",
      "username": "驰名",
      "deleted": null,
      "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/4.jpg"
    },
    {
      "created": "2023-04-25T12:19:49.000+00:00",
      "updated": null,
      "id": null,
      "userId": null,
      "noteId": null,
      "comment": "小羔春游日记",
      "username": "热爱生活的黄同学",
      "deleted": null,
      "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/40.jpg"
    }
  ],
  "pictureurl": [
    "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%A9%BF%E6%90%AD/%E5%9B%BE%E7%89%87/2/5.png",
    "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%A9%BF%E6%90%AD/%E5%9B%BE%E7%89%87/2/5ec2fe46f780a137a1b88f7ed666124.png"
  ],
  "videourl": null,
  "tag": "穿搭",
  "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/4.jpg",
  "title": "小高最近 ",
  "collectionnum": 7898,
  "commentTime": null
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» created|null|true|none||none|
|» updated|null|true|none||none|
|» username|string|true|none||none|
|» content|string|true|none||none|
|» comment|[object]|true|none||none|
|»» created|string|true|none||none|
|»» updated|null|true|none||none|
|»» id|null|true|none||none|
|»» userId|null|true|none||none|
|»» noteId|null|true|none||none|
|»» comment|string|true|none||none|
|»» username|string|true|none||none|
|»» deleted|null|true|none||none|
|»» headphoto|string|true|none||none|
|» pictureurl|[string]|true|none||none|
|» videourl|null|true|none||none|
|» tag|string|true|none||none|
|» headphoto|string|true|none||none|
|» title|string|true|none||none|
|» collectionnum|integer|true|none||none|
|» commentTime|null|true|none||none|

## GET 搜索

GET /found/search

提交搜索内容和请求头token，后端根据标签，笔记介绍，和标题进行模糊查询

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|param|query|string| 是 ||根据标签、视频介绍、标题模糊查询|
|Authorization|header|string| 否 ||token|

> 返回示例

> 成功

```json
[
  {
    "note": {
      "created": "2023-04-25T12:14:30.000+00:00",
      "updated": "2023-04-29T03:49:38.000+00:00",
      "id": 1,
      "userId": 1,
      "username": "xm",
      "title": "趁天还没热再来叠穿下",
      "content": "不然就来不及了",
      "tag": "推荐",
      "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%8E%A8%E8%8D%90/%E8%A7%86%E9%A2%91/1/%E5%B0%81%E9%9D%A2.png",
      "praisenum": 34244,
      "deleted": 0
    },
    "user": {
      "created": "2023-04-24T12:22:55.000+00:00",
      "updated": "2023-05-04T07:17:47.000+00:00",
      "id": 1,
      "username": "xm",
      "password": "123456",
      "phone": "13850429386",
      "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/4.jpg",
      "gender": 1,
      "age": 22,
      "introduction": "无"
    }
  },
  {
    "note": {
      "created": "2023-04-25T12:14:30.000+00:00",
      "updated": "2023-04-25T12:14:30.000+00:00",
      "id": 9,
      "userId": 8,
      "username": "吴",
      "title": "Tequila Sunrise",
      "content": "夏天就是积攒美好回忆的",
      "tag": "推荐",
      "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%8E%A8%E8%8D%90/%E5%9B%BE%E7%89%87/6/270ca884eb1950ec1a652ca3765ba4f.png",
      "praisenum": 3333,
      "deleted": 0
    },
    "user": {
      "created": "2023-04-25T11:40:21.000+00:00",
      "updated": "2023-04-25T11:40:23.000+00:00",
      "id": 8,
      "username": "吴",
      "password": "123456",
      "phone": "12345678910",
      "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/22.jpg",
      "gender": 1,
      "age": 14,
      "introduction": "无"
    }
  },
  {
    "note": {
      "created": "2023-04-25T12:14:30.000+00:00",
      "updated": "2023-04-25T12:14:30.000+00:00",
      "id": 18,
      "userId": 14,
      "username": "JezZzZ",
      "title": "重庆什么天气啊一会儿冷一会儿热",
      "content": "六天课 杀了我",
      "tag": "穿搭",
      "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%A9%BF%E6%90%AD/%E5%9B%BE%E7%89%87/5/0733f8d4665325bc729dcae05a3de51.png",
      "praisenum": 667,
      "deleted": 0
    },
    "user": {
      "created": "2023-04-25T11:40:38.000+00:00",
      "updated": null,
      "id": 14,
      "username": "JezZzZ",
      "password": "123456",
      "phone": "12345678910",
      "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/29.jpg",
      "gender": 1,
      "age": 20,
      "introduction": "无"
    }
  },
  {
    "note": {
      "created": "2023-04-25T12:14:30.000+00:00",
      "updated": "2023-04-25T12:14:30.000+00:00",
      "id": 22,
      "userId": 18,
      "username": "苏沫",
      "title": "这个夏天总要去一趟屏山吧",
      "content": "国风",
      "tag": "旅行",
      "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%97%85%E8%A1%8C/%E8%A7%86%E9%A2%91/2/9.png",
      "praisenum": 8999,
      "deleted": 0
    },
    "user": {
      "created": "2023-04-25T11:40:49.000+00:00",
      "updated": null,
      "id": 18,
      "username": "苏沫",
      "password": "123456",
      "phone": "12345678910",
      "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/34.jpg",
      "gender": 1,
      "age": 24,
      "introduction": "无"
    }
  },
  {
    "note": {
      "created": "2023-04-25T12:14:30.000+00:00",
      "updated": "2023-04-29T07:54:06.000+00:00",
      "id": 25,
      "userId": 1,
      "username": "xm",
      "title": "上海City walk 陆家嘴",
      "content": "陆家嘴网红三件套云朵书店震旦博物馆浦东美术馆东方明珠\r\n全程步行：3km，需要花费一天时间 7-8H\r\n路线包括：拍照+博物馆+艺术展+东方明珠\r\n沿途风景：很多地标性建筑，只要来上海必走路线，相比外滩人山人海，陆家嘴不拥挤的美景更值得",
      "tag": "旅行",
      "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%97%85%E8%A1%8C/%E5%9B%BE%E7%89%87/2/29e232bd30e6b22787a7351a0126e95.png",
      "praisenum": 7864,
      "deleted": 0
    },
    "user": {
      "created": "2023-04-24T12:22:55.000+00:00",
      "updated": "2023-05-04T07:17:47.000+00:00",
      "id": 1,
      "username": "xm",
      "password": "123456",
      "phone": "13850429386",
      "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/4.jpg",
      "gender": 1,
      "age": 22,
      "introduction": "无"
    }
  },
  {
    "note": {
      "created": "2023-04-25T12:14:30.000+00:00",
      "updated": "2023-04-25T12:14:30.000+00:00",
      "id": 29,
      "userId": 22,
      "username": "Pentaki",
      "title": "坐落在澳洲深处的宇宙之镜",
      "content": "夜幕降临，星空如诗如画地铺陈在头顶。天空之镜犹如一个宇宙之镜，将璀璨星辰、浩渺银河倒映其中，这一刻，仿佛成为了天地间独一无二的旅者。仰望星空，感受到宇宙的浩瀚无垠；俯瞰盐湖，能触摸到星辰的温度。",
      "tag": "旅行",
      "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%97%85%E8%A1%8C/%E5%9B%BE%E7%89%87/6/12cba05802734b7dbdd3d59d1c1dd93.png",
      "praisenum": 4572,
      "deleted": 0
    },
    "user": {
      "created": "2023-04-25T11:40:56.000+00:00",
      "updated": null,
      "id": 22,
      "username": "Pentaki",
      "password": "123456",
      "phone": "12345678910",
      "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/38.jpg",
      "gender": 1,
      "age": 28,
      "introduction": "无"
    }
  },
  {
    "note": {
      "created": "2023-04-25T12:14:30.000+00:00",
      "updated": "2023-04-25T12:14:30.000+00:00",
      "id": 32,
      "userId": 25,
      "username": "热爱生活的黄同学",
      "title": "春天不让女朋友出去浪的方法就是给她吃",
      "content": "给嘴馋的女朋友做了口水鸡，麻辣鲜香，肉嫩味美，还有外酥里嫩的椒盐虾仁，配上一锅荷包蛋焖面美滋滋    ",
      "tag": "美食",
      "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%BE%8E%E9%A3%9F/%E8%A7%86%E9%A2%91/2/%E5%B0%81%E9%9D%A2.png",
      "praisenum": 4578,
      "deleted": 0
    },
    "user": {
      "created": "2023-04-25T11:41:01.000+00:00",
      "updated": null,
      "id": 25,
      "username": "热爱生活的黄同学",
      "password": "123456",
      "phone": "12345678910",
      "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/40.jpg",
      "gender": 1,
      "age": 31,
      "introduction": "无"
    }
  },
  {
    "note": {
      "created": "2023-04-25T12:14:30.000+00:00",
      "updated": "2023-04-25T12:14:30.000+00:00",
      "id": 34,
      "userId": 27,
      "username": "椰汁波波",
      "title": "我爸尝了一口…让我原地开店",
      "content": "这个酸辣凉面真的泰适合夏天啦",
      "tag": "美食",
      "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%BE%8E%E9%A3%9F/%E5%9B%BE%E7%89%87/1/7f67277bf4753e3bce4491a6d0ac22d.png",
      "praisenum": 6565,
      "deleted": 0
    },
    "user": {
      "created": "2023-04-25T11:41:03.000+00:00",
      "updated": null,
      "id": 27,
      "username": "椰汁波波",
      "password": "123456",
      "phone": "12345678910",
      "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/42.jpg",
      "gender": 0,
      "age": 33,
      "introduction": "无"
    }
  },
  {
    "note": {
      "created": "2023-04-25T12:14:30.000+00:00",
      "updated": "2023-04-25T12:14:30.000+00:00",
      "id": 36,
      "userId": 29,
      "username": "雅雅饿了",
      "title": "奶奶传下来的配方，自制阿达子好吃绝了",
      "content": "手工阿达子真的太好吃啦，晶莹剔透、Q Q弹弹超级有嚼劲、Q弹爽口，糯叽叽比珍珠还好吃，夏天必备哦！！！",
      "tag": "美食",
      "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%BE%8E%E9%A3%9F/%E5%9B%BE%E7%89%87/3/1f31c8eeb972627a42bad21445ad0ce.png",
      "praisenum": 345,
      "deleted": 0
    },
    "user": {
      "created": "2023-04-25T11:41:05.000+00:00",
      "updated": null,
      "id": 29,
      "username": "雅雅饿了",
      "password": "123456",
      "phone": "12345678910",
      "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/45.jpg",
      "gender": 1,
      "age": 35,
      "introduction": "无"
    }
  },
  {
    "note": {
      "created": "2023-04-25T12:14:30.000+00:00",
      "updated": "2023-04-29T03:45:09.000+00:00",
      "id": 40,
      "userId": 1,
      "username": "xm",
      "title": "今天喝19.9，的椰奶星冰乐",
      "content": "星巴克奶油星冰乐换巴旦木奶，椰浆，可可碎片",
      "tag": "美食",
      "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%BE%8E%E9%A3%9F/%E5%9B%BE%E7%89%87/7/ab53ff3630fb1cec529500bf4f518c2.png",
      "praisenum": 654,
      "deleted": 0
    },
    "user": {
      "created": "2023-04-24T12:22:55.000+00:00",
      "updated": "2023-05-04T07:17:47.000+00:00",
      "id": 1,
      "username": "xm",
      "password": "123456",
      "phone": "13850429386",
      "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/4.jpg",
      "gender": 1,
      "age": 22,
      "introduction": "无"
    }
  },
  {
    "note": {
      "created": "2023-04-25T12:14:30.000+00:00",
      "updated": "2023-04-25T12:14:30.000+00:00",
      "id": 44,
      "userId": 34,
      "username": "阿棒的觅食计划",
      "title": "愿每个去长沙的人都能刷到",
      "content": "马上五一假期了，好多朋友来长沙旅游！作为在长沙学习生活7年的土著，给大家整理了「2天1夜的自由行线路攻略」，有需要的宝子可以参考我的行程哦！一点不会踩雷！",
      "tag": "其它",
      "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E5%85%B6%E5%AE%83/%E5%9B%BE%E7%89%87/1/0e4e98e85cac442efe792e7a7330a88.png",
      "praisenum": 673,
      "deleted": 0
    },
    "user": {
      "created": "2023-04-25T11:41:09.000+00:00",
      "updated": null,
      "id": 34,
      "username": "阿棒的觅食计划",
      "password": "123456",
      "phone": "12345678910",
      "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/50.jpg",
      "gender": 1,
      "age": 40,
      "introduction": "无"
    }
  },
  {
    "note": {
      "created": "2023-04-25T12:14:30.000+00:00",
      "updated": "2023-04-25T12:14:30.000+00:00",
      "id": 46,
      "userId": 36,
      "username": "Maxxx",
      "title": "釜山行",
      "content": "咱们去釜山尊的是去拍釜山行3的 落地大暴雨\r\n天气巨差 釜山的食物店把犬妹气哭",
      "tag": "其它",
      "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E5%85%B6%E5%AE%83/%E5%9B%BE%E7%89%87/3/12a4b2452df24057d083211955eafd0.png",
      "praisenum": 457,
      "deleted": 0
    },
    "user": {
      "created": "2023-04-25T11:41:11.000+00:00",
      "updated": null,
      "id": 36,
      "username": "Maxxx",
      "password": "123456",
      "phone": "12345678910",
      "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/11.jpg",
      "gender": 0,
      "age": 42,
      "introduction": "无"
    }
  }
]
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» note|object|true|none||none|
|»» created|string|true|none||none|
|»» updated|string|true|none||none|
|»» id|integer|true|none||none|
|»» userId|integer|true|none||none|
|»» username|string|true|none||none|
|»» title|string|true|none||none|
|»» content|string|true|none||none|
|»» tag|string|true|none||none|
|»» surfacePicture|string|true|none||none|
|»» praisenum|integer|true|none||none|
|»» collectionnum|integer|true|none||none|
|»» deleted|integer|true|none||none|
|» user|object|true|none||none|
|»» created|string|true|none||none|
|»» updated|string¦null|true|none||none|
|»» id|integer|true|none||none|
|»» username|string|true|none||none|
|»» password|string|true|none||none|
|»» phone|string|true|none||none|
|»» headphoto|string|true|none||none|
|»» gender|integer|true|none||none|
|»» age|integer|true|none||none|
|»» introduction|string|true|none||none|

## POST 评论笔记

POST /found/comment/{noteId}

提交笔记id和笔记的评论，还有请求头token进行笔记评论

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|noteId|path|integer| 是 ||none|
|comment|query|string| 是 ||评论|
|Authorization|header|string| 否 ||token|

> 返回示例

> 成功

```json
"保存成功"
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|null|

# 点赞

## POST 点赞和取消点赞

POST /praise/{noteId}

点赞表的praise默认为0，1为点赞，点赞时提交路径参数noteid和请求他token，后端进行处理将0变为1，表示已点赞，再次提交将1变为0表示取消点赞，未点赞过的笔记将保存到点赞表

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|noteId|path|integer| 是 ||none|
|Authorization|header|string| 是 ||token|

> 返回示例

> 成功

```json
"点赞成功"
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

# 收藏

## POST 收藏和取消收藏

POST /collection/{noteId}

收藏表的collection默认为0，1为收藏，收藏时提交路径参数noteid和请求头token，后端进行处理将0变为1，表示已收藏，再次提交将1变为0表示取消收藏,未收藏过的笔记将保存到收藏表

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|noteId|path|integer| 是 ||none|
|Authorization|header|string| 是 ||token|

> 返回示例

> 成功

```json
"点赞成功"
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|null|

# 发布

## POST 发布笔记

POST /release/note

提交参数和请求头token，后端进行保存

> Body 请求参数

```json
{
  "surfacePicture": "string",
  "title": "string",
  "content": "string",
  "tag": "string",
  "pictureurl": [
    "string"
  ],
  "videourl": "string"
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|Authorization|header|string| 否 ||token|
|body|body|object| 否 ||none|
|» surfacePicture|body|string| 是 | 封面图片|none|
|» title|body|string| 是 | 标题|none|
|» content|body|string| 是 | 笔记内容|none|
|» tag|body|string| 是 | 标签|none|
|» pictureurl|body|[string]| 否 | 上传图片|none|
|» videourl|body|string| 否 | 上传视频|none|

> 返回示例

> 200 Response

```json
{}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

## POST 上传视频

POST /release/uploadVideo

发布笔记时，选择上传视频，提交视频文件和请求头token，后端将视频文件解析，上传到阿里云并返回视频URL地址

> Body 请求参数

```yaml
video: string

```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|Authorization|header|string| 否 ||none|
|body|body|object| 否 ||none|
|» video|body|string(binary)| 否 ||none|

> 返回示例

> 成功

```json
"https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/2023/04/28/a9ac7092-345e-474e-ba7b-805f72289ef1.mp4"
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

## POST 上传图片

POST /release/uploadPicture

发布笔记时，选择上传图片，提交图片文件和请求头token，后端将图片文件遍历解析，上传到阿里云并返回视频URL地址列表

> Body 请求参数

```yaml
pictureList: string

```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|Authorization|header|string| 是 ||none|
|body|body|object| 否 ||none|
|» pictureList|body|string(binary)| 否 ||图片列表|

> 返回示例

> 成功

```json
[
  "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/2023/04/28/0dc291fa-4f7f-4f28-b56e-b234de2e26ba.png",
  "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/2023/04/28/7063a76e-0bbd-4d73-9ee4-a7588a51d57c.png"
]
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

# 笔记管理

## GET 笔记管理页面（分页）

GET /manage

提交当前页数和页尺寸，请求头token，后端进行分页处理并响应结果

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|page|query|integer| 否 ||当前页数|
|pageSize|query|integer| 否 ||页尺寸|
|Authorization|header|string| 是 ||token|

> 返回示例

> 成功

```json
{
  "records": [
    {
      "created": "2023-04-25T12:14:30.000+00:00",
      "updated": "2023-04-25T12:14:30.000+00:00",
      "id": 1,
      "userId": 1,
      "username": "xm",
      "title": "趁天还没热再来叠穿下",
      "content": "不然就来不及了",
      "tag": "推荐",
      "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%8E%A8%E8%8D%90/%E8%A7%86%E9%A2%91/1/%E5%B0%81%E9%9D%A2.png",
      "praisenum": 34244,
      "deleted": 0
    },
    {
      "created": "2023-04-25T12:14:30.000+00:00",
      "updated": "2023-04-25T12:14:30.000+00:00",
      "id": 2,
      "userId": 1,
      "username": "xm",
      "title": "巴黎世家特卖会",
      "content": "开心看看买了啥",
      "tag": "推荐",
      "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%8E%A8%E8%8D%90/%E8%A7%86%E9%A2%91/2/%E5%B0%81%E9%9D%A2.png",
      "praisenum": 1423,
      "deleted": 0
    },
    {
      "created": "2023-04-25T12:14:30.000+00:00",
      "updated": "2023-04-25T12:14:30.000+00:00",
      "id": 14,
      "userId": 1,
      "username": "xm",
      "title": "让我看看到底有啥不一样",
      "content": "ererer",
      "tag": "穿搭",
      "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%A9%BF%E6%90%AD/%E5%9B%BE%E7%89%87/1/4.png",
      "praisenum": 963,
      "deleted": 0
    },
    {
      "created": "2023-04-25T12:14:30.000+00:00",
      "updated": "2023-04-25T12:14:30.000+00:00",
      "id": 15,
      "userId": 1,
      "username": "xm",
      "title": "小高最近 ",
      "content": "看到自己在商场里啦！开心嘿嘿",
      "tag": "穿搭",
      "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%A9%BF%E6%90%AD/%E5%9B%BE%E7%89%87/2/5.png",
      "praisenum": 6433,
      "deleted": 0
    },
    {
      "created": "2023-04-25T12:14:30.000+00:00",
      "updated": "2023-04-25T12:14:30.000+00:00",
      "id": 16,
      "userId": 1,
      "username": "xm",
      "title": "变回21年卷毛偷米咯",
      "content": "期待一下罗鼠准备筹备巡演啦！",
      "tag": "穿搭",
      "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%A9%BF%E6%90%AD/%E5%9B%BE%E7%89%87/3/fa48205a52d4656ae5ba2c0442ee281.png",
      "praisenum": 4562,
      "deleted": 0
    },
    {
      "created": "2023-04-25T12:14:30.000+00:00",
      "updated": "2023-04-25T12:14:30.000+00:00",
      "id": 24,
      "userId": 1,
      "username": "xm",
      "title": "真实经历，这些坑希望你在平潭千万不要踩",
      "content": "血泪教训，想近期平潭环岛游的uu们请收下这份环岛拍照/路线攻略和避坑指南！",
      "tag": "旅行",
      "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%97%85%E8%A1%8C/%E5%9B%BE%E7%89%87/1/28eb92a6ea0dcfa9819da74027fb81f.png",
      "praisenum": 433,
      "deleted": 0
    },
    {
      "created": "2023-04-25T12:14:30.000+00:00",
      "updated": "2023-04-25T12:14:30.000+00:00",
      "id": 25,
      "userId": 1,
      "username": "xm",
      "title": "上海City walk 陆家嘴",
      "content": "陆家嘴网红三件套云朵书店震旦博物馆浦东美术馆东方明珠\r\n全程步行：3km，需要花费一天时间 7-8H\r\n路线包括：拍照+博物馆+艺术展+东方明珠\r\n沿途风景：很多地标性建筑，只要来上海必走路线，相比外滩人山人海，陆家嘴不拥挤的美景更值得",
      "tag": "旅行",
      "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%97%85%E8%A1%8C/%E5%9B%BE%E7%89%87/2/29e232bd30e6b22787a7351a0126e95.png",
      "praisenum": 7864,
      "deleted": 0
    },
    {
      "created": "2023-04-25T12:14:30.000+00:00",
      "updated": "2023-04-25T12:14:30.000+00:00",
      "id": 26,
      "userId": 1,
      "username": "xm",
      "title": "大二学生穷游威海",
      "content": "总要去一次威海吧",
      "tag": "旅行",
      "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%97%85%E8%A1%8C/%E5%9B%BE%E7%89%87/3/f7228ecc01bb58ea03b9098e3732050.png",
      "praisenum": 346,
      "deleted": 0
    },
    {
      "created": "2023-04-25T12:14:30.000+00:00",
      "updated": "2023-04-25T12:14:30.000+00:00",
      "id": 38,
      "userId": 1,
      "username": "xm",
      "title": "分享近期在厦门吃到的...（非常好次的合集）",
      "content": "厦门美食，我的美食日记",
      "tag": "美食",
      "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%BE%8E%E9%A3%9F/%E5%9B%BE%E7%89%87/5/5f3870abfd29bc015a91db365085d9b.png",
      "praisenum": 45,
      "deleted": 0
    },
    {
      "created": "2023-04-25T12:14:30.000+00:00",
      "updated": "2023-04-25T12:14:30.000+00:00",
      "id": 39,
      "userId": 1,
      "username": "xm",
      "title": "1r多早餐店倒闭有它一半责任！",
      "content": "往外直透油的肉包子！谁懂啊啊啊！！",
      "tag": "美食",
      "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E7%BE%8E%E9%A3%9F/%E5%9B%BE%E7%89%87/6/7246eb9b57ee9a4e7c2d91bd37901df.png",
      "praisenum": 665,
      "deleted": 0
    }
  ],
  "total": 14,
  "size": 10,
  "current": 1,
  "orders": [],
  "optimizeCountSql": true,
  "hitCount": false,
  "countId": null,
  "maxLimit": null,
  "searchCount": true,
  "pages": 2
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» records|[object]|true|none||none|
|»» created|string|true|none||none|
|»» updated|string|true|none||none|
|»» id|integer|true|none||none|
|»» userId|integer|true|none||none|
|»» username|string|true|none||none|
|»» title|string|true|none||none|
|»» content|string|true|none||none|
|»» tag|string|true|none||none|
|»» surfacePicture|string|true|none||none|
|»» praisenum|integer|true|none||none|
|»» deleted|integer|true|none||none|
|» total|integer|true|none||none|
|» size|integer|true|none||none|
|» current|integer|true|none||none|
|» orders|[string]|true|none||none|
|» optimizeCountSql|boolean|true|none||none|
|» hitCount|boolean|true|none||none|
|» countId|null|true|none||none|
|» maxLimit|null|true|none||none|
|» searchCount|boolean|true|none||none|
|» pages|integer|true|none||none|

## PUT 删除笔记

PUT /manage/remove/{noteId}

提交路径参数noteid和请求头，后端将笔记表的deleted修改为1表示删除

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|noteId|path|integer| 是 ||none|
|Authorization|header|string| 否 ||token|

> 返回示例

> 200 Response

```json
{}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

# 购物

## GET 商品首页面

GET /shopping

提交登录时后端响应的token，后端响应一个map集合包含推荐笔记列表和所有笔记列表

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|Authorization|header|string| 否 ||token|

> 返回示例

> 成功

```json
{
  "所有商品": [
    {
      "created": "2023-04-30T06:19:17.000+00:00",
      "updated": null,
      "id": 1,
      "goodsName": "创意家居生活用品",
      "price": 18.5,
      "goodsContent": "品牌: 小凡家居风格: 时尚包装种类:",
      "goodsTag": "家居",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%8E%A8%E8%8D%90/1/O1CN0160sQnm23r793wD3S8_%21%21267817308.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:20.000+00:00",
      "updated": null,
      "id": 2,
      "goodsName": "德古德训鞋",
      "price": 200,
      "goodsContent": "品牌: Lidaren Produced闭合方式: 系带尺码: 34 35 36 37 38 39 40 41 42图案: 拼色风格: 韩版流行元素: 交叉绑带 拼色后跟高: 平跟颜色分类: 白色 真皮白 白色（厚底） 真皮白（厚底）货号: 1926-1上市年份季节",
      "goodsTag": "家居",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%8E%A8%E8%8D%90/1%20-%20%E5%89%AF%E6%9C%AC/O1CN01NVGvsc2AORhBr9xI0_%21%21127138193.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:22.000+00:00",
      "updated": null,
      "id": 3,
      "goodsName": "德训鞋女款小众复古奶茶阿甘鞋小白鞋",
      "price": 87.9,
      "goodsContent": "日常跟底款式: 平底鞋底材质: 橡胶内里材质: 超细纤维适用对象: 青年开口深度: 浅口鞋制作工艺: 胶粘鞋款式: 德训鞋帮面材质: 二层牛皮（除牛反绒）",
      "goodsTag": "家居",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%8E%A8%E8%8D%90/1%20-%20%E5%89%AF%E6%9C%AC%20%282%29/O1CN01VgnYNI1c6PFEHC7aE_%21%21876273551.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:24.000+00:00",
      "updated": null,
      "id": 4,
      "goodsName": "舍涂Shetu小众三原康裕骨头溶解鞋",
      "price": 178,
      "goodsContent": "品牌: 舍涂功能: 增高闭合方式: 系带尺码: 35女码（现货） 36女码（现货） 37女码（现货 修面皮鞋制作工艺: 胶粘鞋鞋面材质: 二层牛皮（除牛反绒）鞋垫材质: 头层猪皮款式: 板鞋销售渠道类型: 纯电商(只在线上销售)",
      "goodsTag": "家居",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%8E%A8%E8%8D%90/1%20-%20%E5%89%AF%E6%9C%AC%20%283%29/O1CN017sHkIQ2A6aEFmxroN_%21%21677978154.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:28.000+00:00",
      "updated": null,
      "id": 5,
      "goodsName": "冬季真皮马丁靴男切尔西靴子",
      "price": 583,
      "goodsContent": "品牌: other/其他功能: 耐磨闭合方式: 系带尺码: 38 39 40 41 42 43 44风格: 厚底鞋底材质: 橡胶鞋面内里材质: 二层猪皮适用对象: 青年（18-40周岁）真皮材质工艺: 磨砂皮鞋面材质: 头层猪皮鞋垫材质: 头层猪皮款式: 马丁靴靴筒材质: 头层猪皮靴筒内里材质: 头层猪皮",
      "goodsTag": "家居",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%8E%A8%E8%8D%90/1%20-%20%E5%89%AF%E6%9C%AC%20%284%29/O1CN01p46qH51OA9mG1lHA6_%21%212259221664.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:32.000+00:00",
      "updated": null,
      "id": 6,
      "goodsName": "Midea/美的大1.5匹p空调",
      "price": 3399,
      "goodsContent": "CCC证书编号: 2020010703276793空调品牌: Midea/美的美的空调型号: KFR-35GW/功能: 除菌空调功率: 大1.5匹售后服务: ",
      "goodsTag": "家居",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%8E%A8%E8%8D%90/1%20-%20%E5%89%AF%E6%9C%AC%20%285%29/O1CN01ruQZwz1rUQBFTvXFY_%21%212210852105634.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:34.000+00:00",
      "updated": null,
      "id": 7,
      "goodsName": "新品国行Dyson戴森吹风机",
      "price": 2840,
      "goodsContent": "产品名称: dyson/戴森 HD08电吹风品牌: dyson/戴森型号: HD08功能: 冷热风 护发售后服务: 全国联保产地:",
      "goodsTag": "家居",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%8E%A8%E8%8D%90/1%20-%20%E5%89%AF%E6%9C%AC%20%286%29/O1CN01cYLzTh1caAvEl5B11_%21%211777573616.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:35.000+00:00",
      "updated": null,
      "id": 8,
      "goodsName": "家居家义乌商贸城小商品小百货",
      "price": 0.88,
      "goodsContent": "：包装种类: 其他颜色分类: 薄款 厚款适用对象: 其他礼品类别: 其他礼品",
      "goodsTag": "家居",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%8E%A8%E8%8D%90/1%20-%20%E5%89%AF%E6%9C%AC%20%287%29/O1CN014nTnRg26qbQWlLWvQ_%21%211712577713.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:36.000+00:00",
      "updated": null,
      "id": 9,
      "goodsName": "创意居家居厨房用品用具小百货家用大全",
      "price": 8.8,
      "goodsContent": "包装种类: 其他颜色分类: 橘红 咖啡 藏青礼品类别: 其他礼品",
      "goodsTag": "家居",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%8E%A8%E8%8D%90/1%20-%20%E5%89%AF%E6%9C%AC%20%288%29/O1CN019p9OXW25IshdpAh51_%21%211660857504.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:36.000+00:00",
      "updated": null,
      "id": 10,
      "goodsName": "日本进口MUJIΕ家居厨房用品用具小百货",
      "price": 75,
      "goodsContent": "品牌: MUJIE/慕杰包装种类: 其他颜色分类: 轻奢蓝 轻奢白",
      "goodsTag": "家居",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%8E%A8%E8%8D%90/1%20-%20%E5%89%AF%E6%9C%AC%20%289%29/O1CN011bNU8X2GVfgP5OhjX_%21%212200567069021.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:37.000+00:00",
      "updated": null,
      "id": 11,
      "goodsName": "家居用品用具小百货",
      "price": 9.8,
      "goodsContent": "包装种类: 其他颜色分类: 白色 黄色 红色",
      "goodsTag": "平价",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%B9%B3%E4%BB%B7/new/O1CN0109ZFuV25IshaJHuTL_%21%211660857504.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:37.000+00:00",
      "updated": null,
      "id": 12,
      "goodsName": "创意家居日用小商品厨房用品",
      "price": 1.61,
      "goodsContent": "品牌: other/其他风格: 日式包装种类: 其他颜色分类: 长方形毛重: 4g适用节日: 春节是否可定制: 否",
      "goodsTag": "平价",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%B9%B3%E4%BB%B7/new%20-%20%E5%89%AF%E6%9C%AC/QQ%E6%88%AA%E5%9B%BE20230425183202.png",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:40.000+00:00",
      "updated": null,
      "id": 13,
      "goodsName": "家居家用小东西家庭厨房卫生间用品",
      "price": 5.39,
      "goodsContent": "包装种类: 其他颜色分类: 强力透明款 10个装 强力透明款 20个装 强力透明款40个装【立省5元】",
      "goodsTag": "平价",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%B9%B3%E4%BB%B7/new%20-%20%E5%89%AF%E6%9C%AC%20%282%29/O1CN016F1OuP25IsftQfhJl_%21%211660857504.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:40.000+00:00",
      "updated": null,
      "id": 14,
      "goodsName": "创意居家居用品用具",
      "price": 1.5,
      "goodsContent": "是否量贩装: 否",
      "goodsTag": "平价",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%B9%B3%E4%BB%B7/new%20-%20%E5%89%AF%E6%9C%AC%20%283%29/TB17jMGSXXXXXX3XXXXXXXXXXXX_%21%210-item_pic.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:41.000+00:00",
      "updated": null,
      "id": 15,
      "goodsName": "抖音居家居厨房用品用具",
      "price": 15,
      "goodsContent": "包装种类: 其他颜色分类: 白色 乳白色 浅灰色 灰色 绿色 蓝色 深蓝色 墨绿色 宝蓝色 米白色 桔红色 小号颜色随机一个 中号颜色随机一个 大号颜色随机一个",
      "goodsTag": "平价",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%B9%B3%E4%BB%B7/new%20-%20%E5%89%AF%E6%9C%AC%20%284%29/O1CN01NE58xC25Isml5o13q_%21%211660857504.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:42.000+00:00",
      "updated": null,
      "id": 16,
      "goodsName": "创意家居厨房用品用具",
      "price": 24.79,
      "goodsContent": "包装种类: 其他颜色分类: 黑色1个装(送1个挂钩) 黄色1个装(送1个挂钩) 灰色1个装(送1个挂钩) 黑色2个装(送2个挂钩) ",
      "goodsTag": "平价",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%B9%B3%E4%BB%B7/new%20-%20%E5%89%AF%E6%9C%AC%20%285%29/O1CN01oG53Cd25IsqZBNhwf_%21%211660857504.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:38.000+00:00",
      "updated": null,
      "id": 17,
      "goodsName": "大学生活住校生宿舍用品",
      "price": 11.19,
      "goodsContent": "包装种类: 其他颜色分类: 1个装【黑色】 1个装【白色】 2个装【黑色】",
      "goodsTag": "平价",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%B9%B3%E4%BB%B7/new%20-%20%E5%89%AF%E6%9C%AC%20%286%29/O1CN019bhUR925IsqFVRR5j_%21%211660857504.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:42.000+00:00",
      "updated": null,
      "id": 18,
      "goodsName": "清洁洗碗神器日常用品",
      "price": 18.89,
      "goodsContent": "包装种类: 其他颜色分类: 4个装（颜色随机） 8个装（颜色随机） 12个装（颜色随机）礼品类别: 其他礼品",
      "goodsTag": "平价",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%B9%B3%E4%BB%B7/new%20-%20%E5%89%AF%E6%9C%AC%20%287%29/O1CN01PVUHWS25IsiiAo2yc_%21%211660857504.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:46.000+00:00",
      "updated": null,
      "id": 19,
      "goodsName": "懒人神器",
      "price": 11.79,
      "goodsContent": "包装种类: 其他颜色分类: 2大1小6件套（军绿色） 2大1小6件套（酒红色） 2大1小6件套（灰蓝色） 2大1小6件套（米色） 2大1小6件套（撞色蓝） 2大1小6件套（撞色粉） 2大1小6件套（撞色绿） 1大1小4件套（军绿色）",
      "goodsTag": "平价",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%B9%B3%E4%BB%B7/new%20-%20%E5%89%AF%E6%9C%AC%20%288%29/O1CN019i3Urs25Isr2U1PHK_%21%211660857504.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:47.000+00:00",
      "updated": null,
      "id": 20,
      "goodsName": "洗手盆漏网不锈钢厨房下水道过滤网",
      "price": 2.1,
      "goodsContent": "颜色分类: 小号 中号 大号 特大号",
      "goodsTag": "平价",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%B9%B3%E4%BB%B7/new%20-%20%E5%89%AF%E6%9C%AC%20%289%29/TB2KSUAX1n85uJjSZFvXXXIgXXa_%21%211660857504.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:47.000+00:00",
      "updated": null,
      "id": 21,
      "goodsName": "F重磅230g夏季FORNINES刺绣FOR9插肩袖短袖T恤男上衣潮牌宽松半袖",
      "price": 68,
      "goodsContent": "品牌: 其它/other尺码: M L XL 2XL花型图案: 字母/数字/文字领型: 圆领颜色: 咖啡色 黑色 军绿色袖型: 插肩袖细分风格: 美式休闲基础风格: 青春流行适用季节: 夏季上市年份季节: 2023年夏季袖长: 短袖厚薄: 常规适用场景: 日常版型: 宽松型款式细节: 绣花服饰工艺: 刺绣适用对象: 青年印花主题: 文字思想",
      "goodsTag": "潮流",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%BD%AE%E6%B5%81/1/O1CN01Ann8ZI2AxiHpiJe9G_%21%21862068270.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:49.000+00:00",
      "updated": null,
      "id": 22,
      "goodsName": "花花公子短袖t恤男士夏季薄款潮牌宽松青少年男装五分半袖上衣服",
      "price": 138,
      "goodsContent": "品牌：PLAYBOY/花花公子尺码：M L XL 2XL 3XL 4XL 5XL面料分类：棉毛布\r\n花型图案：字母/数字/文字领型：圆领颜色：白色 黑色 深灰色 石青色",
      "goodsTag": "潮流",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%BD%AE%E6%B5%81/1%20-%20%E5%89%AF%E6%9C%AC/O1CN01PYq3rW1hYroB1f46N_%21%212075424290.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:52.000+00:00",
      "updated": null,
      "id": 23,
      "goodsName": "外贸t恤男剪标短袖阿美咔叽美式纯棉出口原尾单男装男士体恤上衣",
      "price": 399,
      "goodsContent": "品牌: rxvuq尺码: M L XL 2XL 3XL面料分类: 棉毛布花型图案: 卡通动漫领型: 圆领颜色: 8615白色 8615黑色 8615军绿色 8607灰蓝色 8607黑色 8607铁灰色 8603灰蓝色 8603铁灰色 8603卡其色 8609白色 8609黑色 8609灰色 8610灰色 8610灰绿 8610黑色 8611白色 8611蓝色 8611黑色 8612白色 8612深灰 8612",
      "goodsTag": "潮流",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%BD%AE%E6%B5%81/1%20-%20%E5%89%AF%E6%9C%AC%20%282%29/O1CN01soZwuI2I5Dy3OWhKT_%21%212850899234.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:53.000+00:00",
      "updated": null,
      "id": 24,
      "goodsName": "美式复古后背印花t恤男短袖潮牌百搭潮流打底衫外贸尾单男装上衣",
      "price": 149,
      "goodsContent": "品牌: rxvuq尺码: M L XL 2XL 3XL面料分类: 棉毛布花型图案: 字母/数字/文字领型: 圆领颜色: 白色 湖蓝色 藏青色 铁灰色袖型: 常规货号: 28519细分风格: 美式休闲基础风格: 青春流行品牌类型: 时尚潮牌适用季节: 夏季上市年份季节: 2023年夏季袖长: 短袖厚薄: 常规适用场景: 其他休闲版型: 修身款式细节: 印花服饰工艺: 水洗适用对象: 青年印花主题: 复古民族",
      "goodsTag": "潮流",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%BD%AE%E6%B5%81/1%20-%20%E5%89%AF%E6%9C%AC%20%283%29/O1CN01h2Q7Lm2I5E5RSAqfs_%21%212850899234.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:54.000+00:00",
      "updated": null,
      "id": 25,
      "goodsName": "【KGOODS】260克重磅夏季国潮潮牌字母印花情侣宽松圆领短袖T恤男",
      "price": 128,
      "goodsContent": "品牌: HYPERBASIC尺码: S M L XL花型图案: 字母/数字/文字领型: 圆领颜色: 米白色 黑白色 黑玫红色 棕绿色 白粉色 浅粉色 黑白色预售 黑玫红色预售 浅黄色袖型: 常规货号: HB23SS-022细分风格: 潮基础风格: 青春流行品牌类型: 时尚潮牌适用季节: 夏季上市年份季节: 2023年春季袖长: 短袖厚薄: 常规适用场景: 日常版型: 宽松型款式细节: 印花服饰工艺: 免烫处理适用对象: 青年印花主题: 创意趣味材质成分: 棉100%",
      "goodsTag": "潮流",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%BD%AE%E6%B5%81/1%20-%20%E5%89%AF%E6%9C%AC%20%285%29/QQ%E6%88%AA%E5%9B%BE20230425182237.png",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:54.000+00:00",
      "updated": null,
      "id": 26,
      "goodsName": "国潮休闲宽松开衫棒球服男短袖棒球衬衣衬衫女嘻哈",
      "price": 166,
      "goodsContent": "品牌: 其他/other尺码: S M L XL面料分类: 色织布图案: 其他/other领型: 其他/other颜色: 黑色 藏蓝色货号: KF19SS-SYGU0010细分风格: 嘻哈基础风格: 青春流行适用季节: 四季通用上市年份季节: 2023年春季袖长: 短袖厚薄: 常规适用场景: 其他休闲版型: 宽松型服装款式细节: 拼色服饰工艺: 其他适用对象: 青年面料功能: 免烫材质成分: 聚酯纤维100%",
      "goodsTag": "潮流",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%BD%AE%E6%B5%81/1%20-%20%E5%89%AF%E6%9C%AC%20%286%29/O1CN01VkWKHm1yWtXdCMDAw_%21%2188766587.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:55.000+00:00",
      "updated": null,
      "id": 27,
      "goodsName": "Turnthetables基础款印花T恤男女宽松休闲圆领短袖上衣",
      "price": 158,
      "goodsContent": "品牌: Turnthetables尺码: S M L XL花型图案: 纯色领型: 圆领颜色: 白色 黑色 黄色 蓝色 绿色袖型: 常规货号: TTT21SS-014细分风格: 潮基础风格: 青春流行品牌类型: 时尚潮牌适用季节: 夏季上市年份季节: 2021年夏季袖长: 短袖厚薄: 常规适用场景: 其他休闲版型: 宽松型款式细节: 印花服饰工艺: 免烫处理适用对象: 青年印花主题: 品牌LOGO",
      "goodsTag": "潮流",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%BD%AE%E6%B5%81/1%20-%20%E5%89%AF%E6%9C%AC%20%287%29/O1CN01OY71pV1yWtVkP195u_%21%2188766587.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:55.000+00:00",
      "updated": null,
      "id": 28,
      "goodsName": "Turnthetables潮牌宽松上衣日系加绒复古枣红色卫衣男",
      "price": 533,
      "goodsContent": "品牌: Turnthetables尺码: S M L XL图案: 其他/other领型: 圆领颜色: 枣红色-加绒 绿色-加绒 黑色-加绒 卡其色-加绒 紫色-加绒 花灰色-加绒 红色-毛圈底 黑色-毛圈底 绿色-毛圈底 紫色-毛圈底 荧光黄-毛圈底 深灰色-毛圈底 黑色-加绒预售 绿色-加绒预售 花灰色-加绒预售 枣红色-加绒预售 紫色-加绒预售货号: KF19AW-TTT012细分风格: 潮基础风格: 青春流行上市年份季节: 2019年冬季厚薄: 加绒版型: 宽松型款式: 套头",
      "goodsTag": "潮流",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%BD%AE%E6%B5%81/1%20-%20%E5%89%AF%E6%9C%AC%20%287%29/O1CN01y1unJO1yWtUiyFfd4_%21%2188766587.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:56.000+00:00",
      "updated": null,
      "id": 29,
      "goodsName": "圆领长袖情侣t恤纯色纯棉打底衫男上衣春季",
      "price": 421,
      "goodsContent": "品牌: Turnthetables尺码: S M L XL面料分类: 其他花型图案: 纯色领型: 其他/other颜色: 白色 湖蓝色 桔红色 黑色 蓝色 绿色袖型: 常规货号: KF20AW-TTT022细分风格: 潮基础风格: 青春流行品牌类型: 时尚潮牌适用季节: 秋季上市年份季节: 2020年秋季袖长: 长袖厚薄: 常规适用场景: 日常版型: 宽松型款式细节: 其他服饰工艺: 免烫处理适用对象: 青少年",
      "goodsTag": "潮流",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%BD%AE%E6%B5%81/1%20-%20%E5%89%AF%E6%9C%AC%20%288%29/O1CN014kMYa71yWtUhglynb_%21%2188766587.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:57.000+00:00",
      "updated": null,
      "id": 30,
      "goodsName": "幻彩反光印花长袖上衣嘻哈情侣t恤潮",
      "price": 234,
      "goodsContent": "品牌: Turnthetables尺码: S M L XL面料分类: 其他花型图案: 渐变领型: 圆领颜色: 白色 灰色 尺码表 黑色袖型: 常规货号: KF20AW-TTT006细分风格: 潮基础风格: 青春流行品牌类型: 时尚潮牌适用季节: 秋季上市年份季节: 2023年春季袖长: 长袖厚薄: 常规适用场景: 其他休闲版型: 宽松型款式细节: 其他服饰工艺: 免烫处理适用对象: 青少年印花主题: 品牌LOGO材质成分: 棉100%",
      "goodsTag": "潮流",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%BD%AE%E6%B5%81/1%20-%20%E5%89%AF%E6%9C%AC%20%289%29/O1CN01Hile4S1yWtUveE1Yj_%21%2188766587.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:57.000+00:00",
      "updated": null,
      "id": 31,
      "goodsName": "居家居厨房卫生间用品家用大全生活用具小百货小物件各种清洁神器",
      "price": 36.5,
      "goodsContent": "材质: 树脂风格: 北欧风格安装方式: 免打孔颜色分类: 薰衣草紫1包30片 薰衣草紫2包60片 薰衣草紫3包90片 薰衣草紫5包150片 薰衣草紫10包300片 海洋蓝1包30片 海洋蓝2包60片 海洋蓝3包90片 海洋蓝5包150片 海洋蓝10包300片层数: 1层是否手工: 否",
      "goodsTag": "其它",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%85%B6%E5%AE%83/new/O1CN013UlTrR21tHrUNTpuB_%21%212375307042.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:59.000+00:00",
      "updated": null,
      "id": 32,
      "goodsName": "厨房用品家用大全生活用具小百货厨具小物件家居各种居家除锈神器",
      "price": 23.8,
      "goodsContent": "包装种类: 简装颜色分类: 小瓶装【4瓶】共400ml 小瓶装【2瓶】共200ml 小瓶装【1瓶】100ml【试用装】 大瓶装【1瓶】350ml【热销装】 大瓶装【2瓶】350ml【实惠装】适用对象: 其他礼品类别: 其他礼品",
      "goodsTag": "其它",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%85%B6%E5%AE%83/new%20-%20%E5%89%AF%E6%9C%AC/O1CN016aQO1G1PcqCYVOOM0_%21%213452661862.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:59.000+00:00",
      "updated": null,
      "id": 33,
      "goodsName": "家居家用小东西居家生活日用品家庭厨房卫生间用品用具小百货大全",
      "price": 13.66,
      "goodsContent": "品牌: other/其他包装种类: 简装颜色分类: S码100只（TPE韧性强加厚） M码100只（TPE韧性强加厚） L码100只（TPE韧性强加厚） S码200只（TPE韧性强加厚） M码200只（TPE韧性强加厚） L码200只（TPE韧性强加厚）适用对象: 其他礼品类别: 其他礼品 创意类礼品",
      "goodsTag": "其它",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%85%B6%E5%AE%83/new%20-%20%E5%89%AF%E6%9C%AC%20%282%29/O1CN01ZUcoXp1dYAk1CN2RE_%21%212182353747.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:20:02.000+00:00",
      "updated": null,
      "id": 34,
      "goodsName": "抖音居家居用品用具",
      "price": 17.5,
      "goodsContent": "品牌: other/其他包装种类: 简装颜色分类: 白色1个 蓝黄1个 白色3个 蓝黄3个 白色6个 蓝黄6个 白3个+蓝黄3个礼品类别: 其他礼品 创意类礼品 装饰类",
      "goodsTag": "其它",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%85%B6%E5%AE%83/new%20-%20%E5%89%AF%E6%9C%AC%20%283%29/O1CN01NPV6R41dYAfG7hqpX_%21%212182353747.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:20:02.000+00:00",
      "updated": null,
      "id": 35,
      "goodsName": "简约家居用品用具家用小百货好物",
      "price": 52.3,
      "goodsContent": "品牌: LD家居风格: 简约包装种类: 其他颜色分类: 【灰色】1个 【粉色】1个 【蓝色】1个 【灰色】2个 【粉色】2个 【蓝色】2个 【粉色】1个+【灰色】1个 【蓝色】1个+【粉色】1个 【蓝色】1个+【灰色】1个 【每色一个】共3个毛重: 0.5货号: LD-3适用对象: 其他礼品类别: 其他礼品 创意类礼品",
      "goodsTag": "其它",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%85%B6%E5%AE%83/new%20-%20%E5%89%AF%E6%9C%AC%20%284%29/O1CN01GWbOib1z0fJ9GT9sX_%21%212516716652.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:20:03.000+00:00",
      "updated": null,
      "id": 36,
      "goodsName": "乐扣乐扣小型14寸手提化妆箱女便携洗漱收纳箱包迷你化妆包小巧",
      "price": 138.8,
      "goodsContent": "品牌: 乐扣乐扣质地: ABS闭合方式: 拉链图案: 卡通动漫成色: 全新尺寸: 14寸【无锁】赠运费险 14寸【带锁】赠运费险 15寸【无锁】赠运费险 15寸【带锁】赠运费险 16寸【无锁】赠运费险",
      "goodsTag": "其它",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%85%B6%E5%AE%83/new%20-%20%E5%89%AF%E6%9C%AC%20%285%29/O1CN01PcbhSR26kC7UoXsuk_%21%212211027117699.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:20:04.000+00:00",
      "updated": null,
      "id": 37,
      "goodsName": "欧美真皮编织女士手提包",
      "price": 780,
      "goodsContent": "品牌: 蔻盾质地: 羊皮闭合方式: 拉链图案: 格子风格: 欧美时尚形状: 横款方形成色: 全新流行元素: 编织颜色分类: 白色 黑色 宝蓝色 银红色 灰白色 雾霾蓝 大红色内部结构: 拉链暗袋 手机袋 证件位有无夹层: 无是否可折叠: 否货号: G03MS背包方式: 单肩斜挎手提适用场景: 休闲里料材质: 真皮肩带样式: 单根适用对象: 青年提拎部件类型: 软把箱包外袋种类: 带盖袋箱包硬度: 软款式: 单肩包大小: 中流行款式名称: 小方包",
      "goodsTag": "其它",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%85%B6%E5%AE%83/new%20-%20%E5%89%AF%E6%9C%AC%20%286%29/O1CN01Ao6z4G1xqIiI5RZsC_%21%213431946494.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:20:04.000+00:00",
      "updated": null,
      "id": 38,
      "goodsName": "日本ZD妈咪包新款时尚外出大容量多功能母婴包背包妈妈双肩包",
      "price": 336,
      "goodsContent": "品牌: ZIZI DONOHOE型号: 52785224适用年龄: 新生 3个月 6个月 12个月 18个月 2岁 9个月面料: 混纺风格: 休闲适用性别: 男女通用颜色分类: 绿色+送床垫 黑色+送床垫 灰色+送床垫 粉配灰升级款+送床垫 蓝色款升级款+送床垫",
      "goodsTag": "其它",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%85%B6%E5%AE%83/new%20-%20%E5%89%AF%E6%9C%AC%20%287%29/O1CN012YectV1bwmoF5KzrY_%21%21908003530.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:20:05.000+00:00",
      "updated": null,
      "id": 39,
      "goodsName": "纯棉婴儿衣服新生儿礼盒春夏刚初出生宝宝套装母婴用品满月送礼物",
      "price": 235,
      "goodsContent": "品牌: 兰咖小熊型号: 001适用年龄: 3个月 6个月 18个月 9个月面料: 其他/other风格: 卡通产地: 中国大陆省份: 江苏省地市: 无锡市适用性别: 女衣门襟: 单排扣件数: 20件及以上颜色分类: 粉色星星花A款礼盒 粉色星星花B款礼盒组合形式: 服装+用品货号: 001参考身高: 59cm(0-3个月宝宝） 66cm(3-6个月宝宝） 73cm(6-9个月宝宝） 80cm(9-12个月宝宝） 90cm(12-18个月宝宝）安全等级: A类材质成分: 其他材质100% 其他",
      "goodsTag": "其它",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%85%B6%E5%AE%83/new%20-%20%E5%89%AF%E6%9C%AC%20%288%29/O1CN01HUWvwk1aufUi5loyx_%21%212637083390.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:20:08.000+00:00",
      "updated": null,
      "id": 40,
      "goodsName": "新生的儿虎宝宝出生见面礼初生婴儿用品大全母婴礼盒满月百天礼物",
      "price": 568,
      "goodsContent": "品牌: other/其他型号: 母婴用品大全必备高端礼品男女孩H1适用年龄: 新生 3个月",
      "goodsTag": "其它",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%85%B6%E5%AE%83/new%20-%20%E5%89%AF%E6%9C%AC%20%289%29/O1CN010UgVEf276B3gNrD9f_%21%212213062167747.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:20:09.000+00:00",
      "updated": null,
      "id": 41,
      "goodsName": "厨房水龙头置物架",
      "price": 68,
      "goodsContent": "品牌: WNL/万年利功能: 其他/other材质: 塑料风格: 创意颜色分类: 【绿色】2个装",
      "goodsTag": "宝藏好店",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%AE%9D%E8%97%8F%E5%A5%BD%E5%BA%97/1/O1CN010fArx41Rfi0sxB20G_%21%212917322139.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:20:09.000+00:00",
      "updated": null,
      "id": 42,
      "goodsName": "厨房调料置物架",
      "price": 100,
      "goodsContent": "品牌: BOUSSAC（厨房用品）功能: 防锈材质: 金属风格: 创意安装方式: 置地式颜色分类: 单层圆形-黑色（360度可旋转 加固底盘） 双层圆形-黑色（360度可旋转 加固底盘）",
      "goodsTag": "宝藏好店",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%AE%9D%E8%97%8F%E5%A5%BD%E5%BA%97/1%20-%20%E5%89%AF%E6%9C%AC/O1CN01GK1QOh1Rfi0qZAtVA_%21%212917322139.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:20:11.000+00:00",
      "updated": null,
      "id": 43,
      "goodsName": "益伟免手洗海绵拖把",
      "price": 295,
      "goodsContent": "产品名称: 益伟 yw-20品牌: 益伟型号: YW-20颜色分类: 28cm加厚海绵拖把+1棉头/天蓝【不锈钢杆】 28cm加厚海绵拖把+1棉头/卡其【不锈钢杆】",
      "goodsTag": "宝藏好店",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%AE%9D%E8%97%8F%E5%A5%BD%E5%BA%97/1%20-%20%E5%89%AF%E6%9C%AC%20%282%29/O1CN011FDEHI1Rfi0nYMutz_%21%212917322139.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:20:13.000+00:00",
      "updated": null,
      "id": 44,
      "goodsName": "硅藻泥速干软地垫浴室卫生间门口吸水防滑脚垫子",
      "price": 76,
      "goodsContent": "品牌: 怡沁园材质: 硅藻泥图案: 卡通动漫风格: 简约现代产地: 中国大陆省份: 浙江省地市: 绍兴市尺寸: 40*60cm【加厚约4.0mm丨买一送一 ",
      "goodsTag": "宝藏好店",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%AE%9D%E8%97%8F%E5%A5%BD%E5%BA%97/1%20-%20%E5%89%AF%E6%9C%AC%20%283%29/O1CN01OCxSv51Rfi0naXaV0_%21%212917322139.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:20:13.000+00:00",
      "updated": null,
      "id": 45,
      "goodsName": "郁金香垃圾桶网红ins风家用大容量客厅小宿舍卧室厨房卫生间轻奢",
      "price": 137,
      "goodsContent": "品牌: STIMULATE RECORDS/激志容量: 12L形状: 圆桶形颜色分类: 圆形小号+20只垃圾袋-内外双桶 圆形大号+20只垃圾袋-内外双桶 ",
      "goodsTag": "宝藏好店",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%AE%9D%E8%97%8F%E5%A5%BD%E5%BA%97/1%20-%20%E5%89%AF%E6%9C%AC%20%284%29/O1CN016fevbe1Rfi0p00B7G_%21%212917322139.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:20:14.000+00:00",
      "updated": null,
      "id": 46,
      "goodsName": "垃圾桶客厅家用轻奢高档厨房卧室大容量高颜值现代大号2022新款",
      "price": 147,
      "goodsContent": "品牌: 飞达三和容量: 12L形状: 圆桶形颜色分类: 爱马橙 12L 内外双桶 珍珠白 12L 简约小鹿印花 墨玉绿 12L 内外双桶 靛青蓝 12L 简约小鹿印花 静谧黑 12L 简约小鹿印花 爱马橙金 15L H印花",
      "goodsTag": "宝藏好店",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%AE%9D%E8%97%8F%E5%A5%BD%E5%BA%97/1%20-%20%E5%89%AF%E6%9C%AC%20%285%29/O1CN018BbR0Z1Rfi0kjH9GE_%21%212917322139.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:20:15.000+00:00",
      "updated": null,
      "id": 47,
      "goodsName": "德国油污净厨房抽油烟机强力去油污清洗剂重清洁剂油除垢渍烟神器",
      "price": 354,
      "goodsContent": "品牌: 老管家系列: 重油污清洗剂香味: 柠檬香 【1瓶】进口魔力泡泡重油 【3瓶】进口魔力泡泡重油一喷净 【5瓶】进口魔力泡泡重油一喷净",
      "goodsTag": "宝藏好店",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%AE%9D%E8%97%8F%E5%A5%BD%E5%BA%97/1%20-%20%E5%89%AF%E6%9C%AC%20%286%29/O1CN018vxDZh1Rfi0ekvyhK_%21%212917322139.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:20:16.000+00:00",
      "updated": null,
      "id": 48,
      "goodsName": "厕所洗手间壁挂式收纳架子神器",
      "price": 166,
      "goodsContent": "品牌: 喵可可材质: 塑料风格: 简约安装方式: 免打孔流行元素: 纯色颜色分类: 俩杯牙刷架【送杯贴】 俩杯牙刷架+灰白色挤牙膏器【送杯贴】",
      "goodsTag": "宝藏好店",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%AE%9D%E8%97%8F%E5%A5%BD%E5%BA%97/1%20-%20%E5%89%AF%E6%9C%AC%20%287%29/O1CN012PAHaD1Rfi0lW3pDp_%21%212917322139.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:20:16.000+00:00",
      "updated": null,
      "id": 49,
      "goodsName": "厨房神器大全灶台用具用品",
      "price": 14.21,
      "goodsContent": "品牌: WNL/万年利材质: 其他颜色分类: 亚克力防水美缝贴【甜蜜水果款】 亚克力防水透明美缝贴【缤纷甜蜜款】 亚克力防水透明美缝贴【摩卡时光款】",
      "goodsTag": "宝藏好店",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%AE%9D%E8%97%8F%E5%A5%BD%E5%BA%97/1%20-%20%E5%89%AF%E6%9C%AC%20%288%29/O1CN01LWhuAj27Jv1zZMOnJ_%21%212214098687777.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:20:17.000+00:00",
      "updated": null,
      "id": 50,
      "goodsName": "厨房网红用品家用大全小百货壁挂式",
      "price": 33.67,
      "goodsContent": "品牌: WNL/万年利材质: 塑料颜色分类: 蚝油挤压器（黑色） 蚝油挤压器（白色） 蚝油挤压器（黑色）*2 蚝油挤压器（白色）*2 升级款-白灰色（赠吸管2根） 升级款-墨绿金色（赠吸管2根） 升级款-白金色（赠吸管2根）",
      "goodsTag": "宝藏好店",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%AE%9D%E8%97%8F%E5%A5%BD%E5%BA%97/1%20-%20%E5%89%AF%E6%9C%AC%20%289%29/O1CN01awLIQL1T1ysRqvuSf_%21%212358342323.jpg",
      "deleted": 0
    }
  ],
  "推荐商品": [
    {
      "created": "2023-04-30T06:19:17.000+00:00",
      "updated": null,
      "id": 1,
      "goodsName": "创意家居生活用品",
      "price": 18.5,
      "goodsContent": "品牌: 小凡家居风格: 时尚包装种类:",
      "goodsTag": "家居",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%8E%A8%E8%8D%90/1/O1CN0160sQnm23r793wD3S8_%21%21267817308.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:20:15.000+00:00",
      "updated": null,
      "id": 47,
      "goodsName": "德国油污净厨房抽油烟机强力去油污清洗剂重清洁剂油除垢渍烟神器",
      "price": 354,
      "goodsContent": "品牌: 老管家系列: 重油污清洗剂香味: 柠檬香 【1瓶】进口魔力泡泡重油 【3瓶】进口魔力泡泡重油一喷净 【5瓶】进口魔力泡泡重油一喷净",
      "goodsTag": "宝藏好店",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%AE%9D%E8%97%8F%E5%A5%BD%E5%BA%97/1%20-%20%E5%89%AF%E6%9C%AC%20%286%29/O1CN018vxDZh1Rfi0ekvyhK_%21%212917322139.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:35.000+00:00",
      "updated": null,
      "id": 8,
      "goodsName": "家居家义乌商贸城小商品小百货",
      "price": 0.88,
      "goodsContent": "：包装种类: 其他颜色分类: 薄款 厚款适用对象: 其他礼品类别: 其他礼品",
      "goodsTag": "家居",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%8E%A8%E8%8D%90/1%20-%20%E5%89%AF%E6%9C%AC%20%287%29/O1CN014nTnRg26qbQWlLWvQ_%21%211712577713.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:52.000+00:00",
      "updated": null,
      "id": 23,
      "goodsName": "外贸t恤男剪标短袖阿美咔叽美式纯棉出口原尾单男装男士体恤上衣",
      "price": 399,
      "goodsContent": "品牌: rxvuq尺码: M L XL 2XL 3XL面料分类: 棉毛布花型图案: 卡通动漫领型: 圆领颜色: 8615白色 8615黑色 8615军绿色 8607灰蓝色 8607黑色 8607铁灰色 8603灰蓝色 8603铁灰色 8603卡其色 8609白色 8609黑色 8609灰色 8610灰色 8610灰绿 8610黑色 8611白色 8611蓝色 8611黑色 8612白色 8612深灰 8612",
      "goodsTag": "潮流",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%BD%AE%E6%B5%81/1%20-%20%E5%89%AF%E6%9C%AC%20%282%29/O1CN01soZwuI2I5Dy3OWhKT_%21%212850899234.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:32.000+00:00",
      "updated": null,
      "id": 6,
      "goodsName": "Midea/美的大1.5匹p空调",
      "price": 3399,
      "goodsContent": "CCC证书编号: 2020010703276793空调品牌: Midea/美的美的空调型号: KFR-35GW/功能: 除菌空调功率: 大1.5匹售后服务: ",
      "goodsTag": "家居",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%8E%A8%E8%8D%90/1%20-%20%E5%89%AF%E6%9C%AC%20%285%29/O1CN01ruQZwz1rUQBFTvXFY_%21%212210852105634.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:20:13.000+00:00",
      "updated": null,
      "id": 44,
      "goodsName": "硅藻泥速干软地垫浴室卫生间门口吸水防滑脚垫子",
      "price": 76,
      "goodsContent": "品牌: 怡沁园材质: 硅藻泥图案: 卡通动漫风格: 简约现代产地: 中国大陆省份: 浙江省地市: 绍兴市尺寸: 40*60cm【加厚约4.0mm丨买一送一 ",
      "goodsTag": "宝藏好店",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%AE%9D%E8%97%8F%E5%A5%BD%E5%BA%97/1%20-%20%E5%89%AF%E6%9C%AC%20%283%29/O1CN01OCxSv51Rfi0naXaV0_%21%212917322139.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:47.000+00:00",
      "updated": null,
      "id": 20,
      "goodsName": "洗手盆漏网不锈钢厨房下水道过滤网",
      "price": 2.1,
      "goodsContent": "颜色分类: 小号 中号 大号 特大号",
      "goodsTag": "平价",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%B9%B3%E4%BB%B7/new%20-%20%E5%89%AF%E6%9C%AC%20%289%29/TB2KSUAX1n85uJjSZFvXXXIgXXa_%21%211660857504.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:20:02.000+00:00",
      "updated": null,
      "id": 35,
      "goodsName": "简约家居用品用具家用小百货好物",
      "price": 52.3,
      "goodsContent": "品牌: LD家居风格: 简约包装种类: 其他颜色分类: 【灰色】1个 【粉色】1个 【蓝色】1个 【灰色】2个 【粉色】2个 【蓝色】2个 【粉色】1个+【灰色】1个 【蓝色】1个+【粉色】1个 【蓝色】1个+【灰色】1个 【每色一个】共3个毛重: 0.5货号: LD-3适用对象: 其他礼品类别: 其他礼品 创意类礼品",
      "goodsTag": "其它",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%85%B6%E5%AE%83/new%20-%20%E5%89%AF%E6%9C%AC%20%284%29/O1CN01GWbOib1z0fJ9GT9sX_%21%212516716652.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:20:17.000+00:00",
      "updated": null,
      "id": 50,
      "goodsName": "厨房网红用品家用大全小百货壁挂式",
      "price": 33.67,
      "goodsContent": "品牌: WNL/万年利材质: 塑料颜色分类: 蚝油挤压器（黑色） 蚝油挤压器（白色） 蚝油挤压器（黑色）*2 蚝油挤压器（白色）*2 升级款-白灰色（赠吸管2根） 升级款-墨绿金色（赠吸管2根） 升级款-白金色（赠吸管2根）",
      "goodsTag": "宝藏好店",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%AE%9D%E8%97%8F%E5%A5%BD%E5%BA%97/1%20-%20%E5%89%AF%E6%9C%AC%20%289%29/O1CN01awLIQL1T1ysRqvuSf_%21%212358342323.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:32.000+00:00",
      "updated": null,
      "id": 6,
      "goodsName": "Midea/美的大1.5匹p空调",
      "price": 3399,
      "goodsContent": "CCC证书编号: 2020010703276793空调品牌: Midea/美的美的空调型号: KFR-35GW/功能: 除菌空调功率: 大1.5匹售后服务: ",
      "goodsTag": "家居",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%8E%A8%E8%8D%90/1%20-%20%E5%89%AF%E6%9C%AC%20%285%29/O1CN01ruQZwz1rUQBFTvXFY_%21%212210852105634.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:20:13.000+00:00",
      "updated": null,
      "id": 45,
      "goodsName": "郁金香垃圾桶网红ins风家用大容量客厅小宿舍卧室厨房卫生间轻奢",
      "price": 137,
      "goodsContent": "品牌: STIMULATE RECORDS/激志容量: 12L形状: 圆桶形颜色分类: 圆形小号+20只垃圾袋-内外双桶 圆形大号+20只垃圾袋-内外双桶 ",
      "goodsTag": "宝藏好店",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%AE%9D%E8%97%8F%E5%A5%BD%E5%BA%97/1%20-%20%E5%89%AF%E6%9C%AC%20%284%29/O1CN016fevbe1Rfi0p00B7G_%21%212917322139.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:20.000+00:00",
      "updated": null,
      "id": 2,
      "goodsName": "德古德训鞋",
      "price": 200,
      "goodsContent": "品牌: Lidaren Produced闭合方式: 系带尺码: 34 35 36 37 38 39 40 41 42图案: 拼色风格: 韩版流行元素: 交叉绑带 拼色后跟高: 平跟颜色分类: 白色 真皮白 白色（厚底） 真皮白（厚底）货号: 1926-1上市年份季节",
      "goodsTag": "家居",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%8E%A8%E8%8D%90/1%20-%20%E5%89%AF%E6%9C%AC/O1CN01NVGvsc2AORhBr9xI0_%21%21127138193.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:32.000+00:00",
      "updated": null,
      "id": 6,
      "goodsName": "Midea/美的大1.5匹p空调",
      "price": 3399,
      "goodsContent": "CCC证书编号: 2020010703276793空调品牌: Midea/美的美的空调型号: KFR-35GW/功能: 除菌空调功率: 大1.5匹售后服务: ",
      "goodsTag": "家居",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%8E%A8%E8%8D%90/1%20-%20%E5%89%AF%E6%9C%AC%20%285%29/O1CN01ruQZwz1rUQBFTvXFY_%21%212210852105634.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:35.000+00:00",
      "updated": null,
      "id": 8,
      "goodsName": "家居家义乌商贸城小商品小百货",
      "price": 0.88,
      "goodsContent": "：包装种类: 其他颜色分类: 薄款 厚款适用对象: 其他礼品类别: 其他礼品",
      "goodsTag": "家居",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%8E%A8%E8%8D%90/1%20-%20%E5%89%AF%E6%9C%AC%20%287%29/O1CN014nTnRg26qbQWlLWvQ_%21%211712577713.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:36.000+00:00",
      "updated": null,
      "id": 10,
      "goodsName": "日本进口MUJIΕ家居厨房用品用具小百货",
      "price": 75,
      "goodsContent": "品牌: MUJIE/慕杰包装种类: 其他颜色分类: 轻奢蓝 轻奢白",
      "goodsTag": "家居",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%8E%A8%E8%8D%90/1%20-%20%E5%89%AF%E6%9C%AC%20%289%29/O1CN011bNU8X2GVfgP5OhjX_%21%212200567069021.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:20:13.000+00:00",
      "updated": null,
      "id": 44,
      "goodsName": "硅藻泥速干软地垫浴室卫生间门口吸水防滑脚垫子",
      "price": 76,
      "goodsContent": "品牌: 怡沁园材质: 硅藻泥图案: 卡通动漫风格: 简约现代产地: 中国大陆省份: 浙江省地市: 绍兴市尺寸: 40*60cm【加厚约4.0mm丨买一送一 ",
      "goodsTag": "宝藏好店",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%AE%9D%E8%97%8F%E5%A5%BD%E5%BA%97/1%20-%20%E5%89%AF%E6%9C%AC%20%283%29/O1CN01OCxSv51Rfi0naXaV0_%21%212917322139.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:53.000+00:00",
      "updated": null,
      "id": 24,
      "goodsName": "美式复古后背印花t恤男短袖潮牌百搭潮流打底衫外贸尾单男装上衣",
      "price": 149,
      "goodsContent": "品牌: rxvuq尺码: M L XL 2XL 3XL面料分类: 棉毛布花型图案: 字母/数字/文字领型: 圆领颜色: 白色 湖蓝色 藏青色 铁灰色袖型: 常规货号: 28519细分风格: 美式休闲基础风格: 青春流行品牌类型: 时尚潮牌适用季节: 夏季上市年份季节: 2023年夏季袖长: 短袖厚薄: 常规适用场景: 其他休闲版型: 修身款式细节: 印花服饰工艺: 水洗适用对象: 青年印花主题: 复古民族",
      "goodsTag": "潮流",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%BD%AE%E6%B5%81/1%20-%20%E5%89%AF%E6%9C%AC%20%283%29/O1CN01h2Q7Lm2I5E5RSAqfs_%21%212850899234.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:20:04.000+00:00",
      "updated": null,
      "id": 38,
      "goodsName": "日本ZD妈咪包新款时尚外出大容量多功能母婴包背包妈妈双肩包",
      "price": 336,
      "goodsContent": "品牌: ZIZI DONOHOE型号: 52785224适用年龄: 新生 3个月 6个月 12个月 18个月 2岁 9个月面料: 混纺风格: 休闲适用性别: 男女通用颜色分类: 绿色+送床垫 黑色+送床垫 灰色+送床垫 粉配灰升级款+送床垫 蓝色款升级款+送床垫",
      "goodsTag": "其它",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%85%B6%E5%AE%83/new%20-%20%E5%89%AF%E6%9C%AC%20%287%29/O1CN012YectV1bwmoF5KzrY_%21%21908003530.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:19:47.000+00:00",
      "updated": null,
      "id": 21,
      "goodsName": "F重磅230g夏季FORNINES刺绣FOR9插肩袖短袖T恤男上衣潮牌宽松半袖",
      "price": 68,
      "goodsContent": "品牌: 其它/other尺码: M L XL 2XL花型图案: 字母/数字/文字领型: 圆领颜色: 咖啡色 黑色 军绿色袖型: 插肩袖细分风格: 美式休闲基础风格: 青春流行适用季节: 夏季上市年份季节: 2023年夏季袖长: 短袖厚薄: 常规适用场景: 日常版型: 宽松型款式细节: 绣花服饰工艺: 刺绣适用对象: 青年印花主题: 文字思想",
      "goodsTag": "潮流",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%BD%AE%E6%B5%81/1/O1CN01Ann8ZI2AxiHpiJe9G_%21%21862068270.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-30T06:20:11.000+00:00",
      "updated": null,
      "id": 43,
      "goodsName": "益伟免手洗海绵拖把",
      "price": 295,
      "goodsContent": "产品名称: 益伟 yw-20品牌: 益伟型号: YW-20颜色分类: 28cm加厚海绵拖把+1棉头/天蓝【不锈钢杆】 28cm加厚海绵拖把+1棉头/卡其【不锈钢杆】",
      "goodsTag": "宝藏好店",
      "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%AE%9D%E8%97%8F%E5%A5%BD%E5%BA%97/1%20-%20%E5%89%AF%E6%9C%AC%20%282%29/O1CN011FDEHI1Rfi0nYMutz_%21%212917322139.jpg",
      "deleted": 0
    }
  ]
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» created|null|true|none||none|
|» updated|null|true|none||none|
|» id|integer|true|none||none|
|» goodsName|string|true|none||none|
|» price|number|true|none||none|
|» goodsContent|string|true|none|商品描述|none|
|» goodsTag|string|true|none|商品标签|none|
|» picture|string|true|none||none|

## GET 商品内容

GET /shopping/content/{goodsId}

提交笔记id和token，后端响应商品内容的业务对象，包含商品信息和评论信息

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|goodsId|path|integer| 是 ||none|
|Authorization|header|string| 否 ||token|

> 返回示例

> 成功

```json
{
  "goods": {
    "created": "2023-04-30T06:19:37.000+00:00",
    "updated": null,
    "id": 12,
    "goodsName": "创意家居日用小商品厨房用品",
    "price": 1.61,
    "goodsContent": "品牌: other/其他风格: 日式包装种类: 其他颜色分类: 长方形毛重: 4g适用节日: 春节是否可定制: 否",
    "goodsTag": "平价",
    "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%B9%B3%E4%BB%B7/new%20-%20%E5%89%AF%E6%9C%AC/QQ%E6%88%AA%E5%9B%BE20230425183202.png"
  },
  "goodsComment": [
    {
      "created": "2023-04-25T11:21:44.000+00:00",
      "updated": "2023-04-25T15:39:39.000+00:00",
      "id": 23,
      "userId": 2,
      "goodsId": 12,
      "comment": "好用好用",
      "username": "足球张雨绮",
      "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/6.jpg",
      "deleted": 0
    },
    {
      "created": "2023-04-25T11:41:09.000+00:00",
      "updated": "2023-04-25T15:39:39.000+00:00",
      "id": 24,
      "userId": 34,
      "goodsId": 12,
      "comment": "便宜并且耐用！下次还来",
      "username": "阿棒的觅食计划",
      "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/50.jpg",
      "deleted": 0
    }
  ]
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» goods|object|true|none||none|
|»» created|string|true|none||none|
|»» updated|null|true|none||none|
|»» id|integer|true|none||none|
|»» goodsName|string|true|none||none|
|»» price|number|true|none||none|
|»» goodsContent|string|true|none||none|
|»» goodsTag|string|true|none||none|
|»» picture|string|true|none||none|
|» goodsComment|[object]|true|none||none|
|»» created|string|true|none||none|
|»» updated|string|true|none||none|
|»» id|integer|true|none||none|
|»» userId|integer|true|none||none|
|»» goodsId|integer|true|none||none|
|»» comment|string|true|none||none|
|»» username|string|true|none||none|
|»» headphoto|string|true|none||none|
|»» deleted|integer|true|none||none|

## GET 搜索

GET /shopping/search

提交搜索内容和请求头token，后端根据商品名，商品介绍，和商品标签进行模糊查询

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|param|query|string| 是 ||none|
|Authorization|header|string| 否 ||token|

> 返回示例

> 成功

```json
[
  {
    "created": null,
    "updated": null,
    "id": 1,
    "goodsName": "创意家居生活用品",
    "price": 18.5,
    "goodsContent": "品牌: 小凡家居风格: 时尚包装种类:",
    "goodsTag": "推荐",
    "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%8E%A8%E8%8D%90/1/O1CN0160sQnm23r793wD3S8_%21%21267817308.jpg"
  },
  {
    "created": null,
    "updated": null,
    "id": 17,
    "goodsName": "大学生活住校生宿舍用品",
    "price": 11.19,
    "goodsContent": "包装种类: 其他颜色分类: 1个装【黑色】 1个装【白色】 2个装【黑色】",
    "goodsTag": "平价",
    "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%B9%B3%E4%BB%B7/new%20-%20%E5%89%AF%E6%9C%AC%20%286%29/O1CN019bhUR925IsqFVRR5j_%21%211660857504.jpg"
  },
  {
    "created": null,
    "updated": null,
    "id": 31,
    "goodsName": "居家居厨房卫生间用品家用大全生活用具小百货小物件各种清洁神器",
    "price": 36.5,
    "goodsContent": "材质: 树脂风格: 北欧风格安装方式: 免打孔颜色分类: 薰衣草紫1包30片 薰衣草紫2包60片 薰衣草紫3包90片 薰衣草紫5包150片 薰衣草紫10包300片 海洋蓝1包30片 海洋蓝2包60片 海洋蓝3包90片 海洋蓝5包150片 海洋蓝10包300片层数: 1层是否手工: 否",
    "goodsTag": "其它",
    "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%85%B6%E5%AE%83/new/O1CN013UlTrR21tHrUNTpuB_%21%212375307042.jpg"
  },
  {
    "created": null,
    "updated": null,
    "id": 32,
    "goodsName": "厨房用品家用大全生活用具小百货厨具小物件家居各种居家除锈神器",
    "price": 23.8,
    "goodsContent": "包装种类: 简装颜色分类: 小瓶装【4瓶】共400ml 小瓶装【2瓶】共200ml 小瓶装【1瓶】100ml【试用装】 大瓶装【1瓶】350ml【热销装】 大瓶装【2瓶】350ml【实惠装】适用对象: 其他礼品类别: 其他礼品",
    "goodsTag": "其它",
    "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%85%B6%E5%AE%83/new%20-%20%E5%89%AF%E6%9C%AC/O1CN016aQO1G1PcqCYVOOM0_%21%213452661862.jpg"
  },
  {
    "created": null,
    "updated": null,
    "id": 33,
    "goodsName": "家居家用小东西居家生活日用品家庭厨房卫生间用品用具小百货大全",
    "price": 13.66,
    "goodsContent": "品牌: other/其他包装种类: 简装颜色分类: S码100只（TPE韧性强加厚） M码100只（TPE韧性强加厚） L码100只（TPE韧性强加厚） S码200只（TPE韧性强加厚） M码200只（TPE韧性强加厚） L码200只（TPE韧性强加厚）适用对象: 其他礼品类别: 其他礼品 创意类礼品",
    "goodsTag": "其它",
    "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%85%B6%E5%AE%83/new%20-%20%E5%89%AF%E6%9C%AC%20%282%29/O1CN01ZUcoXp1dYAk1CN2RE_%21%212182353747.jpg"
  }
]
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» id|integer|true|none||none|
|» goodsName|string|true|none||none|
|» price|number|true|none||none|
|» goodsContent|string|true|none|商品介绍|none|
|» goodsTag|string|true|none|商品标签|none|
|» picture|string|true|none||none|

## GET 商品内容页面直接结算

GET /

> 返回示例

> 200 Response

```json
{}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

# 购物车

## POST 添加商品到购物车

POST /shoppingCart/add/{goodsId}

提交商品id和商品数量，后端进行处理并保存到购物车表

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|goodsId|path|string| 是 ||none|
|count|query|integer| 否 ||商品数量|
|Authorization|header|string| 否 ||token|

> 返回示例

> 成功

```json
"保存成功"
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

## POST 增加购物车商品数量

POST /shoppingCart/addCount/{goodsId}

在购物车中提交路径参数goodsId，每提交一次，后端将购物车表的商品数量加1，商品金额自动计算增加

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|goodsId|path|string| 是 ||none|
|Authorization|header|string| 否 ||token|

> 返回示例

> 成功

```json
"商品数量加1"
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

## POST 减少购物车商品数量

POST /shoppingCart/reduceCount/{goodsId}

在购物车中提交路径参数goodsId，每提交一次，后端将购物车表的商品数量减1，商品金额自动计算减少，减少到0时自动删除了购物车表中的商品信息

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|goodsId|path|integer| 是 ||none|
|Authorization|header|string| 是 ||token|

> 返回示例

> 成功

```json
"商品数量减1"
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

## PUT 删除购物车商品

PUT /shoppingCart/remove/{goodsId}

提交路径参数goodsId和请求头，后端将购物车表的deleted修改为1表示删除

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|goodsId|path|integer| 是 ||none|
|Authorization|header|string| 否 ||token|

> 返回示例

> 成功

```json
"删除成功"
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

## GET 所有购物车商品信息

GET /shoppingCart

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|Authorization|header|string| 是 ||token|

> 返回示例

> 成功

```json
[
  {
    "created": "2023-04-29T14:47:35.000+00:00",
    "updated": "2023-04-29T16:36:10.000+00:00",
    "id": 8,
    "userId": 1,
    "goodsId": 1,
    "goodsName": "创意家居生活用品",
    "price": 18.5,
    "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%8E%A8%E8%8D%90/1/O1CN0160sQnm23r793wD3S8_%21%21267817308.jpg",
    "count": 1,
    "amount": 18.5,
    "deleted": 0
  },
  {
    "created": "2023-04-29T14:47:39.000+00:00",
    "updated": "2023-04-29T14:49:34.000+00:00",
    "id": 9,
    "userId": 1,
    "goodsId": 2,
    "goodsName": "德古德训鞋",
    "price": 200,
    "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%8E%A8%E8%8D%90/1%20-%20%E5%89%AF%E6%9C%AC/O1CN01NVGvsc2AORhBr9xI0_%21%21127138193.jpg",
    "count": 4,
    "amount": 800,
    "deleted": 0
  },
  {
    "created": "2023-04-29T14:48:05.000+00:00",
    "updated": null,
    "id": 10,
    "userId": 1,
    "goodsId": 5,
    "goodsName": "冬季真皮马丁靴男切尔西靴子",
    "price": 583,
    "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%8E%A8%E8%8D%90/1%20-%20%E5%89%AF%E6%9C%AC%20%284%29/O1CN01p46qH51OA9mG1lHA6_%21%212259221664.jpg",
    "count": 2,
    "amount": 1166,
    "deleted": 0
  },
  {
    "created": "2023-04-29T14:48:09.000+00:00",
    "updated": null,
    "id": 11,
    "userId": 1,
    "goodsId": 10,
    "goodsName": "日本进口MUJIΕ家居厨房用品用具小百货",
    "price": 75,
    "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%8E%A8%E8%8D%90/1%20-%20%E5%89%AF%E6%9C%AC%20%289%29/O1CN011bNU8X2GVfgP5OhjX_%21%212200567069021.jpg",
    "count": 2,
    "amount": 150,
    "deleted": 0
  },
  {
    "created": "2023-04-29T14:48:22.000+00:00",
    "updated": null,
    "id": 12,
    "userId": 1,
    "goodsId": 11,
    "goodsName": "家居用品用具小百货",
    "price": 9.8,
    "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%B9%B3%E4%BB%B7/new/O1CN0109ZFuV25IshaJHuTL_%21%211660857504.jpg",
    "count": 1,
    "amount": 9.8,
    "deleted": 0
  },
  {
    "created": "2023-04-29T14:50:12.000+00:00",
    "updated": null,
    "id": 13,
    "userId": 1,
    "goodsId": 12,
    "goodsName": "创意家居日用小商品厨房用品",
    "price": 1.61,
    "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E5%B9%B3%E4%BB%B7/new%20-%20%E5%89%AF%E6%9C%AC/QQ%E6%88%AA%E5%9B%BE20230425183202.png",
    "count": 2,
    "amount": 3.22,
    "deleted": 0
  }
]
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» created|string|true|none||none|
|» updated|string¦null|true|none||none|
|» id|integer|true|none||none|
|» userId|integer|true|none||none|
|» goodsId|integer|true|none||none|
|» goodsName|string|true|none||none|
|» price|number|true|none||none|
|» picture|string|true|none||none|
|» count|integer|true|none|数量|none|
|» amount|number|true|none|金额|none|
|» deleted|integer|true|none||none|

## POST 购物车结算

POST /shoppingCart/settlement

购物车结算商品,结算时，提交要结算的商品Id列表，后端进行处理将这些商品添加到订单表，并计算返利总金额，同时扣除用户余额，增加用户待返金额

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|goodsIdList|query|array[string]| 是 ||要结算的商品id|
|Authorization|header|string| 否 ||token|

> 返回示例

> 200 Response

```json
{}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

# 订单

## GET 订单首页面

GET /order

订单首页面的所有信息

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|Authorization|header|string| 是 ||token|

> 返回示例

> 成功

```json
[
  {
    "created": "2023-04-30T06:22:48.000+00:00",
    "updated": null,
    "id": 10,
    "goodsId": 1,
    "userId": 1,
    "goodsName": "创意家居生活用品",
    "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%8E%A8%E8%8D%90/1/O1CN0160sQnm23r793wD3S8_%21%21267817308.jpg",
    "count": 1,
    "amount": 18.5,
    "deleted": 0
  },
  {
    "created": "2023-04-30T06:22:48.000+00:00",
    "updated": null,
    "id": 11,
    "goodsId": 2,
    "userId": 1,
    "goodsName": "德古德训鞋",
    "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%8E%A8%E8%8D%90/1%20-%20%E5%89%AF%E6%9C%AC/O1CN01NVGvsc2AORhBr9xI0_%21%21127138193.jpg",
    "count": 4,
    "amount": 800,
    "deleted": 0
  },
  {
    "created": "2023-04-30T06:22:48.000+00:00",
    "updated": null,
    "id": 12,
    "goodsId": 5,
    "userId": 1,
    "goodsName": "冬季真皮马丁靴男切尔西靴子",
    "picture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%95%86%E5%93%81/%E6%8E%A8%E8%8D%90/1%20-%20%E5%89%AF%E6%9C%AC%20%284%29/O1CN01p46qH51OA9mG1lHA6_%21%212259221664.jpg",
    "count": 2,
    "amount": 1166,
    "deleted": 0
  }
]
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

## POST 对订单中的商品进行评论

POST /order/comment/{goodsId}

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|goodsId|path|integer| 是 ||none|
|comment|query|string| 否 ||评论|
|Authorization|header|string| 否 ||none|

> 返回示例

> 200 Response

```json
{}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

# 个人资料

## GET 获取个人资料

GET /userInfo

获取当前用户的个人信息

> Body 请求参数

```json
null
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|Authorization|header|string| 是 ||tokem|
|body|body|null| 否 ||none|

> 返回示例

> 成功

```json
{
  "created": "2023-04-24T12:22:55.000+00:00",
  "updated": "2023-04-24T12:23:00.000+00:00",
  "id": 1,
  "username": "xm",
  "password": "123456",
  "headphoto": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E5%A4%B4%E5%83%8F/%E7%94%A8%E6%88%B7%E5%A4%B4%E5%83%8F/5.jpg",
  "gender": 1,
  "age": 22,
  "introduction": "暂无"
}
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» id|integer|true|none||none|
|» username|string|true|none||none|
|» password|string|true|none||none|
|» headphoto|string|true|none||none|
|» gender|integer|true|none||none|
|» age|integer|true|none||none|
|» introduction|string|true|none|简介|none|

## PUT 修改个人资料

PUT /userInfo/update

修改个人资料内容并提交参数

> Body 请求参数

```json
{
  "headphoto": "http://dummyimage.com/400x400",
  "username": "丁静",
  "introduction": "proident",
  "password": "Duis",
  "gender": 49,
  "age": 88
}
```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|Authorization|header|string| 是 ||token|
|body|body|object| 否 ||none|
|» headphoto|body|string| 是 | 头像|none|
|» username|body|string| 是 | 用户名|none|
|» password|body|string| 是 ||none|
|» gender|body|integer| 是 ||男1，女0|
|» age|body|integer| 是 ||none|
|» introduction|body|string| 是 | 个人简介|none|
|» phone|body|string| 是 ||none|

> 返回示例

> 成功

```json
"更新成功"
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

## GET 点赞信息

GET /userInfo/praise

当前登录用户的点赞笔记列表

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|Authorization|header|string| 是 ||token|

> 返回示例

> 成功

```json
[
  {
    "created": "2023-04-25T12:14:30.000+00:00",
    "updated": "2023-04-29T03:49:38.000+00:00",
    "id": 1,
    "userId": 1,
    "username": "xm",
    "title": "趁天还没热再来叠穿下",
    "content": "不然就来不及了",
    "tag": "推荐",
    "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%8E%A8%E8%8D%90/%E8%A7%86%E9%A2%91/1/%E5%B0%81%E9%9D%A2.png",
    "praisenum": 34244,
    "deleted": 0
  },
  {
    "created": "2023-04-25T12:14:30.000+00:00",
    "updated": "2023-04-29T03:45:09.000+00:00",
    "id": 2,
    "userId": 1,
    "username": "xm",
    "title": "巴黎世家特卖会",
    "content": "开心看看买了啥",
    "tag": "推荐",
    "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%8E%A8%E8%8D%90/%E8%A7%86%E9%A2%91/2/%E5%B0%81%E9%9D%A2.png",
    "praisenum": 1423,
    "deleted": 0
  },
  {
    "created": "2023-04-25T12:14:30.000+00:00",
    "updated": "2023-04-29T03:38:18.000+00:00",
    "id": 3,
    "userId": 2,
    "username": "足球张雨绮",
    "title": "贴地斩练习",
    "content": "新手足球练习正脚背，就要反复用30.40%的力量重复刻意的练习，慢慢你会拥有自己的射门风格",
    "tag": "推荐",
    "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%8E%A8%E8%8D%90/%E8%A7%86%E9%A2%91/3/%E5%B0%81%E9%9D%A2.png",
    "praisenum": 432,
    "deleted": 0
  }
]
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» created|string|true|none||none|
|» updated|string|true|none||none|
|» id|integer|true|none||none|
|» userId|integer|true|none||none|
|» username|string|true|none||none|
|» title|string|true|none|标题|none|
|» content|string|true|none|笔记内容|none|
|» tag|string|true|none|标签|none|
|» surfacePicture|string|true|none|封面图片|none|
|» praisenum|integer|true|none|点赞数|none|
|» deleted|integer|true|none||none|

## GET 收藏信息

GET /userInfo/collection

当前登录用户收藏笔记列表

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|Authorization|header|string| 是 ||token|

> 返回示例

> 成功

```json
[
  {
    "created": "2023-04-25T12:14:30.000+00:00",
    "updated": "2023-04-25T12:14:30.000+00:00",
    "id": 6,
    "userId": 5,
    "username": "安仔",
    "title": "一个男生挚爱的6瓶香水",
    "content": "分享春夏喜欢的6支香水，都是偏清爽的气味，口碑和市场接受度都蛮高的。个人觉得还蛮适合春夏的，基本男女都可，也都是之前都陆续分享过的",
    "tag": "推荐",
    "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%8E%A8%E8%8D%90/%E5%9B%BE%E7%89%87/6/4aee29f3fedda7ba36e9ab9115e96af.png",
    "praisenum": 456,
    "deleted": 0
  },
  {
    "created": "2023-04-25T12:14:30.000+00:00",
    "updated": "2023-04-25T12:14:30.000+00:00",
    "id": 7,
    "userId": 6,
    "username": "Jerry",
    "title": "看电影",
    "content": "希望我和樱木的伤快快好哈哈哈哈",
    "tag": "推荐",
    "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%8E%A8%E8%8D%90/%E5%9B%BE%E7%89%87/6/270ca884eb1950ec1a652ca3765ba4f.png",
    "praisenum": 874,
    "deleted": 0
  },
  {
    "created": "2023-04-25T12:14:30.000+00:00",
    "updated": "2023-04-25T12:14:30.000+00:00",
    "id": 8,
    "userId": 7,
    "username": "泡芙味的女孩子",
    "title": "独一无二属于自己的小螃蟹",
    "content": "肉蟹煲",
    "tag": "推荐",
    "surfacePicture": "https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/%E5%B0%8F%E7%BA%A2%E4%B9%A6/%E7%AC%94%E8%AE%B0/%E6%8E%A8%E8%8D%90/%E5%9B%BE%E7%89%87/5/c4287c1f3ac5d8e6054cf48c7c824f5.png",
    "praisenum": 3456,
    "deleted": 0
  }
]
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» created|string|true|none||none|
|» updated|string|true|none||none|
|» id|integer|true|none||none|
|» userId|integer|true|none||none|
|» username|string|true|none||none|
|» title|string|true|none|标题|none|
|» content|string|true|none|笔记内容|none|
|» tag|string|true|none|标签|none|
|» surfacePicture|string|true|none|封面|none|
|» praisenum|integer|true|none|点赞数|none|
|» deleted|integer|true|none||none|

## POST 更新头像

POST /userInfo/headphoto

提交头像，后端将文件解析上传到阿里云并返回图片的URL地址

> Body 请求参数

```yaml
headphoto: string

```

### 请求参数

|名称|位置|类型|必选|中文名|说明|
|---|---|---|---|---|---|
|Authorization|header|string| 是 ||token|
|body|body|object| 否 ||none|
|» headphoto|body|string(binary)| 是 ||none|

> 返回示例

> 成功

```json
"https://tanhua-zxm.oss-cn-hangzhou.aliyuncs.com/2023/04/30/f535955c-e541-429e-b588-5a1184f72389.png"
```

### 返回结果

|状态码|状态码含义|说明|数据模型|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### 返回数据结构

状态码 **200**

|名称|类型|必选|约束|中文名|说明|
|---|---|---|---|---|---|
|» headphotoUrl|string|true|none|用户头像url|none|

# 数据模型

