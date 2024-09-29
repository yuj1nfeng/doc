**安装

```bash
docker run --deatch \
--name redis \
--publish 6379:6379 \
--restart always \
redis --requirepass 123456
```
