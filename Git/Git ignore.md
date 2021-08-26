# 解决git-忽略文件，添加gitignore，处理已经track的文件

**1. 问题**
    我在一开始创建项目的时候没有意识到要忽略文件，把所有文件都track了，此时如果只添加.gitignore就不会生效。 gitignore只对未track的文件生效，对已经track的文件不生效。对于已经track的文件，直接添加gitignore文件是不够的，还需要额外的操作。

**2. 解决方案**
按以下步骤解决： 
:one:在项目的Git bash执行以下命令(加 -f  表示强制  )清除对所有文件的追踪，最后的点代表操作对象是所有文件。 

```
git rm -r -f --cache .
```

:two: 在项目根目录下和App目录下添加.gitignore文件： 

```
touch .gitignore
```

 加入如下内容:

```
.idea
out
*.iml
```

:three: 在git bash中执行

```
git add .
```

此时gitignore就会生效，按照配置忽略

:four:在git bash中执行

```
git commit -m "add gitignore"
```

提交修改即可。