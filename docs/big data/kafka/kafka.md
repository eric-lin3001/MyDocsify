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

3. ##### kafka基本概念

   1）kafka是一种分布式消息队列。

   2）几个名词：生产者(producer)，消费者(consumer)， 消费者组(consumer group)，kafka实例(broker)，主题(topic)，分区(partition)。

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

   1） 创建topic

   ```bash
   ./kafka-topics.sh --zookeeper 192.168.6.143:2181 --create --topic mytest --replication-factor 1 --partitions 3
   ```

   - 指定topic相关脚本文件: kafka-topics.sh
   - 指定zookeeper节点（因为topic信息要被存到zookeeper上）。
   - --topic： 指定topic名
   - --replication-factor 指定副本数量（副本数不能超过broker数）
   - --partition 指定分区数量

   2） 查看topic列表

   ```bash
   ./kafka-topics.sh --list --zookeeper 192.168.6.143:2181
   ```

   3）发送消息

   4）消费信息

   消费者连的是zookeeper,因为zookeeper会保存消费者offset信息。

   警告：新版本不交给zookeeper维护，而是维护在本地。

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

