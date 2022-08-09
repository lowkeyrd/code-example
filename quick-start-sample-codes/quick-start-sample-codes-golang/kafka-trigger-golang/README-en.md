# kafka-trigger-fc-event-golang help documentation

<p align="center" class="flex justify-center">
    <a href="https://www.serverless-devs.com" class="ml-1">
    <img src="http://editor.devsapp.cn/icon?package=kafka-producer-fc-event-golang&type=packageType">
  </a>
  <a href="http://www.devsapp.cn/details.html?name=kafka-producer-fc-event-golang" class="ml-1">
    <img src="http://editor.devsapp.cn/icon?package=kafka-producer-fc-event-golang&type=packageVersion">
  </a>
  <a href="http://www.devsapp.cn/details.html?name=kafka-producer-fc-event-golang" class="ml-1">
    <img src="http://editor.devsapp.cn/icon?package=kafka-producer-fc-event-golang&type=packageDownload">
  </a>
</p>

## Preliminary preparation

### Permission preparation

Using this item, verify that your operational account has the following product permissions/policies:


| Service/Business     | Functional Computing                                         |
| -------------------- | ------------------------------------------------------------ |
| Permissions/Policies | AliyunFCFullAccess<br/>AliyunKafkaReadOnlyAccess<br/>AliyunVPCReadOnlyAccess |


### Resource preparation

  * For an available Kafka message queue, please refer to the official document of message queue Kafka version [Quick Start of Message Queue](https://help.aliyun.com/document_detail/99949.html).

    - Create a VPC private network (VPC is recommended in the production environment), please refer to [VPC official document](https://help.aliyun.com/document_detail/65398.htm?spm=a2c4g.11186623.0.0.61be4c9d4aGfpg# task-1012575). VPC console [link](https://vpcnext.console.aliyun.com/). At this point, you can have a VPC and corresponding switches.

    > When deploying a Kafka instance, you will be prompted to create an available VPC private network

  * Create the Kafka Topic and Consumer Group to be used in the Kafka console.

# Code & Preview

- [ :smiley_cat:source code](https://github.com/devsapp/)
- In order to successfully deploy this sample code, you need to provide the following parameters during the deployment process:
  - Region: You need to configure the region where your Function Compute service needs to be deployed through this parameter. The default value is cn-qingdao (Qingdao).
    - The geographic options available to you are:
      - cn-qingdao (Qingdao)
      - cn-hongkong (Hong Kong)
  - Service name: You need to name your Function Compute service. The service name can only contain letters, numbers, underscores and dashes. Cannot start with a number or a dash. The length is between 1-128, the default value is kafka-trigger-quick-start.
  - Function name: You need to name your function calculation function. The function name can only contain letters, numbers, underscores and dashes. Cannot start with a number or a dash. The length is between 1-64. The default is kafka-trigger-event-function-golang.
  - vpcId: We recommend that you use a VPC to access Kafka, and select the VPC used to create a Kafka instance. Note that you need to fill in the az supported by Function Compute.
  - vswitchIds: Use the vswitch id in the vpc to access kafka on the intranet. Note that az needs to be supported by Function Compute.
  - securityGroupId: The security group id of the vpc where the kafka instance is located, which can be found in the `ECS` console `Network and Security` menu item.
  - Instance ID (instanceId): The Kafka instance ID you purchased.
  - topicName: The topic name of the Kafka instance. The data production of this topic will trigger the deployment function, which needs to be created in advance.
  - Consumer Group: Data is consumed by this consumer group, which needs to be created in advance.
  - Consumption location (offsetReset): Kafka consumption location, you can choose the latest location (latest) or the earliest location (earliest).

</codepre>

<deploy>

## Deployment & Experience

<appcenter>

- :fire: via [Serverless Application Center](https://fcnext.console.aliyun.com/applications/create?template=kafka-trigger-fc-event-golang),
   [![Deploy with Severless Devs](https://img.alicdn.com/imgextra/i1/O1CN01w5RFbX1v45s8TIXPz_!!6000000006118-55-tps-95-28.svg)](https://fcnext.console.aliyun. com/applications/create?template=kafka-trigger-fc-event-golang) the application.

</appcenter>

- Deploy via [Serverless Devs Cli](https://www.serverless-devs.com/serverless-devs/install):

  - [Install Serverless Devs Cli Developer Tools](https://www.serverless-devs.com/serverless-devs/install), and perform [Authorization Information Configuration](https://www.serverless-devs.com/ fc/config);
  - Initialize the project: `s init kafka-trigger-fc-event-golang -d kafka-trigger-fc-event-golang`
  - Fill in the parameters described in the above modules
  - Enter the project and deploy the project: `cd kafka-trigger-fc-event-golang && s deploy -y`
- local debugging
  - Enter the application project project and execute the following command: `s invoke --event-file event-example/kafka-eventbridge-fc-sample.json`.
  - You can view the logs and results after the simulated event triggers the function.

```bash
========= FC invoke Logs begin =========
2022/08/02 10:09:24.563207 start
FC Invoke Start RequestId: 947e52d4-c453-43a2-a53d-a64ba020bbe9
2022-08-02T10:09:24.568Z 947e52d4-c453-43a2-a53d-a64ba020bbe9 [INFO] main.go:46: kafka event: [{"data":{"topic":"HelloTopic","partition": 9,"offset":3,"timestamp":1659346376797,"headers":{"headers":[],"isReadOnly":false},"value":"b\u0027{\\n \"Test\" : \"TestKafkaEBtrigger\"\\n}\u0027"},"id":"1cb591f9-987e-41d9-b974-0342e9acb90a","source":"acs:alikafka","specversion":"1.0"," type":"alikafka:Topic:Message","datacontenttype":"application/json; charset\u003dutf-8","time":"2022-08-01T09:32:56.797Z","subject":"acs :alikafka:alikafka_pre-cn-7pp2t2jwj001:topic:HelloTopic","aliyunaccountid":"1938858730552836"}]
2022-08-02T10:09:24.568Z 947e52d4-c453-43a2-a53d-a64ba020bbe9 [INFO] main.go:48: kafka topic: HelloTopic
2022-08-02T10:09:24.568Z 947e52d4-c453-43a2-a53d-a64ba020bbe9 [INFO] main.go:49: kafka messgae: b'{\n "Test": "TestKafkaEBtrigger"\n}'
FC Invoke End RequestId: 947e52d4-c453-43a2-a53d-a64ba020bbe9

Duration: 1.13 ms, Billed Duration: 2 ms, Memory Size: 128 MB, Max Memory Used: 8.58 MB
========= FC invoke Logs end =========

FC Invoke instanceId: c-62e8f7d4-698c5e9d72d94301af34

FC Invoke Result:
"Receive Kafka Trigger Event: [{"data":{"topic":"HelloTopic","partition":9,"offset":3,"timestamp":1659346376797,"headers":{"headers":[] ,"isReadOnly":false},"value":"b\u0027{\\n \"Test\": \"TestKafkaEBtrigger\"\\n}\u0027"},"id":"1cb591f9-987e-41d9 -b974-0342e9acb90a","source":"acs:alikafka","specversion":"1.0","type":"alikafka:Topic:Message","datacontenttype":"application/json; charset\u003dutf-8 ","time":"2022-08-01T09:32:56.797Z","subject":"acs:alikafka:alikafka_pre-cn-7pp2t2jwj001:topic:HelloTopic","aliyunaccountid":"1938858730552836"}]"End of method: invoke
````



- End-to-end testing

  - Log in to the Kafka console to view the `details` of the corresponding topic of the corresponding instance
  - Select `Quick Experience Messaging` to send a test message
  - Log in to the Function Compute console, find the function you just deployed, and view the `call log` (if the log is not activated, click one-click activation) to view the function trigger log.

  

</deploy>

<appdetail id="flushContent">

# application details



This application is only used for learning and reference. You can carry out secondary development and improvement based on this project to realize your own business logic.



</appdetail>

<devgroup>

## Developer Community

If you have feedback about bugs or future expectations, you can give feedback and exchange in [Serverless Devs repo Issues](https://github.com/serverless-devs/serverless-devs/issues). If you want to join our discussion group or keep up to date with the latest developments in FC components, you can do so through the following channels:

<p align="center">
| <img src="https://serverless-article-picture.oss-cn-hangzhou.aliyuncs.com/1635407298906_20211028074819117230.png" width="130px" > | <img src="https://serverless-article-picture.oss-cn-hangzhou.aliyuncs.com/1635407044136_20211028074404326599.png" width="130px" > | <img src="https://serverless-article-picture.oss-cn-hangzhou.aliyuncs.com/1635407252200_20211028074732517533.png" width="130px" > |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| <center>WeChat Official Account: `serverless`</center>       | <center>WeChat Assistant: `xiaojiangwh`</center>             | <center>DingTalk Group:`33947367`</center>                   |

</p>

</devgroup>
