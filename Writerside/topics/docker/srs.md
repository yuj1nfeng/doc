**安装

```bash
docker run --detach \
--name srs \
--restart always \
--publish 1935:1935/tcp --publish 1935:1935/udp \
--publish 80:80/tcp --publish 80:80/udp \
--publish 8080:8080/tcp --publish 8080:8080/udp \
--publish 8088:8088/tcp --publish 8088:8088/udp \
	ossrs/srs
```
