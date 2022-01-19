

### tar

```shell
# 排除命令
tar --exclude=node_modules --exclude='.git' -zcvf demo.tar.gz demo
```



### 替换文本

```shell
sed -i "s/dev_test.yaml/test.yaml/g"  vline_live/src/main.py
```



### 常用命令

##### 查看历史操作

```shell
➜  ~ history
```

##### dpkg

```shell
sudo dpkg -i deb
```

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



### awk

```shell
➜  ~ cat test.log
[2020-12-14 12:23:23,365] - [live_service.services.socketio_server] - [DEBUG] - [SocketIoServerManager process message: {'event': 'heartbeat', 'data': {'server_data': {'port': 8001, 'host': '0.0.0.0', 'has_admin_router': True, 'server_name': 'test_socket_server_1', 'server_path': 'http://54.223.205.242:8001'}, 'server_time': 1607919803355, 'msgId': 'f47c7a0a64b0423296360adbec8bfe0e'}}] - [socketio_server.py:59]
[2020-12-14 12:23:26,438] - [live_service.services.socketio_server] - [DEBUG] - [SocketIoServerManager process message: {'event': 'heartbeat', 'data': {'server_data': {'port': 8001, 'host': '0.0.0.0', 'has_admin_router': True, 'server_name': 'test_socket_server_1', 'server_path': 'http://54.223.205.242:8001'}, 'server_time': 1607919806360, 'msgId': 'ac625165d9f04ab291e5a5f920bf9fe5'}}] - [socketio_server.py:59]
[2020-12-14 12:23:29,410] - [live_service.services.socketio_server] - [DEBUG] - [SocketIoServerManager process message: {'event': 'heartbeat', 'data': {'server_data': {'port': 8001, 'host': '0.0.0.0', 'has_admin_router': True, 'server_name': 'test_socket_server_1', 'server_path': 'http://54.223.205.242:8001'}, 'server_time': 1607919809366, 'msgId': '699779a567a54ed5b095f6663ed8af3e'}}] - [socketio_server.py:59]
➜  ~
➜  ~ awk '{print $1, $2, $4}' test.log
[2020-12-14 12:23:23,365] [live_service.services.socketio_server]
[2020-12-14 12:23:26,438] [live_service.services.socketio_server]
[2020-12-14 12:23:29,410] [live_service.services.socketio_server]
➜  ~ # 输出最后一列
➜  ~ awk '{print $(NF-0)}' test.log
[socketio_server.py:59]
[socketio_server.py:59]
[socketio_server.py:59]
➜  ~ # 设置输出分隔符
➜  ~ awk -v OFS="|" '{print $1, $2, $4}' test.log
[2020-12-14|12:23:23,365]|[live_service.services.socketio_server]
[2020-12-14|12:23:26,438]|[live_service.services.socketio_server]
[2020-12-14|12:23:29,410]|[live_service.services.socketio_server]
➜  ~ # 多分隔符
➜  ~ awk -F '[][]' '{print $1, $2, $3, $4}' test.log
 2020-12-14 12:23:23,365  -  live_service.services.socketio_server
 2020-12-14 12:23:26,438  -  live_service.services.socketio_server
 2020-12-14 12:23:29,410  -  live_service.services.socketio_server
➜  ~ # 设置变量
➜  ~ awk -v time='时间:' -F '[][]' '{print time$2}' test.log
时间:2020-12-14 12:23:23,365
时间:2020-12-14 12:23:26,438
时间:2020-12-14 12:23:29,410
➜  ~ # 提取日志中 msgId
➜  ~ awk -F "msgId': '" '{print $2}' test.log | awk -F "'}" '{print $1}'
f47c7a0a64b0423296360adbec8bfe0e
ac625165d9f04ab291e5a5f920bf9fe5
699779a567a54ed5b095f6663ed8af3e
➜  ~
```



### 查找含有特定字符串的文件*grep*

```shell
root@iZwz95djn12xfvvkcs94hvZ:/etc/nginx/conf.d# grep -rn 9080 *
midas-developer.conf:8:    listen 9080;
root@iZwz95djn12xfvvkcs94hvZ:/etc/nginx/conf.d#



policy_group_id,ad_serving_tag
1000,test_ks
policy_group_id,ad_serving_tag
1001,test_gdt
policy_group_id,ad_serving_tag
1002,test_csj
policy_group_id,ad_serving_tag
1003,test_baidu

anchor_140359518@vshow-euc1.1-1.io
anchor_138470064@vshow-euc1.1-1.io
```



### crontabs

```shell
# 文件位置
sudo vi /var/spool/cron/crontabs/ubuntu
```





Flora_Tamanna,Calsa_SS,Ravi_Trishul,Ravi_King,Ravi_Blessing,Calsa_Deccan Clan,Calsa_Trust,Calsa_Jaimahakal,Calsa_SK,Ravi_OMG,Calsa_Meeru,Ravi_Shadow,Calsa_Ahmed,Calsa_Rampal,Calsa_AliRaza,Ravi_binashkari,Calsa_Shiva,Calsa_Honest,Calsa_Airone,Calsa_Ajal,Sean_Amitabh,Ravi_KR

