# MySQL

[toc]



## 常用函数

### 平均值 SELECT AVG(column_name) FROM table_name

### 【四舍五入取整截取】

select round(54.56,0)

###  【向下取整截取】

SELECT FLOOR(54.56)


## 时间与字符串
### 时间转字符串：

DATE_FORMAT(日期，格式字符串)

SELECT DATE_FORMAT(NOW(), '%Y-%m-%d %H:%i:%s');--now()为当期时间

--结果：2019-08-20 20:40:08

### 字符串转时间：

STR_TO_DATE(字符串，日志格式)

SELECT STR_TO_DATE('2019-08-20 20:40:08', '%Y-%m-%d %H:%i');

--结果：2019-08-20 20:40:00

### 时间转时间戳：

select unix_timestamp(now());--now()为当期时间

--结果：1566304856

### 字符串转时间戳：

select unix_timestamp('2019-08-20');

--结果：1566230400

### 时间戳转字符串：

select from_unixtime(1566230400,'%Y-%m-%d');

--结果：2019-08-20

### 附表

<img src="MySQL\时间字符串.png" width="500" height="900">



## 时间函数

~~~sql
SELECT end_time FROM chuhe WHERE end_time BETWEEN STR_TO_DATE('2020-07-20 16', '%Y-%m-%d %H:%i') AND DATE_ADD(STR_TO_DATE('2020-07-20 16', '%Y-%m-%d %H:%i'),INTERVAL 1 HOUR)
~~~

select date_add(日期, interval 1 day); 日期加天
select date_add(日期, interval 1 hour); 日期加小时
select date_add(日期, interval 1 minute); 日期加分
select date_add(日期, interval 1 second);日期加秒
select date_add(日期, interval 1 microsecond); 日期加微秒
select date_add(日期, interval 1 week); 日期加周
select date_add(日期, interval 1 month); 日期加月
select date_add(日期, interval 1 quarter); 日期加季度
select date_add(日期, interval 1 year); 日期加年



## 字符串截取

1、left（name,4）截取左边的4个字符

　　列： `SELECT LEFT(201809,4) 年`

　　结果：2018

2、right（name,2）截取右边的2个字符

```
  SELECT RIGHT(201809,2) 月份
```

　  结果：09

3、SUBSTRING(name,5,3) 截取name这个字段 从第五个字符开始 只截取之后的3个字符

```
　　SELECT SUBSTRING('成都融资事业部',5,3)
```

　　结果：事业部

4、SUBSTRING(name,3) 截取name这个字段 从第三个字符开始，之后的所有个字符

```
　　SELECT SUBSTRING('成都融资事业部',3)
```

　　结果：融资事业部

5、SUBSTRING(name, -4) 截取name这个字段的第 4 个字符位置（倒数）开始取，直到结束

```
　　SELECT SUBSTRING('成都融资事业部',-4)
```

　　结果：资事业部

6、SUBSTRING(name, -4，2) 截取name这个字段的第 4 个字符位置（倒数）开始取，只截取之后的2个字符

```
　　SELECT SUBSTRING('成都融资事业部',-4,2)
```

　　结果：资事

　　注意：我们注意到在函数 substring(str,pos, len)中， pos 可以是负值，但 len 不能取负值。

7、substring_index('www.baidu.com', '.', 2) 截取第二个 '.' 之前的所有字符

```
　　SELECT substring_index('www.baidu.com', '.', 2)
```

　　结果：[www.baidu](http://www.baidu/)

8、substring_index('www.baidu.com', '.', -2) 截取第二个 '.' （倒数）之后的所有字符

```
　　SELECT substring_index('www.baidu.com', '.', -2)
```

　　结果：baidu.com

9、SUBSTR(name, 1, CHAR_LENGTH(name)-3) 截取name字段，取除name字段后三位的所有字符

```
　　SELECT SUBSTR('成都融资事业部', 1, CHAR_LENGTH('成都融资事业部')-3)
```

　　结果：成都融资



## 显示行号

~~~sql
set @rank=0;
SELECT (@rank := @rank + 1) AS rownum FROM chuhe LIMIT 10
~~~



# 特殊情况

## 字符串的百分比排序

~~~
方法一：ORDER BY '123'+0;（首推）

方法二：ORDER BY '123'*1; 
方法三：ORDER BY CAST('123' AS SIGNED);
方法四：ORDER BY CONVERT('123',SIGNED);
~~~

