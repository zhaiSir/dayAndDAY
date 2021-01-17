# zhaiSir收集
# kafka实战应用&文章自动审核
## 今日目标

熟悉kafka的封装技巧

熟悉阿里审核图片和文本内容审核

完成自媒体文章审核代码

完成自媒体端发布文章发送信息

完成admin端接收消息并自动审核

# 1.kafka封装

## 1.1.功能需求

消息对于现代软件项目来说，占据很重要的地位；同时市场上也发展出ActiveMq、RabbitMQ、kafka、RocketMQ、pulsar等众多优秀的框架；这些优秀的框架都有自身的特点和擅长的业务领域，在大数据领域中kafka目前是使用较多的框架，Pulsar是一个后起之秀，目前处于一个快速发展的状态，有望成为下一代中间件的黑马。在本案例中我们选择使用kafka作为内部消息通知的框架，以适应项目中大数据量的高吞吐、实时流计算等功能的实现。

## 1.2 定义

### 1.2.1 约束定义
（1）Topic命名约束
Topic分为单类和混合类消息，不同类的消息命名约束如下：
- 单类：heima.topic.[自定义名称].single
- 混合类：heima.topic.[自定义名称].bus

## 1.3 实现设计

- kafkaProducerConfig自动配置kafka消费者
- kafkaConsumerConfig自动配置kafka消费者
- RetryErrorHandler实现消费者处理信息失败后重新发送到消息队列
- kafkaMessage实现对发送的消息包装，提供重试次数、分类等信息
- kafkaSender实现消息的统一发送入口功能
- kafkaTopicConfig自动装载topic名称信息
- kafkaListenter提供自动注册消息消费监听接口类
- kafkaListenerFactory提供启动时自动注册实现了KafkaListener的消息消费者

## 1.4 开发实现

### 1.4.1 配置文件

kafka功能有独立的配置文件，放置在是src\main\resources\kafka.properties,相关的值在maven_*.properties中配置。

```propperties
#kafka config
kafka.hosts=locallhost:9092
kafka.group=heima.${profiles.name}.${spirng.aplication.name}

# 单消息通道，需要以single结尾
kafka.topic.admin-test${kafaka.topic.admin-test}
```

### 1.4.2 kafkaMessage
```java
/**
*kafaka消息
*/
public abstract class kafkaMessage<T> {
    //尝试次数
    @Getter
    int retry;
    //生成时间
    @Getter
    long time = System.currentTimeMillis();
}
```

