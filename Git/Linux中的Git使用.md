[toc]

# 一， linux安装Git

[git官方文档](https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git)

~~~
 yum -y install git
 rpm -qa|grep git
 rpm -ql git
 whereis git
~~~

## 1.1 检查是否已安装git，若有则卸载

~~~
// 查看当前git版本
# git --version
git version 1.7.1

// 卸载旧版本
# yum remove -y git
~~~

## 1.2 安装依赖包，下载最新版git源码

~~~
yum install -y curl-devel expat-devel gettext-devel openssl-devel zlib-devel perl-devel
wget https://github.com/git/git/archive/v2.13.2.tar.gz
tar zxf v2.13.2.tar.gz
~~~

## 1.3 安装git，配置环境变量

~~~
cd git-2.13.2
make prefix=/usr/local/git all
make prefix=/usr/local/git install
echo "export PATH=$PATH:/usr/local/git/bin" >> /etc/bashrc
source /etc/bashrc    // 实时生效 
~~~

## 1.4 查看git版本号，确认是否安装成功

~~~
# git --version
~~~

## 1.5 配置git用户名和邮箱

~~~
git config --global user.name 'liwenbo'
git config --global user.email '17751002310@189.cn'
~~~



# 二，服务器设置

## 2.1添加git用户，并修改密码

~~~
useradd git
passwd git
~~~

## 2.2 初始化一个项目目录为一个仓库

~~~
su git
//git的~的实际地址为/home/git
cd ~
//yourName为自定义的仓库名称
mkdir yourName.git
cd yourName.git
git init --bare
~~~



# 三，客户端操作

## 3.1Win10下配置远端

~~~
ssh://git@182.92.83.153/home/git/repo1
~~~

## 3.2之后常规操作即可