查看所有分支

git branch -a



发现本地commit没有提交到远程分支上



切换分支

git checkout master  

合并分支

git merge br(这里换成你的分支名字)

删除本地分支（当前分支已经没用了，记得删除，如果你还要用就不要删除了）

git branch -d br

推送

git push -u origin master 