- Nmap 基本语法

```
nmap [ <扫描类型> ...] [ <选项> ] { <扫描目标说明> }
```

- 全面进攻性扫描（包括各种主机发现、端口扫描、版本扫描、OS扫描及默认脚本扫描）:

```
nmap -A -v target_ip
```

- Ping扫描:

```
nmap -sn -v target_ip
```

- 快速端口扫描:

```
nmap -F -v target_ip
```

例子

~~~
TCP SYN扫描
nmap -sS 61.147.13.114
TCP connect()扫描
nmap -sT 61.147.13.114
UDP扫描
nmap -sU 61.147.13.114
-sN; -sF; -sX (TCP Null，FIN，and Xmas扫描)
nmap -sN 61.147.13.114
~~~



- 版本扫描:

```
nmap -sV -v target_ip 
```

- 操作系统扫描:

```
nmap -O -v target_ip
```

- 运行标记为safe的nse script

```
nmap -sC -v target_ip
```