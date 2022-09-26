## HKTools
一款辅助安全研发在日常工作中渗透测试、安全研究、安全开发等工作的工具！
**程序支持Yaml格式的http请求模版**

## 启动密码：

```
GMYTGMRTGMZDCNBQGIZ6PHEL42QLPZNNSDSYHD7IX6N6LCFW466JNZ5AQHSZHJXPXSAQ====
```

个人觉得不难，提示已经给到位了...

## 演示视频

[**BliBli点击观看**](https://www.bilibili.com/video/BV13N4y1K7eE)

## 漏洞模版

**漏洞模版采用yaml格式，文件名后缀也为yaml.**

### 基础语法

1. 漏洞名称，必须为英文.

```yaml
name: poc-yaml-thinkphp5023-method-rce
```

1. 内置函数

```jsx
set:
  randomInt: 0,1
  md5: 'admin'
```

- randomInt：由英文逗号分隔，禁止存在空格，逗号左侧为最小数字，逗号右侧为最大数字，可以在`responsebody`、`body`、`path`{{md5}}处通过进行调用
- md5：必须由单引号或双引号闭合，可以在`responsebody`、`body`、`path`{{md5}}处通过进行调用
1. 发包配置

```yaml
rules:
  r1:
    method: "POST"
    path: "/index.php?s=captcha"
    headers:
      Content-Type: application/x-www-form-urlencoded
    body: "_method=__construct&filter[]=printf&method=GET&server[REQUEST_METHOD]={{md5}}&get[]=1"
    expression:
      responsestatus: 200
      responsebody: '{{md5}}'
  r2:
    method: "GET"
    path: "/{{md5}}"
    expression:
      responsestatus: 404
      responsebody: '{{md5}}'
```

- r1：自定义请求函数名，从上到下依次执行请求函数
- method：必须由单引号或双引号闭合，请求方式，当前支持POST、GET、PUT
- path：必须由单引号或双引号闭合，请求路径
- headers：可不写此项（直接删除，参考r2），一行一条，冒号左侧为键名，冒号右侧为键值
- body：必须由单引号或双引号闭合，可不写此项（直接删除，参考r2），在GET请求中不应填写
- responsestatus：不可存在单引号或双引号，必须填写，判断响应状态码
- responsebody：必须由单引号或双引号闭合，必须填写，在响应正文中查找指定字符串
1. 脚本信息

```yaml
info:
  author: Explang
  Homepage: https://github.com/ExpLangcn
  CodeLink:
    - https://github.com/vulhub/vulhub/tree/master/thinkphp/5.0.23-rce
```

- author：POC作者名称，不可为空，必须为英文
- Homepage：个人主页链接
- CodeLink：漏洞参考链接，一行一个

## 截图介绍

### 正则匹配

<img width="1089" alt="image" src="https://user-images.githubusercontent.com/52586866/191400721-ce0051c0-b1ac-4e74-9eb4-ac9f38c45890.png">

### 加密解密

<img width="1089" alt="image" src="https://user-images.githubusercontent.com/52586866/191400818-df75cd14-5759-4fa0-85ae-95a041502c0b.png">

### http调试

<img width="1089" alt="image" src="https://user-images.githubusercontent.com/52586866/191400866-7ae9f4dd-99a9-486f-accf-babd8b5f91cb.png">

<img width="1089" alt="image" src="https://user-images.githubusercontent.com/52586866/191400875-27e65394-4d6d-4b19-a639-ff2babd54044.png">

### http多个模版请求（支持批量请求多个模版，支持请求多次）

<img width="1089" alt="image" src="https://user-images.githubusercontent.com/52586866/191401034-e2d93d55-c363-4d83-b4c9-2f2404596b31.png">

----

## 知识星球

如同星球名字一样我是想做一个安全资源库，内容包括但不限于：安全工具/安全思路/技巧资料/学习资料，方向包括但不限于：WEB渗透/安全开发/内网渗透/免杀处理/零信任安全/云安全/工控安全/硬件安全/区块链安全等！

我会专注于分享一写我在做研发的时候遇到的一写比较有意思的点会将它们变成文档沉淀下来，以及我自己写的一些安全工具。

**星球拥有完整的运营体系可放心加入。**

加入星球共同学习提升自我，**我荒废的今日，正是昨日殒身之人祈求的明日！望诸君 共勉之.**

![星球优惠券](https://user-images.githubusercontent.com/52586866/191401470-0b2dd4a9-0549-4854-9a44-97be836a959a.png)
