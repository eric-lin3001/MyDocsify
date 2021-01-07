## Apacha Kafka

1. ##### 历史

2. ##### 为什么需要kafka

   如果消息从客户端A传到客户端B，设想以下情况：

   1）A在发送的时候，B处于宕机状态，消息就丢了。

   2）A以10M/秒的速度主动传给B，而B的接收速度只有5M/秒，会产生阻塞/丢包/B挂机等情况。

   ###### 消息队列能解决上述问题：

   问题1） A发送消息给消息队列Q，若B处于宕机，消息不会丢，B可以随时去消息队列获取数据（消息）。

   问题2）客户端B可以控制从消息队列Q拉取的速度。 

2. ##### 消息队列

   1）模式：

   ① 点对点模式：客户端主动向Q拉取（缺点是客户端要有线程实时监听Q）

   ② 发布/订阅模式： Q主动推送给客户端，即客户端被动接收，类似公众号。（缺点是Q发送的速度值是唯一的，无法根据客户端接收数据的不同而指定不同的传输速度）。

   ###### 上述两种模式的缺点即为对方的优点，应根据业务的不同选择不同的模式。

4. ##### kafka基本概念

   1）kafka是一种分布式消息队列。

   2）几个名词：

   - 生产者(producer)

   - 消费者(consumer) 

   - 消费者组(consumer group):

      一个或多个消费者构成一个消费者组。若不指定消费者组，则默认的消费者组id为consumer.properties文件中的group.id:

     ![Screen Shot 2020-12-16 at 14.29.01](/Users/linzeyang/Library/Application Support/typora-user-images/Screen Shot 2020-12-16 at 14.29.01.png)

     查看group id列表：

     ```bash
     bin/kafka-consumer-groups.sh --zookeeper 【zk的ip】:2181 --list
     ```

     ![Screen Shot 2020-12-16 at 14.35.44](/Users/linzeyang/Library/Application Support/typora-user-images/Screen Shot 2020-12-16 at 14.35.44.png)

     查看某个group id详情：

     ```bash
     bin/kafka-consumer-groups.sh --zookeeper 【zk的ip】:2181 --group 【group_id】--describe
     ```

     ![Screen Shot 2020-12-16 at 14.36.58](/Users/linzeyang/Library/Application Support/typora-user-images/Screen Shot 2020-12-16 at 14.36.58.png)

     同一消费者组，同时开大于1个消费者，可以同时消费来自同一个topic的消息，但消息不全。比如topic发了5条消息[1,2,3,4,5,6,7,8,9,10]，consumer1收到1,2,4,5,7,8,10，consumer2收到3,6,9。

     对于不同消费者组的消费者，消费来自同一个topic消息时，每个消费者将收到全部的消息。

   - kafka实例(broker)

   - 主题(topic)

   - 分区(partition)

     Partitions are the main concurrency mechanism in Kafka. A topic is divided into 1 or more partitions, enabling producer and consumer loads to be scaled. Specifically, a consumer group supports as many consumers as partitions for a topic. 

     - 分区是kafka中主要的并发机制。一个topic可以被分成1个或多个partition，使得producer和consumer的扩展性更强。
     - 一个消费者组里，consumer数量<=partition数量。

   3）无论是kafka集群，还是consumer都依赖于zookeeper集群保存一些meta信息。

4. kafka架构


![Screen Shot 2020-11-14 at 21.55.39](/Users/linzeyang/Desktop/shots/Screen Shot 2020-11-14 at 21.55.39.png)



0）分区主要做负载均衡用。怎么理解？怎么理解topic下为什么要有分区？

1） 同一个topic下有不同partition，每个分区又有leader和follower，follower只做备份用。

2） 同一个消费者组的消费者，不可以同时消费同一个分区下的数据，而不同组的消费者可以。

6. kafka集群搭建和启动

7. kafka常用命令行操作（均在kafka bin目录下）

   0）查看帮助

   ```bash
   ./xxx.sh --help
   ```

   1） 创建topic/查看topic属性

   ```bash
   ./kafka-topics.sh --zookeeper 192.168.6.143:2181 --create --topic mytest --replication-factor 1 --partitions 3
   
/kafka-topics.sh --zookeeper 192.168.6.143:2181  --describe --topic ppjnb
   ```
   
   - 指定topic相关脚本文件: kafka-topics.sh
   - 指定zookeeper节点（因为topic信息要被存到zookeeper上）。
   - --topic： 指定topic名
- --replication-factor 指定副本数量（副本数不能超过broker数）
   - --partition 指定分区数量

   2） 查看topic列表/列举所有topic/删除topic
   
   ```bash
./kafka-topics.sh --list --zookeeper 192.168.6.143:2181
   
bin/kafka-topics.sh --zookeeper --zookeeper 192.168.6.143:2181 --list
   
bin/kafka-topics.sh --zookeeper --zookeeper 192.168.6.143:2181 --delete --topic ppjnb
   ```

   3）发送消息

   ```bash
   ./kafka-console-producer.sh --broker-list kafka01.test:6667,kafka02.test:6667,kafka03.test:6667 --topic [topicName]
   ```
   
   4）消费消息
   
   ```bash
   sh kafka-console-consumer.sh --bootstrap-server kafka01.test:6667,kafka02.test:6667,kafka03.test:6667 --topic ericuu1 --group cwz2	 --from-beginning
   ```
   
   - 同一个消费者，同一时间只能消费一个topic。
- 消费者连的是zookeeper,因为zookeeper会保存消费者offset信息。
  
   - 警告：新版本不交给zookeeper维护，而是维护在本地。
   
     
   

5) 查看partition情况

```bash
   ./kafka-run-class.sh kafka.tools.ConsumerOffsetChecker --group group_mytes2 topic mytest1 --zookeeper 192.168.6.143:2181
```

   ![Screen Shot 2020-12-02 at 15.50.50](/Users/linzeyang/Library/Application Support/typora-user-images/Screen Shot 2020-12-02 at 15.50.50.png)

- Pid: 分区 ID
   - Offset: 某个消费组目前在此分区所在的offset（已消费多少条）。
- logSize: 该分区消息总数量。
   - Lag: 该消费组当前在此分区未消费的消息数量（#Lag = #LogSize - #Offset）
- 同一个topic下不同partition存的数据是不一样的，同一消费者组的不同消费者，可以同时消费不同的分区数据，但这就需要消费者对producer发来的数据顺序没有要求？比如producer发送支付订单，消费者消费不同消费者的订单，判断其是否有效，这里就对先收到哪个订单没要求，而是需要很高的吞吐率。
  

6) 查看partition日志

- 日志位置：与config/server.properties的log.dirs配置相同。
  
   - 日志的颗粒度是分区，即每个分区有一个文件夹存放该分区的日志。
   
   - 以topic为mytest1为例，该topic分区值为1的文件夹下有以下文件：
   
     ![Screen Shot 2020-12-02 at 17.02.58](/Users/linzeyang/Library/Application Support/typora-user-images/Screen Shot 2020-12-02 at 17.02.58.png)



7) 查看kafka版本号

```bash
cd /usr/hdp/current/kafka-broker/libs
ll |grep kafka
```



##### References:

###### 1. The Power of Kafka Partitions:

https://www.instaclustr.com/the-power-of-kafka-partitions-how-to-get-the-most-out-of-your-kafka-cluster/