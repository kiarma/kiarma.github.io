---
layout: post
title: MQ面试合集
category: 面试
---

### 1.介绍消息队列的作用？
+  吞吐量提升：无需等待订阅者处理完成，响应更快速
+  故障隔离：服务没有直接调用，不存在级联失败问题
+  调用间没有阻塞，不会造成无效的资源占用
+  耦合度极低，每个服务都可以灵活插拔，可替换
+  流量削峰：不管发布事件的流量波动多大，都由Broker接收，订阅者可以按照自己的速度去处理事件

### 2.常见的mq产品?
| | **<font style="color:rgb(51, 51, 51);">RabbitMQ</font>** | **<font style="color:rgb(51, 51, 51);">ActiveMQ</font>** | **<font style="color:rgb(51, 51, 51);">RocketMQ</font>** | **<font style="color:rgb(51, 51, 51);">Kafka</font>** |
| --- | :--- | :--- | :--- | :--- |
| <font style="color:rgb(51, 51, 51);">公司/社区</font> | <font style="color:rgb(51, 51, 51);">Rabbit</font> | <font style="color:rgb(51, 51, 51);">Apache</font> | <font style="color:rgb(51, 51, 51);">阿里</font> | <font style="color:rgb(51, 51, 51);">Apache</font> |
| <font style="color:rgb(51, 51, 51);">开发语言</font> | <font style="color:rgb(51, 51, 51);">Erlang</font> | <font style="color:rgb(51, 51, 51);">Java</font> | <font style="color:rgb(51, 51, 51);">Java</font> | <font style="color:rgb(51, 51, 51);">Scala&Java</font> |
| <font style="color:rgb(51, 51, 51);">协议支持</font> | <font style="color:rgb(51, 51, 51);">AMQP，XMPP，SMTP，STOMP</font> | <font style="color:rgb(51, 51, 51);">OpenWire,STOMP，REST,XMPP,AMQP</font> | <font style="color:rgb(51, 51, 51);">自定义协议</font> | <font style="color:rgb(51, 51, 51);">自定义协议</font> |
| <font style="color:rgb(51, 51, 51);">可用性</font> | <font style="color:rgb(51, 51, 51);">高</font> | <font style="color:rgb(51, 51, 51);">一般</font> | <font style="color:rgb(51, 51, 51);">高</font> | <font style="color:rgb(51, 51, 51);">高</font> |
| <font style="color:rgb(51, 51, 51);">单机吞吐量</font> | <font style="color:rgb(51, 51, 51);">一般</font> | <font style="color:rgb(51, 51, 51);">差</font> | <font style="color:rgb(51, 51, 51);">高</font> | <font style="color:rgb(51, 51, 51);">非常高</font> |
| <font style="color:rgb(51, 51, 51);">消息延迟</font> | <font style="color:rgb(51, 51, 51);">微秒级</font> | <font style="color:rgb(51, 51, 51);">毫秒级</font> | <font style="color:rgb(51, 51, 51);">毫秒级</font> | <font style="color:rgb(51, 51, 51);">毫秒以内</font> |
| <font style="color:rgb(51, 51, 51);">消息可靠性</font> | <font style="color:rgb(51, 51, 51);">高</font> | <font style="color:rgb(51, 51, 51);">一般</font> | <font style="color:rgb(51, 51, 51);">高</font> | <font style="color:rgb(51, 51, 51);">一般</font> |


<font style="color:rgb(51, 51, 51);">追求可用性：Kafka、 RocketMQ 、RabbitMQ</font>

<font style="color:rgb(51, 51, 51);">追求可靠性：RabbitMQ、RocketMQ</font>

<font style="color:rgb(51, 51, 51);">追求吞吐能力：RocketMQ、Kafka(</font><font style="color:#fa8c16;">大吞吐量才会去使用</font><font style="color:rgb(51, 51, 51);">)</font>

<font style="color:rgb(51, 51, 51);">追求消息低延迟：RabbitMQ、Kafka</font>

### 3.rabbitmq支持哪些消息模式?
+ 基本消息队列(使用默认转换器)
+ 工作消息队列(使用默认转换器)
+ 发布订阅
    - Fanout Exchange: 广播
    - Direct Exchange: 路由
    - Topic Exchange: 主题

### 4.什么是AMQP协议模型?
![](https://cdn.nlark.com/yuque/0/2021/png/22908560/1635755137094-b7932cf1-55ae-411a-a63f-2a97b545f8d4.png)

<font style="color:rgb(77, 77, 77);">Broker：代表着一个中间件应用，负责接收消息生产者的消息，然后将消息发送至消息接受者或者其他的broker。  
</font>

<font style="color:rgb(77, 77, 77);">Virtual host：这是对broker的虚拟化分，主要用于对consumer、producer和他们依赖的AMQP相关结构进行隔离。通常是处于安全因素的考虑。</font>

<font style="color:rgb(77, 77, 77);">Connection：代表着producer、consumer和broker之间的物理网络（TCP），connection只有在客户端断开连接或者网络问题的时候会断开。  
</font>

<font style="color:rgb(77, 77, 77);">Channel：代表着producer、consumer和broker之间的逻辑连接，一个Connection可以包含多个Channel。Channel使得基同一连接的不同进程之间与broker之间的交互相互隔离，不干扰。而不需要重新建立连接，channel在发生协议错误的时候会被关闭。</font>

<font style="color:rgb(77, 77, 77);">Exchange：这是所有被发送的消息首先到达的目的地，Exchange负责根据路由规则将消息路由到不同的目的地。路由规则包括下面几种：direct（point-to-point）、topic（publish-subscribe）和fanout（multicast）。</font>

<font style="color:rgb(77, 77, 77);">Queue：这是消息到达的最终目的地，到达queue的消息是已经准备好被消费的消息，一个消息可以被exchange copy发送至多个queue。  
</font>

<font style="color:rgb(77, 77, 77);">Binding：这是queue和exchange之间的虚拟连接，使得消息从哪个exchange路由到Queue。routing key可以通过binding和exchange routing规则关联。</font>

### 5.消息转换器的作用?
<font style="color:rgb(77, 77, 77);">MessageConverter的作用主要有两方面.</font>

    - <font style="color:rgb(77, 77, 77);">一方面它可以把我们的非标准化Message对象转换成我们的目标Message对象，这主要是用在发送消息的时候；</font>
    - <font style="color:rgb(77, 77, 77);">另一方面它又可以把我们的Message对象转换成对应的目标对象，这主要是用在接收消息的时候。</font>

### 6.rabbitmq如何保证消息的可靠性?
![](https://cdn.nlark.com/yuque/0/2022/png/26104459/1651137402307-7b9221bf-c32d-4cea-9f0d-06dd13f6a3fc.png)

**<font style="color:rgb(0, 0, 0);">生产者弄丢消息时的解决方法</font>**

+ <font style="color:rgb(49, 70, 89);">方法一：生产者在发送数据之前开启RabbitMQ的事务(采用该种方法由于事务机制，会导致吞吐量下降，太消耗性能。)</font>
+ <font style="color:rgb(49, 70, 89);">方法二：开启confirm模式(使用springboot时在application.yml配置文件中做如下配置，实现confirm回调接口，生产者发送消息时设置confirm回调)</font>
+ <font style="color:rgb(49, 70, 89);">小结： 事务机制和 confirm机制最大的不同在于，事务机制是同步的，你提交一个事务之后会阻塞在那儿，但是 confirm机制是异步的，你发送个消息之后就可以发送下一个消息，RabbitMQ 接收了之后会异步回调confirm接口通知你这个消息接收到了。一般在生产者这块避免数据丢失，建议使用用 confirm 机制。</font>



**MQ自身弄丢消息**

+ <font style="color:rgb(49, 70, 89);">第一步： 创建queue时设置为持久化队列，这样可以保证RabbitMQ持久化queue的元数据，此时还是不会持久化queue里的数据。</font>
+ <font style="color:rgb(49, 70, 89);">第二步： 发送消息时将消息的deliveryMode设置为持久化，此时queue中的消息才会持久化到磁盘。</font>
+ <font style="color:rgb(49, 70, 89);">总结：同时设置queue和message持久化以后，RabbitMQ 挂了再次重启，也会从磁盘上重启恢复 queue，恢复这个 queue 里的数据，保证数据不会丢失。</font>
+ <font style="color:rgb(49, 70, 89);">但是：但是就算开启持久化机制，也有可能出现上面说的的消息落盘时服务挂掉的情况。这时可以考虑结合生产者的confirm机制来处理，持久化机制开启后消息只有成功落盘时才会通过confirm回调通知生产者，所以可以考虑生产者在生产消息时维护一个正在等待消息发送确认的队列，如果超过一定时间还没从confirm中收到对应消息的反馈，自动进行重发处理</font>

<font style="color:rgb(49, 70, 89);"></font>

**<font style="color:rgb(49, 70, 89);">消费者弄丢消息</font>**

+ <font style="color:rgb(49, 70, 89);">方法：关闭自动ACK，使用手动ACK。RabbitMQ中有一个ACK机制，默认情况下消费者接收到到消息，RabbitMQ会自动提交ACK，之后这条消息就不会再发送给消费者了。我们可以更改为手动ACK模式，每次处理完消息之后，再手动ack一下。不过这样可能会出现刚处理完还没手动ack确认，消费者挂了，导致消息重复消费，不过我们只需要保证幂等性就好了，重复消费也不会造成问题。</font>
+ <font style="color:rgb(49, 70, 89);">步骤一：在springboot中修改application.yml配置文件更改为手动ack模式</font>
+ <font style="color:rgb(49, 70, 89);">步骤二：手动实现ack的callback</font>

**<font style="color:rgb(49, 70, 89);"></font>**

**<font style="color:rgb(49, 70, 89);">总结</font>**

![](https://cdn.nlark.com/yuque/0/2022/png/26104459/1651137572752-97a31483-d01b-4696-9a1c-e898fa2f209e.png)

### 7.rabbitmq如何避免消息堆积?
1.去优化消费者代码，提高消费能力。减少消费时间  
2.可以给消费设置年龄（生命周期），如果超时就丢弃掉。可以不让消息大量堆积在消息队列中  
3.可以设置队列的最大长度：如果超过了，就无法接收消息到队列中。  
4.建立新的消息队列，采用订阅模式，消费者同时去订阅新的，还有旧的消息队列，同时去消费消息。

### 8.rabbitmq如何防止消息重复消费?
	<font style="color:rgb(75, 75, 75);">每个消息用一个唯一标识来区分，消费前先判断标识有没有被消费过，若已消费过，则直接ACK</font>

### 9.rabbitmq如何保证高可用
镜像集群模式

### 10.rabbitmq在项目中的使用场景


### ***面试题***
#### 1、RabbitMQ 工作模式
**五种模式**：

1. **简单模式**：<font style="color:rgb(79, 79, 79);">一对一模式，一个生产者、一个消费者，一个队列，生产者发送消息，消费者消费消息</font>



2. **工作队列模式**：<font style="color:rgb(79, 79, 79);">一对多模式，一个生产者，多个消费者，一个队列，每个消费者从队列中获取唯一的消息。与入门程序的简单模式相比，多了一个或一些消费端，多个消费端共同消费同一个队列中的消息</font>



3. **发布订阅模式**：

![](https://cdn.nlark.com/yuque/0/2022/png/26104459/1651133952557-a5d7b357-c5e7-4090-ae87-a38d32cf9323.png)

多了一个 Exchange 角色，而且过程略有变化：

生产者，也就是要发送消息的程序，但是不再发送到队列中，而是发给X（交换机）

消费者，消息的接收者，会一直等待消息到来

消息队列，接收消息、缓存消息

交换机一方面，接收生产者发送的消息。另一方面，知道如何处理消息，例如递交给某个特别队列、递交给所有队列、或是将消息丢弃。到底如何操作，取决于Exchange与消息队列的绑定模式：

+ **<font style="color:rgb(51, 51, 51);">F</font>****<font style="color:rgb(51, 51, 51);">anout</font>**<font style="color:rgb(51, 51, 51);">：广播，将消息交给所有绑定到交换机的队列，</font><font style="color:rgb(77, 77, 77);">当发送一条消息到fanout交换器上时，它会把消息投放到所有附加在此交换器上的队列</font>
+ **<font style="color:rgb(51, 51, 51);">Direct</font>**<font style="color:rgb(51, 51, 51);">：定向，把消息交给符合指定routing key 的队列，</font><font style="color:rgb(77, 77, 77);">如果路由键完全匹配的话，消息才会被投放到相应的队列</font>
+ **<font style="color:rgb(51, 51, 51);">Topic</font>**<font style="color:rgb(51, 51, 51);">：通配符，把消息交给符合routing pattern（路由模式） 的队列，</font><font style="color:rgb(77, 77, 77);">设置模糊的绑定方式，“*”操作符将“.”视为分隔符，匹配单个字符；“#”操作符没有分块的概念，它将任意“.”均视为关键字的匹配部分，能够匹配多个字符</font>



<font style="color:rgb(77, 77, 77);">交换机：只负责转发消息，不具备存储消息的能力，因此如果没有任何队列与 Exchange 绑定，或者没有符合路由规则的队列，那么消息会丢失</font>



**工作模式总结**：

这五种工作模式，可以归结为3类：

生产者，消息队列，一个消费者；

生产者，消息队列，多个消费者；

生产者，交换机，多个消息队列，多个消费者



#### 2、MQ如何保证顺序消费
<font style="color:rgb(77, 77, 77);">RabbitMQ的queue本身就是队列，是可以保证消息的顺序投递的。</font>

<font style="color:rgb(77, 77, 77);">但是消息的顺序消费则是另一回事了，所谓的“顺序消费”意味着是否顺序达到目的地，比如：数据库。</font>

<font style="color:rgb(77, 77, 77);">看看以下场景：</font>

一个 queue，多个 consumer。比如，生产者向 RabbitMQ 里发送了三条数据，顺序依次是 data1/data2/data3，压入的是 RabbitMQ 的一个内存队列。有三个消费者分别从 MQ 中消费这三条数据中的一条，结果消费者2先执行完操作，把 data2 存入数据库，然后是 data1/data3。这不明显乱了。

![](https://cdn.nlark.com/yuque/0/2022/png/26104459/1650554619432-3c20920c-be04-4dc3-8a3b-4d7370b284cd.png)

产生多个consumer去消费一个queue，极有可能是因为：消息消费太慢，所以盲目让多个consumer同时来消费，而忽略了消息消费顺序性。

在某些情况下，消息是需要保证顺序性的，如果上图中的data1, data2, data3 分别意味着对某条数据的增改删，但是如果乱序以后就变成了：删改增。

**解决方案**：

![](https://cdn.nlark.com/yuque/0/2022/png/26104459/1651498232846-33c14cd5-6b16-4cab-b43f-89a49cf47b92.png)

#### 3、MQ如何消息不丢失，持久化
有四种方式可以解决：

1. <font style="color:rgb(77, 77, 77);">消息持久化</font>
2. <font style="color:rgb(77, 77, 77);">ACK确认机制（项目中使用）：ACK确认机制是消费者从队列中收到消息，进行业务逻辑的处理，在这一过程中如果消费者出现服务器异常、网络不稳定等，都不会有ACK应答，这时候RabbitMQ就认为这条消息没有正常消费成功，就会将消息重新放回队列中。直到消费者发送ACK应答，这条消息才会从队列中消费掉。</font>**<font style="color:rgb(77, 77, 77);">使用</font>**<font style="color:rgb(77, 77, 77);">：需要手动开启配置，yaml文件</font>

publisher-confirm-type: correlated  # 开启确认机制回调 必须配置这个才会确认回调

       publisher-returns: true # 开启return机制回调



3. <font style="color:rgb(77, 77, 77);">设置集群镜像模式</font>
4. <font style="color:rgb(77, 77, 77);">消息补偿机制</font>

**消息持久化解决**：

<font style="color:rgba(0, 0, 0, 0.75);">消息中心收到生产者的消息后，先将消息存储在本地数据文件，内存数据库或者远程数据库，再试图把消息发送给消费者，发送成功则讲消息从存储中删除，如失败则继续尝试发送</font>  
<font style="color:rgba(0, 0, 0, 0.75);">消息中心启动时，先会检查指定的存储位置，如有未成功发送的消息，则会把消息发送出去</font>

1. <font style="color:rgb(77, 77, 77);">Exchange 设置持久化：基于代码的，参数设为true</font>
2. <font style="color:rgb(77, 77, 77);">Queue 设置持久化</font>
3. <font style="color:rgb(77, 77, 77);">Message持久化发送：发送消息设置发送模式deliveryMode=2，代表持久化消息</font>



#### 4、MQ的消息确认机制（生产者发送到交换机，有个回调，交换机到队列，也有个回调，消费者有没有去消费这个消息）
1. 为了保证消息从队列可靠的达到消费者，RabbitMQ 提供了消息确认机制（Message Acknowledgement）。消费者在订阅队列时，可以指定 autoAck 参数，当 autoAck 参数等于 false 时，RabbitMQ 会等待消费者显式地回复确认信号后才从内存（或者磁盘）中移除消息（实际上是先打上删除标记，之后在删除）。当 autoAck 参数等于 true 时，RabbitMQ 会自动把发送出去的消息置为确认，然后从内存（或者磁盘）中删除，而不管消费者是否真正地消费到了这些消息。
2. 采用消息确认机制后，只要设置 autoAck 参数为 false，消费者就有足够的时间处理消息（任务），不用担心处理消息过程中消费者进程挂掉后消息丢失的问题，因为 RabbitMQ 会一直等待持有消息直到消费者显式调用 Basic.Ack 命令为止。
3. 当autoAck 参数为 false 时，对于 RabbitMQ 服务器端而言，队列中的消息分成了两部分：一部分是等待投递给消费者的消息；一部分是已经投递给消费者，但是还没有收到消费者确认信号的消息。如果 RabbitMQ 服务器端一直没有收到消费者的确认信号，并且消费此消息的消费者已经断开连接，则服务器端会安排该消息重新进入队列，等待投递给下一个消费者（也可能还是原来的那个消费者）。
4. RabbitMQ 不会为未确认的消息设置过期时间，它判断此消息是否需要重新投递给消费者的唯一依据是消费该消息连接是否已经断开，这个设置的原因是 RabbitMQ 允许消费者消费一条消息的时间可以很久很久。



#### 5、MQ高可用
**镜像集群模式**：

![](https://cdn.nlark.com/yuque/0/2022/png/26104459/1650557061244-ed4c5750-ba29-4fb2-9b7f-1703c03a9716.png)

1. 无论元数据还是 queue 里的消息都会存在于多个broker上
2. 每个queue都想拥有多个镜像放在其他broker上，可以选择镜像队列的数量
3. 由于每个broker上都具有近乎完整的数据，所以消费者消费的时候并不需要进行消息传输，但由于并不是想Kafka分布式消息队列那样的分片存储，所以性能并不高



小小总结一下，RabbitMQ其实并不是分布式消息队列，大厂使用的分布式消息队列，更多是RocketMQ或者Kafka，可以分布式分片存储，水平扩容性能会有明显提升



#### 6、消息生产方将消息成功投递到消息消费方，消息消费成功了， 业务逻辑执行失败了， 问怎么办？
自动确认机制 改成 手动确认，在业务逻辑 try...catch{} 拒绝接收，消息重放到MQ队列

#### 7、MQ消息堆积问题
多线程消息 + 一个线程一次去消费多少条消息

#### 8、如何保证幂等性
+ <font style="color:rgb(49, 70, 89);">消费数据为了单纯的写入数据库，可以先根据主键查询数据是否已经存在，如果已经存在了就没必要插入了。或者直接插入也没问题，因为可以利用主键的唯一性来保证数据不会重复插入，重复插入只会报错，但不会出现脏数据。</font>
+ <font style="color:rgb(49, 70, 89);">消费数据只是为了缓存到redis当中，这种情况就是直接往redis中set value了，天然的幂等性。</font>
+ <font style="color:rgb(49, 70, 89);">针对复杂的业务情况，可以在生产消息的时候给每个消息加一个全局唯一ID，消费者消费消息时根据这个ID去redis当中查询之前是否消费过。如果没有消费过，就进行消费并将这个消息的ID写入到redis当中。如果已经消费过了，就无需再次消费了。</font>key：全局唯一  redis：key

#### 9、消费者已经接收了消息，因为某种原因导致业务代码没执行完全，怎么处理？
1. **失败重试机制，配置**

![](https://cdn.nlark.com/yuque/0/2022/png/26104459/1651757307344-ba69c313-aeb2-426a-9305-fb91b24beda4.png)

2. **策略**

![](https://cdn.nlark.com/yuque/0/2022/png/26104459/1651757335247-9eba0028-3e03-47ce-b50d-a7a72558a313.png)

