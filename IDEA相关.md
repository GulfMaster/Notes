[TOC]

# 常用快捷键

Shift*2	万能搜索

CTRL+N	搜索所有类

Alt+F7	查询该类的被引用情况

CTRL+O	返回待实现方法

Shift+F6修改文件名称



# 常见问题及解决方法

- 清除DNS缓存

  - ~~~
    ipconfig /flushdns
    ~~~

  

- 重置 Winsock 目录
  - ~~~
    netsh winsock reset
    ~~~

  -  ~~~
    netsh int ipv4 set dynamicport tcp start=49152 num=16383
    netsh int ipv4 set dynamicport udp start=49152 num=16383
    ~~~



# 必备设置

- ## **设置File and Code Templates**

  位置: File>Settings>Editor>File and Code Templates

  设置 Class|Interface|Enum|Annotation

  取消勾选Reformat according to style

  ~~~java
  
  /**
   * @author: liwenbo
   * @date: ${YEAR}-${MONTH}-${DAY} ${HOUR}:${MINUTE}:${SECOND}
   * 
   * @desc: 
   */
  ~~~

- ## **设置Live Templates**

  位置: File>Settings>Editor>Live Templates

~~~
Abbreviation: time
Description: 快速插入当前时间
Template Text: $date$
Edit Variable: 
	name: date
	expression: date("yyyy-MM-dd hh:mm:ss")
作用范围：全局
~~~

~~~
Abbreviation: anno
Description: 快速插入注释
Template Text: 

/**
 * @author: liwenbo
 * @date: $date$
 * 
 * @desc: $END$
 */
 
Edit Variable: 
	name: date
	expression: date("yyyy-MM-dd hh:mm:ss")
	Skip If Defined: true
作用范围：全局
~~~

- 打印日志设置

  ~~~
  Abbreviation: log
  Description: 快速插入Logger
  Template Text: 
  private static final Logger logger = LoggerFactory.getLogger($className$.class);
  
   
  Edit Variable: 
  	name: className
  	expression: className()
  	Skip If Defined: true
  作用范围：Java
  ~~~

  

# 常用插件

~~~
Free Mybatis Plus
mybatis-plus
Lombok
Alibaba Java Coding Guidelines
FindBugs
VisualVM Launcher
translate
CodeGlance
~~~
