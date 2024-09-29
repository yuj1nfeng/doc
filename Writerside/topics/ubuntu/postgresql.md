###### 更新系统包列表

```bash
apt update
```

###### 安装 PostgreSQL

```bash
apt install postgresql postgresql-contrib
```

###### 启动和启用 PostgreSQL 服务

```bash
systemctl start postgresql
systemctl enable postgresql
```

###### 切换到 PostgreSQL 用户

```bash
sudo -i -u postgres
```

###### 访问 PostgreSQL 命令行界面

```bash
psql
```

###### 创建数据库和用户

-   创建数据库

```sql
create database mydatabase;
```

-   创建用户

```sql
create user myuser with encrypted password 'mypassword';
```

-   授予用户数据库权限

```sql
grant all privileges on database mydatabase to myuser;
```

-   退出 psql

```sql
\q
```

###### 授予权限

-   假设您的数据库名称是  mydatabase，用户是  myuser，您需要授予该用户对  public  模式的权限
-   切换到目标数据库

```sql
\c mydatabase
```

-   授予 public 模式的使用权限

```sql
grant usage on schema public to myuser;
```

-   授予 public 模式的所有权限

```sql
grant all privileges on schema public to myuser;
```

-   授予 public 模式中所有表的权限

```sql
grant all privileges on all tables in schema public to myuser;
```

-   授予 public 模式中所有序列的权限

```sql
grant all privileges on all sequences in schema on public to myuser;
```

-   退出 psql

```sql
\q
```

###### 配置远程访问

-   如果需要远程访问 PostgreSQL 数据库，您需要进行以下配置：
-   修改 postgresql.conf 文件
-   编辑 PostgreSQL 配置文件 postgresql.conf，允许 PostgreSQL 监听所有 IP 地址：

```bash
vim /etc/postgresql/12/main/postgresql.conf
```

-   找到并修改以下行：

```conf
#listen_addresses = 'localhost'
listen_addresses = '*'
```

-   修改 pg_hba.conf 文件

```bash
vim /etc/postgresql/12/main/pg_hba.conf
```

-   在文件末尾添加以下行（替换 your_subnet 为您的实际子网）：

```.conf
host    all             all             your_subnet/24          md5
```

-   如果需要允许所有地址能访问 0.0.0.0/0

###### 测试连接

```bash
psql -h localhost -U myuser -d mydatabase
```
