### 设置密码认证

```bash
#加上下面两行内容：
auth_basic "登陆验证";
auth_basic_user_file /etc/nginx/htpasswd;   #/etc/nginx/htpasswd是密码文件，路径自定义
```

