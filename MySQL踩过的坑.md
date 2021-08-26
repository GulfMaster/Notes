# 对新用户增删改

~~~
1.创建用户:
# 指定ip：192.118.1.1的用户登录
create user 'wenbo'@'192.118.1.1' identified by 'Lwb2597721727';
# 指定ip：192.118.1.开头的用户登录
create user 'wenbo'@'192.118.1.%' identified by 'Lwb2597721727';
# 指定任何ip的用户登录
create user 'wenbo'@'%' identified by 'Lwb2597721727';

2.删除用户
drop user '用户名'@'IP地址';

3.修改用户
rename user '用户名'@'IP地址' to '新用户名'@'IP地址';

4.修改密码
set password for '用户名'@'IP地址'=Password('新密码');
~~~





# 对当前的用户授权管理

~~~
#查看权限
show grants for '用户'@'IP地址'

#授权wenbo用户仅对db1.t1文件有查询、插入和更新的操作
grant select ,insert,update on db1.t1 to "wenbo"@'%';

# 表示有所有的权限，除了grant这个命令，这个命令是root才有的。wenbo用户对db1下的t1文件有任意操作
grant all privileges  on db1.t1 to "wenbo"@'%';
#wenbo用户对db1数据库中的文件执行任何操作
grant all privileges  on db1.* to "wenbo"@'%';
#wenbo用户对所有数据库中文件有任何操作
grant all privileges  on *.*  to "wenbo"@'%';
 
#取消权限
 
# 取消mjj用户对db1的t1文件的任意操作
revoke all on db1.t1 from 'wenbo'@"%";  

# 取消来自远程服务器的mjj用户对数据库db1的所有表的所有权限

revoke all on db1.* from 'wenbo'@"%";  

取消来自远程服务器的mjj用户所有数据库的所有的表的权限
revoke all privileges on *.* from 'wenbo'@'%';
~~~

