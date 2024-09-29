###### 安装

```shell
# 更新系统包列表
apt update
# 安装MySQL服务
apt install mysql-server
# 检查服务状态
systemctl status mysql
# 启动服务
systemctl start mysql
# 停止服务
systemctl stop mysql
# 重启服务
systemctl restart mysql
# 设置开机启动
systemctl enable mysql
# 检查开机启动状态
systemctl is-enabled mysql
# 卸载
## 停止mysql服务
systemctl stop mysql
## 卸载mysql包
apt remove mysql-server mysql-client mysql-common
## 卸载额外的依赖包
apt autoremove
## 清除 MySQL 配置文件
apt purge mysql-server mysql-client mysql-common
## 删除 MySQL 数据目录
rm -rf /var/lib/mysql
rm -rf /etc/mysql
## 删除MySQL日志文件
rm -rf /var/log/mysql
## 删除MySQL用户和组
deluser mysql
delgroup mysql
## 更新软件包
apt update
## 清理不在需要的软件包
sudo apt autoremove
## 检查是否还有任何MySQL相关包
dpkg -l | grep mysql
## 如果列出了任何包使用 apt remove 命令删除它们

```

###### 连接 MySQL

```shell
# 连接mysql
mysql -u root -p
```

###### 修改密码

```shell
# 初始设置
mysqladmin -u root password 'new_password'
## 如果已有密码
mysqladmin -u root -p'old_password' password 'new_password'
```

###### 防火墙

```shell
ufw allow 3306
```

###### 允许远程连接

-   修改 MySQL 配置文件
-   某些 MySQL 版本或发行版可能使用不同的配置文件位置
-   /etc/mysql/mysql.conf.d/mysqld.cnf
-   /etc/mysql/my.cnf
-   /etc/my.cnf

```ini
bind-address = 127.0.0.1 改成  bind-address = 0.0.0.0  或者直接注释掉这一行
```

###### 创建远程用户

```sql
-- 创建用户
create user 'username'@'%' identified by 'password' ;
-- 或者修改现有用户
update mysql.user set host='%' where user = 'username';
-- 授权
grant all privileges on *.* to 'username'@'%' with grant option;
-- 刷新权限
flush privileges;
-- 退出MySQL
exit;
```
