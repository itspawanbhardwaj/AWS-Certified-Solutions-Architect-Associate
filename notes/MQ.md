Exam tip: When a scenario in which we are migrating an on-premise app, using protocols such as MQTT, AMQP, STOMP, Openwire, WSS, to cloud, we will use MQf

- SQS, SNS are cloud-native services using proprietary protocols from AWS. There are traditional applications running from on-premise may use open protocols such as MQTT, AMQP, STOMP, Openwire, WSS etc
- When migrating such applications to the cloud, we dont want to re-engineer the messaging layer to use SQS and SNS
- MQ provides a way to run MQTT into cloud
- AMazon MQ =  managed Apache ActiveMQ
- MQ doesnt scale as much as SQS or SNS
- MQ runs on a dedicated machine, can run in HA with failover
- MQ has both queue feature (SQS) and topic feature (SNS)
