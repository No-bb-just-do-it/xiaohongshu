# 小红书通信5.26版本协议签名

## 简介

通过小红书通信协议实现自动化爬取小红书文章，点赞，评论等功能

小红书通信协议支持 iOS 5.26（最新）版本协议，最低兼容版本及Android支持请自测，之后会提供设备信息生成功能，方便调用协议

提供生成签名服务，方便对小红书通信协议进行签名。签名参数: `sign`

项目持续更新中...

## 使用说明
通过调用API加签服务来完成获取新的设备信息及协议签名。

实现过程:
1. 通过访问 `https://api.appsign.vip:2688/token/xiaohongshu` 获取小红书的最新版本加签token，token有效期为60分钟，token失效前请不要重复获取token
2. 自己生成设备信息。之后会开放设备信息生成接口
3. 有了设备信息和加签Token， 需要通过参数构造加签字符串，调用 `https://api.appsign.vip:2688/sign` 完成参数的加签

---

> token有效期为一个小时，支持多线程进行加签，token失效之前无需重复获取

## API参数
1. 获取小红书加签Token
```
https://api.appsign.vip:2688/token/xiaohongshu  # 默认版本为最新
https://api.appsign.vip:2688/token/xiaohongshu/version/5.26
```
```
{
    "token":"5826aa5b56614ea798ca42d767170e74",
    "success":true
}
```

2. 参数加签
```
https://api.appsign.vip:2688/sign
{
    "token":"TOKEN",
    "query":"通过参数生成的加签字符串"      # 务必带上deviceId参数
}
```
```
{
    "data":{
        "sign":"0041******cf******",
    },
    "success":true
}
```

> 提醒： 如果是post请求，post请求参数和get请求参数使用'&'符号链接成统一参数，传递到`query`参数，加签参数中必须存在`deviceId`参数

## APP版本信息
...

## 实例
* [ ] 爬取首页信息

## 更新
* 2018.09.28 更新支持最新版5.26协议，最低支持版本请自测
