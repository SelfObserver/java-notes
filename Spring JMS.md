# 消息中间件
为了改善系统模块的调用关系、减少模块之间的耦合

## 什么是消息中间件

消息中间件利用信息传递机制进行平台无关的数据交流，基于数据通信进行分布式系统的集成，通过提供消息传递和消息排队模型，它可以在分布式环境下扩展进程之间的通信。对于消息中间件，常见的角色大致有生产者和消费者。

## 常见的消息中间件产品

1. ActiveMQ
2. RabbitMQ
3. ZeroMQ
4. Kafka

## 什么是JMS

JMS是java平台上有关面向消息中间件的技术规范，它便于消息系统中的java应用程序进行信息交换，并且通过提供标准的产生、发送、接受消息的接口简化企业应用的开发。

## JSM五种不同的消息正文格式

* TextMessage 字符串对象
* MapMessage 键值对
* ObjectMessage 序列化的java对象
* BytesMessgae 一个字节的数据流
* StreamMessage java原始数据流

## JMS消息传递类型

1. 点对点，一个生产者对应一个消费者
2. 发布/订阅模式，一个生产这产生消息并进行发送后，可以由多个消费者进行接受

## ACtiveMQ默认端口号8161

## 点对点模式

建立在一个队列上，当连接一个队列时，发送端不需要知道接收端是否正在接受，可以直接向ActiveMQ发送消息，发送的消息，将会先进入队列中，如果有接收端在监听，则会发送接收端，如果没有接受端接受，则会保存在activemq服务器中，直到接收端接受消息，点对点的消息模式可以有有个发送端，多个接受端，但是一条消息，只会被一个接受端给接受到，那个接收端先连上ActiveMQ，则会先接受到，而后来的接受端接受不到那条消息

## Spring-JMS

1. 配置connectionFactory
2. 配置队列目的地（点对点/发布订阅 消息正文格式）
3. 配置监听类
4. 配置消息监听容器