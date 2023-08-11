## 钉钉聊天机器人概述

钉钉聊天机器人分为两类

1. 群 Webhook 机器人，在钉钉客户端中，群设置中创建的自定义 webhook 机器人
2. 应用机器人，在[开发者后台](https://open-dev.dingtalk.com)中，创建应用，在应用中开启的机器人

## 优缺点如下

### 群 Webhook 机器人

优点

1. 创建方便，普通用户即可创建

缺点

1. 仅支持 incoming 消息，不支持 outgoing。（受限于合规要求，机器人必须有认证过的实体才能创建，并且有明确的认证过的开发者组织）
2. 发消息能力受限，不支持互动卡片等形式的消息发送
3. API能力受限，不支持调用 OpenAPI，例如发送图片时必须使用外部图床，不能通过钉钉 OpenAPI 来上传图片

### 应用机器人

优点

这种方式创建的机器人归属于一个钉钉平台的应用，因此具备应用开发的丰富能力。

1. 完整的收发消息能力，既能接收 incoming 消息，支持 outgoing 的消息接收
2. 支持 [Stream Mode](https://open.dingtalk.com/document/resourcedownload/Introduction-to-stream-mode)，开发过程极其简单
3. 支持以应用身份调用全部的 OpenAPI，例如调用上传图片文件到钉钉平台，获得MediaID后用于Markdown消息中图片展示（钉钉markdown消息中，支持在图片url地方填写MediaID）
4. 支持发送[互动卡片消息](https://open.dingtalk.com/document/orgapp/overview-card)，更丰富的消息交互能力

缺点

1. 相比群 Webhook 机器人，创建复杂度较高。需要应用子管理员身份，进入[开发者后台](https://open-dev.dingtalk.com)创建

备注：相关体验正在通过升级基础架构解决中

1. 权限：优化后普通用户也可以创建应用，不需要申请应用开发子管理员
2. 入口：优化后可以在钉钉客户端内创建机器人应用，不需要进入开发者后台



