



### 常用命令

```
# 查看历史操作
history
# 安装
sudo dpkg -i deb
```



spluk



netstat -ntplu



Jps

Ravi_Manvi

### 添加任务计划

```shell
#vi /etc/crontab
```

crontab task 格式

\* * * * * user task
分 时 日 月 周 user task
字段 说明
1 分钟（0-59）
2 小时（2-24）
3 日期（1-31）
4 月份（1-12；或英文缩写Jan、Feb等）
5 周几（0-6，0为周日；或单词缩写Sun、Mon等）
6 用户名（执行命令时以此用户的身份）
7 要执行的命令（路径）



### join

1. 文件 test1

   ```
   a 11
   b 22
   c 33
   d 44
   ```

2. 文件 test2

   ```
   a 12
   b 13
   c 14
   h 20
   ```

##### 内连接

```shell
➜ join test1 test2
a 11 12
b 22 13
c 33 14
```

##### 左连接

```shell
➜ join -a1 test1 test2
a 11 12
b 22 13
c 33 14
d 44
```

##### 右连接 （注意输出结果）

```shell
➜ join -a2 test1 test2
a 11 12
b 22 13
c 33 14
h 20
```

##### 全连接（注意输出结果，无法判断第二列是test1还是test2的类容）

```shell
➜ join -a1 -a2 test1 test2
a 11 12
b 22 13
c 33 14
d 44
h 20
```

##### 指定分隔符

1. test1

   ```
   a,11
   b,22
   c,33
   d,44
   ```

2. test2

   ```
   a,12
   b,13
   c,14
   h,20
   ```

```shell
➜ join -t "," test1 test2
a,11,12
b,22,13
c,33,14
```





