# tgbot-heroku

Deploy tgbot to heroku in one key, you can use it as your telegram private notifier.

### Heroku 是一个支持多种编程语言的云平台即服务，tgbot-heroku 则是可部署在 Heroku 平台的`telegram个人通知机器人接口`。

#### 下面的部署方法，前提是你已经拥有一个heroku账号。

1.注册 Heroku 帐号

Heroku 提供免费账号，部分介绍如下：

512 MB RAM per dyno

Free apps sleep automatically after 30 mins of inactivity to conserve your dyno hours

Free apps wake automatically when a web request is received

https://devcenter.heroku.com/articles/limits

https://devcenter.heroku.com/articles/free-dyno-hours#usage

注册地址：https://signup.heroku.com/ （注册和部署过程可能需要梯子）


## 部署方法

本方法为快速部署。

一、在heroku上的部署

1、登陆https://dashboard.heroku.com/login

2、登陆好后，点击

[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy?template=https://github.com/snail007/tgbot-heroku)

3、执行以下三个步骤，见下图：

（1）输入App name.例如`mygblog`

（2）Choose a region:选择一个.例如United States

（3）点击：Deploy app。

<img src="https://cdn.jsdelivr.net/gh/snail007/gblog-heroku/doc/1.png" width="500px" height="auto">

4、等待一会就会完成，这就完成了机器人接口部署。

## 安全建议，设置接口认证

点击Manage App，可以设置博客空间，比如下面的修改路径。

默认调用接口不需要认证，为了安全，可以设置一个系统变量，设置认证信息，可以在heroku的Setting里面的Config Vars配置一个变量：`TG_AUTH=foo`，然后重启你的app即可。

<img src="https://cdn.jsdelivr.net/gh/snail007/gblog-heroku/doc/4.png" width="500px" height="auto">

<img src="https://cdn.jsdelivr.net/gh/snail007/gblog-heroku/doc/5.png" width="500px" height="auto">

<img src="https://cdn.jsdelivr.net/gh/snail007/gblog-heroku/doc/6.png" width="500px" height="auto">

## 接口说明

比如你的heroku地址是：`https://foo.herokuapp.com/`

接口请求路径就是:`https://foo.herokuapp.com/send`

请求方式：`post`，`get`均可以

请求参数：

`msg`: 要发送的文本消息。

`uid`: 消息接受人的用户ID，telegram里面加机器人`@JsonDumpBot`聊天可以的到你的用户ID。

`token`: telegram机器人的token,telegram里面加`@BotFather`可以创建你的机器人并获取token。

`auth`: 上面设置的TG_AUTH，如果没有设置，可以不传递这个参数。

## 传任意文件，图片，视频

只需要发送enctype="multipart/form-data"的普通表单即可，文件的field名称随便写，
其它msg，uid，token，auth字段，放在表单里面或url的参数里面均可以。

## 提示

如果想要`uid`可以收到机器人消息，这个`uid`必须先加机器人，和机器人`开始`聊天，机器人才能给这个`uid`发送消息。
