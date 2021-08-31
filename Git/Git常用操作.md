# 从github拉取代码之后

~~~
创建本地分支
git branch -b master

设置本地分支追踪远程分支
git push --set-upstream origin master

把文件放到暂存区
git add .

提交变更到暂存区
git commit -m "commit message"

推送代码
git push -u origin master
~~~







# 切换分支

~~~
查看远程分支
git branch -a

查看本地分支
git branch

切换到dev分支
git checkout dev
~~~



# 将add的文件撤销

~~~
git restore --staged <file>...
~~~



# 查看用户名、邮箱

~~~
git config user.name
git config user.email
~~~

