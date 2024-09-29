**安装
```bash
dokcer run --detach \
--name mysql \
--publish 3306:3306 \
--restart always \
--env MYSQL_ROOT_PASSWORD=123456 \
--env TZ=Asia/Shanghai \
--volume $HOME/.mysql/conf.d:/etc/mysql/conf.d \
--volume $HOME/.mysql/data:/var/lib/mysql \
mysql:latest
```