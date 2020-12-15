

```json
ssh -L [local_bind_addr:]local_port:remote:remote_port middle_host

ssh -g -L 15672:127.0.0.1:15672 vline

其中"-L"选项表示本地端口转发，其工作方式为：在本地指定一个由ssh监听的转发端口(2222)，将远程主机的端口(host2:80)映射为本地端口(2222)，当有主机连接本地映射端口(2222)时，本地ssh就将此端口的数据包转发给中间主机(host3)，然后host3再与远程主机的端口(host2:80)通信。
```

```json

# 端口转发
Host vline_agency
HostName 54.223.205.242
User ubuntu
PreferredAuthentications publickey
IdentityFile ~/.ssh/keys/vline-lbe-bj.pem
LocalForward 5672 127.0.0.1:5672
LocalForward 15672 127.0.0.1:15672

```

