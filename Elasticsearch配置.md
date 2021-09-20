
# 创建es用户并设置密码

~~~
useradd elasticsearch
passwd elasticsearch
Lwb@9527
~~~



- **修改Linux系统的限制配置**

1. 修改系统中允许应用最多创建多少文件等的限制权限。Linux默认来说，一般限制应用最多创建的文件是65535个。但是ES至少需要65536的文件创建权限。
2. 修改系统中允许用户启动的进程开启多少个线程。默认的Linux限制root用户开启的进程可以开启任意数量的线程，其他用户开启的进程可以开启1024个线程。必须修改限制数为4096+。因为ES至少需要4096的线程池预备。ES在5.x版本之后，强制要求在linux中不能使用root用户启动ES进程。所以必须使用其他用户启动ES进程才可以。
3. Linux低版本内核为线程分配的内存是128K。4.x版本的内核分配的内存更大。如果虚拟机的内存是1G，最多只能开启3000+个线程数。至少为虚拟机分配1.5G以上的内存。

修改如下配置

```bash
[root@VM-0-14-centos elasticsearch-7.12.0]# vi /etc/security/limits.conf

elasticsearch soft nofile 65536
elasticsearch hard nofile 65536
elasticsearch soft nproc 4096
elasticsearch hard nproc 4096
  
```

# 启动ES

~~~
#修改目录权限至新增的elasticsearch用户
chown -R elasticsearch /lwb/es/elasticsearch-7.10.2


# 增加data和log存放区，并赋予elasticsearch用户权限
[root@VM-0-14-centos elasticsearch-7.12.0]# mkdir -p /data/es
[root@VM-0-14-centos elasticsearch-7.12.0]# chown -R elasticsearch /data/es
[root@VM-0-14-centos elasticsearch-7.12.0]# mkdir -p /var/log/es
[root@VM-0-14-centos elasticsearch-7.12.0]# chown -R elasticsearch /var/log/es


su elasticsearch
bin/elasticsearch -d

#查看es是否启动
netstat -ntlp | grep 9200
curl 127.0.0.1:9200
~~~

然后修改上述的data和log路径，`vi /opt/elasticsearch-7.12.0/config/elasticsearch.yml`

```bash
# ----------------------------------- Paths ------------------------------------
#
# Path to directory where to store the data (separate multiple locations by comma):
#
path.data: /data/es
#
# Path to log files:
#
path.logs: /var/log/es
```



# 启动Kibana

~~~
修改目录权限
[root@VM-0-14-centos opt]# chown -R elasticsearch /lwb/es/kibana-7.10.2-linux-x86_64
#配置Kibana的远程访问
[root@VM-0-14-centos opt]# vi /lwb/es/kibana-7.10.2-linux-x86_64/config/kibana.yml
server.host: 0.0.0.0

su elasticsearch
cd /lwb/es/kibana-7.10.2-linux-x86_64
./bin/kibana

#账号&密码
elastic
liwenbo@123456
~~~



# 关闭

~~~
ps -ef|grep kibana
 
ps -ef|grep 5601
 
都找不到 
 
尝试 使用  lsof -i:5601
 
kill -9  端口
 
启动即可 ./kibana
~~~

