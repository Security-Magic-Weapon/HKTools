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

## 学习参考项目

https://gitee.com/xwintop/xJavaFxTool

----

## 知识星球

本星球会**每日更新**全网优秀安全资源包括但不限于：**安全工具**、**安全脚本**、**安全学习资料**、**安全商业产品的破解版**等，资源方向均与安全各领域相关。

本星球建有运营微信群可及时在群内反馈和互动（索取安全资源），并在运营微信群内拥有Bot机器人用于通知星球最新动态方便各位星友不错过任何优秀动态。

本星球会针对安全资源进行**严格的分类**，方便各位星友可以**快速定位**自己所需的资源，及给各位星友带来更好的**阅读体验**。

本星球会**每月**进行一次**优质资源统计**，会根据本阅读点赞/评论/阅读/下载最多的资源进行排序方便大家更好的浏览。

并且本星球将会**每季度**进行一次**星友知识共享直播**，仅限本星球的星友参与，直播会邀请星球内的部分大佬或在外部邀请在某领域有所建设的大佬进行**免费的知识共享**，并且本星球的续费折扣是平台的最低**5折折扣**！

<img src=https://tva1.sinaimg.cn/large/006y8mN6gy1h6tocodn91j30ku0bggm5.jpg width=40% />
