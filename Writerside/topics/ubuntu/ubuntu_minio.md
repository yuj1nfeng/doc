###### 安装

```bash
# 更新系统包列表
apt update
# 安装必要的依赖
apt install wget curl software-properties-common
# 下载 MinIO  服务器
wget https://dl.min.io/server/minio/release/linux-amd64/minio
# 使  MinIO 可执行
chmod +x minio
# 移动 MinIO  到系统路径
sudo mv minio /usr/local/bin/
# 创建 MinIO  数据目录
sudo mkdir /mnt/data
# 启动,浏览器打开 http://your_ip:9001 初始密码 minioadmin:minioadmin
minio server /mnt/data --console-address ':9001'
```

###### 创建 MinIO 环境文件

-   注意用户名最少三个字符,密码至少 8 个字符,否则启动不了

```.env
## /etc/default/minio
MINIO_OPTS="--console-address :9001"
MINIO_ROOT_USER=admin
MINIO_ROOT_PASSWORD=your_strong_password
```

###### 创建 MinIO 系统服务文件

```.env
## /etc/systemd/system/minio.service
[Unit]
Description=MinIO
After=network.target

[Service]
EnvironmentFile=/etc/default/minio
ExecStart=/usr/local/bin/minio server $MINIO_OPTS /mnt/data
Restart=always
SendSIGKILL=no

[Install]
WantedBy=multi-user.target
```

###### 其他

```shell
## 设置
systemctl enable minio
## 查看有没有设置成功
systemctl is-enabled minio
## 启动
systemctl start minio
## 停止
systemctl stop minio
## 重启
systemctl restart minio
## 状态查看
systemctl status minio
```
