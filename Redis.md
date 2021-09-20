### 配置文件修改

~~~
取消注释
# bind 127.0.0.1

修改requirepass
yes为no
~~~



### 启动Redis

~~~
./src/redis-server redis.conf
~~~

### 启动客户端

~~~
./src/redis-cli
~~~
### 验证密码

~~~
auth Lwb@123456
~~~


### 关闭Redis

~~~
图形界面Ctrl+c

./src/redis-cli输入shutdown
~~~



## 常用操作

清空所有数据

~~~
flushall
~~~

查询key

~~~
keys xxx*
~~~

删除key

~~~
del xxx
~~~



### 设置密码

~~~
 config set requirepass Lwb@123456
~~~

### 查询密码

~~~
config get requirepass
~~~







