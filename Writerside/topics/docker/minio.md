**安装
```bash
docker run --detach \
--name minio \
--restartalways \
--publish 9000:9000 \
--publish 9001:9001 \
--volume $HOME/.minio/data:/data \
--volume $HOME/.minio/config:/root/.minio \
minio/minio server /data --console-address ":9001"
```