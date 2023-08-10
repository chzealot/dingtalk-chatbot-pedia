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

python 的 依赖里面，尝试一下这个版本号组合：

```
requests==2.30.0
urllib3==1.26.15
```

高版本的 urllib3 对ssl校验策略也发生了一些变化

## 以前用http模式的是，如果用户的内容里面有"alter table" "insert into" 这类的内容，钉钉会过滤掉，现在stream模式没有过滤，请问以后也不会过滤了吧

近期不会，未来也会谨慎支持。这类waf误判率对开发者有一定的负面影响。
当时安全需求我们会持续关注，有相关想法可以随时跟我们交流 

## 你好问一下, stream 模式下 机器人不能获取 'msgtype' 为 'file' 格式的文件内容吗

这个需要使用open api来处理 https://open.dingtalk.com/document/orgapp/download-the-file-content-of-the-robot-receiving-message

## 但是发送端仍然只支持有限几种格式吗

![image](https://github.com/chzealot/dingtalk-developerpedia/assets/22822/01c4ad1d-580a-46ac-8121-28cb37d8d814)

还有哪些文件类型需求可以发出来我们评估一下 


## upload 文件到钉钉后, 获取的 mediaids 如何使用?
不能钉钉机器人没有接口可以直接回一个文件吗

回复文件这个需求，有业务需求的话，可以加我好友，作为共创客户先试点一下。跑顺畅后就全量开放出来。

## 你好，我原本H5应用里的机器人通过https可以收到消息的回调，但是前两天突然收不到了。用了dingtalk-stream的python版sdk，放入appkey和appsecret也没有用。这是为什么？

## 各位老师，现在Stream摸索支持C#吗，还是要等新的SDK

目前团队里面没有专业的C#开发，但是有开发者原因参与的哈，我们非常乐意和鼓励这种贡献：
1、通过测试后，我们可以提供官网渠道推荐和对贡献者的感谢
2、提供单独的SDK交流群，提升协作效率
3、提供协议文档（比较简单）。协议文档还在编写，近期会开放出来。如果有有人在GitHub上立项开发SDK的话，我们可以提前单独提供协议文档

## 阿里大佬们，想实现个钉钉自动回复的机器人，这个有参考样例么

群公告里有github项目可以参考。其他语言的我尽快更新到群公告里

## 有钉钉机器人@机器人的办法么?

当前不支持

## 请问哪位有自动问答机器人的Demo的？或者文档也行啊

## 服务端 Stream 的SDK有PHP版本吗？

暂时没有

## 有个问题需要请教一下大家 ，项目本地调试请求本地服务可以访问到，但是请求生产环境服务器请求失败， 控制台报错   
error: 19
errorMessage: "HTTP错误"
originalData: undefined

## 想请问下，stream模式下的python版本，有接收卡片按钮事件回调的使用例子吗？

## 最近是不是改成12小时重新建立一次websocket连接了，之前好像是半小时

## 想请问下，stream模式下的python版本，有接收卡片按钮事件回调的使用例子吗？

可以参考 https://open.dingtalk.com/document/isvapp/event-callback-card

我在python代码中注册了'/v1.0/card/instances/callback'这个事件监听，点击卡片的按钮。但是在websocket这，并未收到事件消息。

https://open.dingtalk.com/document/isvapp/interface-for-creating-a-card-instance 需要指定卡片回调模式 

## 现在是不是http回调的方式已经停用了？

很久没有做“停用”这种操作。
比较早期的时候，针对群设置中创建的自定义机器人关闭了outgoing能力。原因是很多群缺乏组织归属，法务合规上上风险较高，从合规上给关闭了。
但是，在开发者后台里，创建的应用机器人，是有明确的组织归属，一直都没有限制。HTTPS和Stream模式回调都是开放的。

## Arguments: (SSLCertVerificationError(1, '[SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed: unable to get local issuer certificate (_ssl.c:992)'),)

请问下，这个报错原因是为什么？

安全证书问题 发送请求时 忽略证书认证 我是临时怎么解决的 


## 现在golang创建审批有什么SDK是支持的吗，我看有些SDK最近更新都是两年前了

现在golang创建审批有什么SDK是支持的吗，我看有些SDK最近更新都是两年前了

![image](https://github.com/chzealot/dingtalk-developerpedia/assets/22822/0b3d4478-7071-44af-ad3a-bfe7ec697bfb)

## 怎么把群成员手机号导出了呢

1、通过会话管理接口，获取群成员列表（主要是获取用户ID）：https://open.dingtalk.com/document/orgapp/session-management-overview
2、通过通讯录接口，查询用户的手机号：https://open.dingtalk.com/document/orgapp/session-management-overview

注意，群成员接口、通讯录接口都需要在开发者后台申请权限，获得企业管理员同意后才能调用成功。手机号是敏感信息，需要单独申请手机号权限。
权限点申请文档：https://open.dingtalk.com/document/orgapp/add-api-permission

## 请问下卡片的按钮链接可以像下面的地址一样设置用系统浏览器打开吗？

![image](https://github.com/chzealot/dingtalk-developerpedia/assets/22822/4a120cd5-2460-4454-8771-03f0e351f4dd)

可以的。

在这里查看卡片使用：https://card.dingtalk.com/card-builder

## 请问下stream模式中，用户在群里@机器人后，机器人调用后端的服务，可能处理的时间比较久（比如需要处理10分钟以上）然后才会返回结果给钉钉机器人，在这种情况下机器人还会将结果发送给对应的人或者群里面吗？

## sessionWebhook 这个超时时间是多久？10分钟？

https://open.dingtalk.com/document/orgapp/the-application-robot-in-the-enterprise-sends-group-chat-messages

![image](https://github.com/chzealot/dingtalk-developerpedia/assets/22822/f4c64529-b315-499a-8824-2c45bc6ad59f)


这个时间通过参数返回的

## 怎么内网穿透

自己搭建的话，可以用：https://github.com/fatedier/frp
没有服务器的话，可以用：https://www.ngrok.cc/

安全提醒：内网穿透在数据安全上有重大风险，经常有企业因为内网穿透导致安全事故。强烈建议不要使用内网穿透，尤其是不要在公司网络、生产服务中使用。

我们也是考虑到这个因素，才设计出来 Stream 能力，避免了客户对内网穿透的依赖。

## 请问目前dingtalk-stream-sdk-python支持卡片回调吗？

支持的，接入方式和机器人类似，需要更换一个topic，参考文档卡片创建和 事件回调文档
 https://open.dingtalk.com/document/orgapp/interface-for-creating-a-card-instance
 https://open.dingtalk.com/document/orgapp/event-callback-card


 最新版 Python SDK 支持了卡片回调。
升级到 dingtalk-stream-v.0.9.1 就可以了： https://pypi.org/project/dingtalk-stream/ 
这里有示例代码： https://github.com/open-dingtalk/dingtalk-stream-sdk-python/blob/main/examples/cardcallback/cardcallback.py

## 机器人clientid clientsecret 是同一个，但是功能不一样，部署了不同的应用，这样是ok的吗？

订阅的topic不同就没关系

## 请问加解密类中的DingCallbackCrypto和DingTalkEncryptor有什么区别

没啥区别，DingTalkEncryptor.cs 是 C# 版本的DingCallbackCrypto

## 请教下, 卡片消息里的回调按钮的配置, 是可以配置回调地址的吧, 

![image](https://github.com/chzealot/dingtalk-developerpedia/assets/22822/abfe7a46-3202-484d-a5c6-eb587abc1b59)

示例里并没有, 如果要配的话应该怎么加

这个截图是互动卡片普通版，不支持回调。
需要回调的卡片参考这个文档：https://open.dingtalk.com/document/isvapp/register-card-callback-address （在这里注册的卡片回调可以通过请求参数选择 HTTP/Stream ）

## 请问一下，官方文档里JAVA的demo中引入了com.aliyun.tea的包，但是我引入了钉钉最新的sdk后并没有这个包

单独下载jar是不行的，会缺少其他依赖，建议maven管理依赖

## https://open.dingtalk.com/document/orgapp/create-and-deliver-cards
请问一下，如果是机器人单聊，如何通过这个接口让机器人给用户发卡片呢？

机器人投放参数貌似没有关联机器人编码

另外刚才调用了一次接口，报错信息如下：errorMsg': 'spaces of card is empty
![image](https://github.com/chzealot/dingtalk-developerpedia/assets/22822/5362b8d5-08a4-474f-a508-1036a7ef0a55)

![image](https://github.com/chzealot/dingtalk-developerpedia/assets/22822/39e04069-f8eb-4551-9896-2674edf535a4)


yuanhao：DeliverCardRequestImGroupOpenDeliverModel 这个model里面可以设置robotCode
这个错误是没有设置你需要投放的场域。

单聊不需要设置robotCode，只需要设置属性为IM_ROBOT，需要以应用里面的机器人发。

## 请问一下，互动卡片搭建时，如何设置按钮的大小，想把这两个按钮调小一点。

![image](https://github.com/chzealot/dingtalk-developerpedia/assets/22822/9eed9b4d-592a-4c70-a52a-7e9eece99d16)

这个改不了。

## 请问一下，我使用dingtalk-stream-sdk-python/examples/cardcallback/cardcallback.py这里的卡片回调代码，成功了，我这里只回传了一个字段，但是卡片中有3个数据字段，刚才试了一下，会把其他两个字段值置为空，这里有解决办法吗？

![image](https://github.com/chzealot/dingtalk-developerpedia/assets/22822/3a3971da-10f8-4a85-9319-f233ab22a89c)

示例中字段都可以去掉，按照自己的实际需求回传数据

卡片中设置了三个数据

![image](https://github.com/chzealot/dingtalk-developerpedia/assets/22822/f554ce40-8afb-469d-9280-cbc6851d7aa2)

https://open.dingtalk.com/document/orgapp/event-callback-card

![image](https://github.com/chzealot/dingtalk-developerpedia/assets/22822/191a6712-5f0f-4b1f-91fe-37eaaaa3c261)

，我只想更新do_feedback这个字段，其他字段保持不变，该怎么做？

你们的这个文档上说是会全量覆盖？



## 请问 stream python sdk 不支持card上按钮回调吗,  DingTalkStreamClient 看起来没有注册card回调的方法, register_callback_hanlder 这个看起来只接受普通的消息接收

![image](https://github.com/chzealot/dingtalk-developerpedia/assets/22822/4e2e31a1-1b91-4ce4-894c-af88ede5592c)

![image](https://github.com/chzealot/dingtalk-developerpedia/assets/22822/c9a57828-a7f8-4fb5-813b-3422e7aeba93)

![image](https://github.com/chzealot/dingtalk-developerpedia/assets/22822/0cb0a31b-8d14-4a5d-b85c-5c0640965a4a)

最新版 Python SDK 支持了卡片回调。
升级到 dingtalk-stream-v.0.9.1 就可以了： https://pypi.org/project/dingtalk-stream/ 
这里有示例代码： https://github.com/open-dingtalk/dingtalk-stream-sdk-python/blob/main/examples/cardcallback/cardcallback.py



## 那我给机器人发送卡片无论是私聊还是群聊，都依据conversationid来发送卡片？

![image](https://github.com/chzealot/dingtalk-developerpedia/assets/22822/43c5ac73-c58f-4926-a6e4-6aa7b6ff6ef8)

私聊用single这个，群聊用上面那个

![image](https://github.com/chzealot/dingtalk-developerpedia/assets/22822/2c1f14dd-7d00-4d26-97cc-dc69e4829781)

需要区分，单聊和群里可以参考这个代码，以及前面提供的文档链接。

## 请问下 发送钉钉互动卡片（高级版）这个接口发的卡片回调按钮，在stream模式下能监听到吗

可以的，发送卡片时候 callbackType 参数设置为 STREAM 即可
说明文档：https://open.dingtalk.com/document/orgapp/interface-for-creating-a-card-instance

## 请问机器人文本消息有字数限制吗？

目前这个限制没有对机器人做特殊处理，跟钉钉聊天消息一样，超过限制会转成文本文件。这个限制目前没有明确公开、承诺，也不保证未来不会变化，建议不要出现显著过长的文本，比如一个长篇小说、大段代码之类的。

## 请问下，启动测试案例，一直提供这个证书问题，请问如何处理呢

![image](https://github.com/chzealot/dingtalk-developerpedia/assets/22822/9a1e9216-9741-4d4b-b896-7a5c453ed9dc)

我mac也碰到过，找到对应路径，执行下就行

/Applications/Python 3.10/Install Certificates

## 有oa审核回调吗，我看都是机器人的

OA 审核还没接入，目前只接入了 事件订阅、卡片回调、机器人收消息。
其他场景有强烈需求可以加好友单独沟通，我们评估一下能否共创接入起来

## 协议就是websocket吗？可以用原生的c#自己实现吗？有什么特别需要注意的地方

可以参考协议文档 https://open.dingtalk.com/document/direction/stream-mode-protocol-access-description















