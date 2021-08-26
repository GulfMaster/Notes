## 下载

~~~
https://www.apache.org/dyn/closer.cgi?path=/kafka/2.7.0/kafka_2.13-2.7.0.tgz
~~~

## 解压

~~~
tar -xzvf kafka_2.13-2.7.0.tgz
~~~

## 修改配置文件

~~~
位置：conf/server.properties
listeners=PLAINTEXT://182.92.83.153:9092

位置：conf/zookeeper.properties

~~~



## 编写启动脚本

~~~
进入kafka目录下 输入命令：vim  kafkaStart.sh
 
添加内容为：
#!/bin/bash
#启动zookeeper
 /lwb/kafka/kafka_2.13-2.7.0/bin/zookeeper-server-start.sh  /lwb/kafka/kafka_2.13-2.7.0/config/zookeeper.properties &
 
sleep 3  #默默等3秒后执行 

#启动kafka
 /lwb/kafka/kafka_2.13-2.7.0/bin/kafka-server-start.sh /lwb/kafka/kafka_2.13-2.7.0/config/server.properties &

~~~

# Linux



### 启动Zookeeper

~~~
bin/zookeeper-server-start.sh ./config/zookeeper.properties
~~~



### 启动Kafka

~~~
bin/kafka-server-start.sh ./config/server.properties
~~~

### 创建一个Topic

~~~
bin/kafka-topics.sh --create --topic quickstart-events --bootstrap-server 127.0.0.1:9092
~~~



~~~
bin/kafka-topics.sh --create --topic quickstart-events --bootstrap-server 182.92.83.153:9092
~~~



### 关闭Kafka

~~~
bin/kafka-server-stop.sh
~~~

### 关闭zookeeper

~~~
bin/zookeeper-server-stop.sh
~~~

### 看启动没有

~~~
sudo lsof -i:9092
~~~



# Windows

### 启动zookeeper

~~~
bin\windows\zookeeper-server-start.bat .\config\zookeeper.properties
~~~

### 启动Kafka

~~~
bin\windows\kafka-server-start.bat .\config\server.properties
~~~

### 创建Topic，显示数据

~~~
bin\windows\kafka-topics.bat --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test
~~~

### 显示所有Topic的列表

~~~
bin\windows\kafka-topics.bat --list --zookeeper localhost:2181 
~~~

### 查看Topic的数据

~~~
bin\windows\kafka-console-consumer.bat --bootstrap-server 127.0.0.1:9092 --topic risk_warning_test --from-beginning
~~~

