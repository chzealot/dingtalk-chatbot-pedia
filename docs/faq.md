## 目前 Stream 模式支持哪些数据回调？更多需求怎么接入？

1. 目前 Stream 模式支持这三种类型的数据回调
    1. 事件订阅，[点此链接](https://open.dingtalk.com/document/orgapp/stream)
    2. 机器人收消息，[点此链接](https://open.dingtalk.com/document/orgapp/the-creation-and-installation-of-the-application-robot-in-the)
    3. 互动卡片回调，[点此链接](https://open.dingtalk.com/document/orgapp/create-and-deliver-cards)
2. 对于更多场景，如果有强烈需求，可以加入 “钉钉开放平台Stream模式共创群” ，联系群主沟通共创，实现新的场景支持。

## 协议就是websocket吗？可以用原生的c#自己实现吗？有什么特别需要注意的地方

我们乐于接受开发者贡献，为此已经开放了 Stream 协议的文档：https://open.dingtalk.com/document/direction/stream-mode-protocol-access-description。

欢迎开发者联系平台，参与 SDK 的开发和完善。

## 请问可以编辑已发送的消息吗？

这个属于打字机模式，还在设计中

## 请问要显示图片信息，应该用哪个消息格式？我用 markdown，但是渲染不出图片

我把这段内容复制出来在markdown里是可以显示的
![image](https://github.com/chzealot/dingtalk-developerpedia/assets/22822/2919e6b5-3c68-4cf3-9d8a-88f2bd363c41)
，discord 被 q了啊。搞个反代，或者别的方式来实现

## stream到底在哪里打开啊

![image](https://github.com/chzealot/dingtalk-developerpedia/assets/22822/bba95479-5432-445e-8dcf-564ab09ccc45)

![image](https://github.com/chzealot/dingtalk-developerpedia/assets/22822/1814797e-b6c2-496b-a5bf-6c36e6b8eb7b)

## 我以前建的机器人是在机器人那里建的，现在要迁移到钉钉用里面吗？

建议还是在钉钉应用内创建机器人，后面最外层的机器人入口会下线的

## Stream模式理解不了，不用推送的吗

这个Stream模式的文档说明，https://open.dingtalk.com/document/resourcedownload/Introduction-to-stream-mode ，主要是免去开发者申请公网域名，IP，服务器的成本。通过可信的方式与钉钉建立连接来接收回调消息

## 打字机模式是像gpt那样流式输出结果吗

是

## 我们玩过交互式卡片，他说调好都用了几天，难度很大

这个卡片能力支持发送卡片json数据，需要的话，可以试用一下，有问题可以随时在共创群中反馈：

卡片入口：https://card.dingtalk.com/card-builder （登录后就能查看）
开发者文档：https://open.dingtalk.com/document/orgapp/robots-send-interactive-cards

采用普通版卡片的话，cardTemplateId是固定的值。（StandardCard）

## 我用 dingtalk-stream-sdk-nodejs 来测试 stream，示例代码运行一小会儿就报错 MidwayUtilHttpClientTimeoutError Request Timeout， 这是啥情况呢？


我把node从20降到了18，这回撑得久了一些，最后还是报错 connect ETIMEDOUT 106.11.210.212:443

你这个就是接口超时了吧，sdk明天会优化一版，之前请求依赖midway，现在去掉了

## http机器人的接口什么时候会下线不让用？

不会下线。

## 目前建立的监听连接只能持续30分钟，然后需要重启，大家是怎么避免重启期间监听不到消息呢

sdk会自动处理断线重连的，不需要重启，中间无连接的时间非常短，如果对可用性要求比较高，可以启动多个实例

## 我的stream的机器人应用换了一个服务器部署，现在报鉴权错误，会有这方面的风控吗？

平台没有特殊的限制。
不过你可以看看 开发者后台(https://open-dev.dingtalk.com ) - 选择应用- 开发管理，查看服务器出口IP这里，是不是以前配置了出口IP白名单

如果服务端出口IP这里配置没有问题的话，可以把接口调用出错的详细信息发一下（应用ID、名称、ClientID，出错的时间点、错误信息、RequestID）

## 目前机器人发送消息的返回值只有errorcode，未来会加上msgId吗

需要msgId有什么用途吗？回复给机器人的消息数据结构相较于直接@，只多了一个originalmsgId，如果要把这个信息用起来，需要机器人发送消息的msgId，这样机器人可以有记忆性

这个问题我先记一下，后面和相关的开发咨询一下看看是否可以优化

## 请问stream模式下，是连的钉钉的哪个域名？部署的服务器外网访问受限，需要按域名 开通外网访问权限

api.dingtalk.com   wss-open-connection.dingtalk.com

## 请问 stream 模式可以主动发消息吗

也是可以的，用钉钉的接口发就好了
https://api.dingtalk.com/v1.0/robot/oToMessages/batchSend
这个接口

## 下的dingtalk-stream-sdk-python的项目 起服务正常。 在后台验证了连接通道是成功的。
在群里拉入机器人 并发消息 @机器人，服务端没收到任何请求
请问可能是什么原因？

控制台有打印出启动日志吗？有启动日志。 后来解决了，h5微应用有这个问题，换成小程序就没问题了

## 目前如果点机器人发的消息进行回复，回复的消息如果含图片，图片会单独视为一条消息，这条单独的消息没有@机器人，机器人就收不到。如果直接@机器人发送RichText又可以视为一个整体。这个有解决办法吗

这个暂时没有

## 钉钉互动卡片目前有参数支持修改这个地方展示内容么

![image](https://github.com/chzealot/dingtalk-developerpedia/assets/22822/80cb0273-702d-4f8e-8f72-347ab752950a)

## 还想再请教下，我想发个markdown，是个图片，应该怎么发？我用reply_markdown_card有这个报错

2023-07-03 16:19:40,895 root     INFO     012608 2023-01-01 2023-07-01 = ./FD/IMG/012608_2023-01-01_2023-07-01_data.png [Run.py:56]
2023-07-03 16:19:41,135 dingtalk_stream.handler ERROR    CardResponder.send_card failed, create card instance failed, error=403 Client Error: Forbidden for url: https://api.dingtalk.com/v1.0/card/instances [card_replier.py:80]

用reply_markdown也不行

应用申请一下机器人发消息权限

我申请了，要等段时间么？
![image](https://github.com/chzealot/dingtalk-developerpedia/assets/22822/40fdb4be-f155-4a10-96c3-a17209f70c27)

卡片的权限也申请一下

## 想验证人员新增，请问怎么调试数据啊？


## 请问在Go中，我给机器人发送一个文件，我该怎么才能拿到这个downloadCode

https://open.dingtalk.com/document/orgapp/download-the-file-content-of-the-robot-receiving-message

## 问一下，我的这个文字怎么设置每行显示字数呀，

目前遵守设计上统一规范，暂不支持。

短期内建议用卡片形式来展示。相比纯文本有更丰富的展示形态。卡片可以是markdown，也可以是交互式卡片。(https://card.dingtalk.com/card-builder )


## 创建的 应用机器人 怎么设置 单独聊天？ 

机器人 在群上设置 没有问题，想单独搜索不了，和它单独对话？

## 钉钉机器人， 目前只支持 一个程序连接？  支持多个程序连接吗？

可以的，但是同一个业务只能部署在同一集群，比如机器人的话后端服务只能是一个应用

## 你们好,就我在使用时会出现我at了机器人但是代码这没有收到消息,并且没有重新连接的情况等其他消息,所以我想问问有没有方式能一段时间有一次通讯来测试它的链接是否是好的

推送连接是有心跳保活的，如果收不到消息的话可能是此应用启动了多个实例，如果后续遇到类似的问题，可以把appkey提供一下，平台侧排查分析。

## 创建+投放模式使用的cardTemplateId是不能用'Standard',必须用开发者后台创建好的吗

## 使用stream模式监听审批事件，同一个事件会出现3次，这个是正常的吗？

有可能的，如果钉钉服务端推送超时之前没收到ack，就会触发重推。超时原因有很多种，网络异常、服务出现block等原因都会导致不能及时返回ack触发超时重推

## Arguments: (SSLCertVerificationError(1, '[SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed: unable to get local issuer certificate (_ssl.c:1129)'),)

![image](https://github.com/chzealot/dingtalk-developerpedia/assets/22822/1bf6c6c5-5a2f-4028-be69-9e6a5f73c6d3)

麻烦看下，这个问题怎么解决，之前发现一些python版本不兼容dingtalk-stream, 后来发现3.9.14可以，mac本地可以，线上报一个认证的错

之前我们也遇到一些，是电脑环境有问题，跟 dingtalk-stream 没有关系，可以试试不用stream，直接用requests库发起请求看看有没有问题

https://pypi.org/project/requests/

![image](https://github.com/chzealot/dingtalk-developerpedia/assets/22822/0b631dac-baac-4cdd-adb1-6ab7445e8ae4)



