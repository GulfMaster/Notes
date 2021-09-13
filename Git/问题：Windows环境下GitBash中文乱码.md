# 问题：Windows环境下GitBash中文乱码

之前很少用GitBash，一直用的Idea进行git操作。最近开始写GitHub写东西，GitBash一直是乱码的，觉得很不舒服，乱码确实影响我们对操作的认知。遂决定解决此问题。

网上查找资料，经过实践，总结以下解决方法。

---

## Setp1

运行Git Bash窗口，在窗口中右键。选择Options，点击左侧的Text，在右侧找到Locale和Character set
　　Locale : 选择 zh_CN 
　　Character set:选择 UTF-8 

## Step2

到Git Bash命令窗口输入如下设置命令语句

~~~
git config --global i18n.commitencoding utf-8 --注释：该命令表示提交命令的时候使用utf-8编码集提交

git config --global i18n.logoutputencoding utf-8 --注释：该命令表示日志输出时使用utf-8编码集显示

export LESSCHARSET=utf-8 --注释：设置LESS字符集为utf-8
~~~



此时，GitBsh中的提交记录和日志都正常显示了。

如果你的计算机名称是中文，或git的文件夹中有中文。在命令行输入界面还是会乱码（仅仅是界面上有一部分数据会乱码）。

如果上一行的情况都没有的话，到**Step2**就结束了，如果有的话，还需最后一步。



## Setp3

打开控制面板，选择更改日期、时间或数字格式

之后选择 **管理** > **更改系统区域设置** > **Beta版: 使用Unicode UTF-8提供全球语言支持(U)**

之后重启电脑，即完整解决此问题。







书于2021年9月13日
