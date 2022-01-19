

### 新建配置文件

```shell
sudo vi /etc/systemd/system/demo.service
```

```shell
# demo.service
[Unit]
After=network.service

[Service]
ExecStart=/opt/init/demo-service.sh
User=ubuntu

[Install]
WantedBy=default.target
```

### 设置启动链接

```shell
sudo systemctl enable demo.service # 命令用于建立符号链接关系，相当于激活开机启动
```

### 启动服务

```shell
sudo systemctl start demo.service
```



### 查看状态

```shell
sudo systemctl status demo.service
```

