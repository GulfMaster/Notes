[toc]



# 一，Git安装与配置

## 1.1 Git安装

[Git下载](https://git-scm.com/download/win)

一路默认 

## 1.2 TortoseGit下载

[TortoiseGit下载](https://tortoisegit.org/)

[语言包下载](https://tortoisegit.org/download/)

![](..\img\Git学习\tortoiseGit语言包下载界面.png)





# 二，连接远程仓库

1. 在GitHub上创建仓库

2. 获取SSH密钥对

   Git Bush输入以下代码，之后一路回车。

~~~
ssh-keygen -t rsa
~~~

在C:\Users\Administrator\.ssh文件夹中会生成密钥对

- id_rsa文件是私钥
- id_rsa.pub是公钥

3. 修改GitHub上的SSH连接配置
   1. 点击徽标
   2. 点击设置
   3. 点击SSH and GPG keys
4. 推送
   1. Git Bush方式【SSH】

~~~
git remote add origin https://github.com/earthtraveller/threadDemo.git
git push -u origin master
~~~

之后输入账号密码，就ok了

​		2.TortoiseGit方式【SSH】

![](..\img\Git学习\tortoiseGit的SSH配置.png)

![配置远端](..\img\Git学习\配置远端.png)

右键Git同步，点击==推送==

![](..\img\Git学习\Git同步.png)

​	3.TortoiseGit方式【https】

![](..\img\Git学习\https方式.png)

右键Git同步，点击==推送==

# 3 克隆到本地

Git Bash方式【SSH】

~~~
 git clone git@github.com:earthtraveller/repo3.git
~~~

Git Bash方式【https】

~~~
git clone https://github.com/earthtraveller/repo2.git
~~~

Tortoise方式

右键Git克隆，输入网址



# 4 提交代码

点击Git提交
