###### 更新系统包列表:

```bash
apt update
```

###### 安装 Nginx:

```bash
apt install nginx
```

###### 启动 Nginx 服务:

```bash
systemctl start nginx
```

###### 设置 Nginx 开机自启:

```bash
systemctl enable nginx
```

###### 检查 Nginx 状态:

```bash
systemctl status nginx
```

###### 配置防火墙(如果启用了):

```bash
ufw allow 'Nginx Full'
```

###### 测试 Nginx 是否正常运行:

-   在浏览器中输入服务器的 IP 地址,应该能看到 Nginx 的默认欢迎页面。

###### Nginx 的主要配置文件位于:

-   /etc/nginx/nginx.conf
-   /etc/nginx/sites-available/default
-   如果您修改了配置,需要重新加载 Nginx:

###### 常用 Nginx 操作命令:

-   停止:

```bash
systemctl stop nginx
```

-   重启

```bash
systemctl restart nginx
```

-   重新加载配置:

```bash
sudo systemctl reload nginx
```

###### Nginx 日志文件位置:

-   访问日志: /var/log/nginx/access.log
-   错误日志: /var/log/nginx/error.log
