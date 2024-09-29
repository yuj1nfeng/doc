###### 安装

```shell
# 更新系统包列表
apt update -y
# 安装 Redis
apt install redis-server
# 如果服务没有自动启动，可以手动启动
systemctl start redis-server
# 设置 Redis 开机自启
systemctl enable redis-server
# 验证 Redis 是否正常工作
redis-cli ping
# 查看服务状态
systemctl status redis-server
```

###### 配置文件

-   Redis   的主配置文件位于   /etc/redis/redis.conf

```shell
# 修改配置文件
## 取消这行的注释，并将  your_strong_password  替换为你想要的强密码：
requirepass your_strong_password
## 修改bind
bind 127.0.0.1 改成 bind 0.0.0.0
## 确保  protected-mode  设置为  no
protected-mode no

```

###### 防火墙

```shell
ufw allow 6379
```
