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

这个Stream模式的文档说明，https://open.dingtalk.com/document/resourcedownload/Introduction-to-stream-mode，主要是免去开发者申请公网域名，IP，服务器的成本。通过可信的方式与钉钉建立连接来接收回调消息



