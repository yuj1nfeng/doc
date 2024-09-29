###### 导入 Elasticsearch 的 GPG 密钥
```bash
wget -qO - https://artifacts.elastic.co/GPG-KEY-elast
```
###### 添加 Elasticsearch 仓库
```bash
echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | tee -a /etc/apt/sources.list.d/elastic-7.x.list
```
###### 更新软件包列表
```bash
apt update
```
###### 安装 Elasticsearch
```bash
apt install elasticsearch
```
###### 启动和启用 Elasticsearch
```bash
systemctl start elasticsearch
systemctl enable elasticsearch
```
###### 验证安装
```bash
curl -X GET "localhost:9200/"
```

###### 配置
- /etc/elasticsearch/elasticsearch.yml

- 修改网络配置
```yml
# 允许所有网络接口访问
network.host: 0.0.0.0        
# 或者替换为您的服务器 IP,允许局域网访问
network.host: 192.168.1.100  
http.port: 9200              # 可选
# 适合生产环境的发现设置
discovery.seed_hosts: ["192.168.1.188"]  # 替换为您的节点 IP
cluster.initial_master_nodes: ["master"]  # 替换为您的主节点名称
# 启用安全配置
xpack.security.enabled: true
xpack.security.transport.ssl.enabled: true
```
- 设置密码
```bash
/usr/share/elasticsearch/bin/elasticsearch-setup-passwords interactive
```

###### 卸载
```bash
# 停止服务
systemctl stop elasticsearch
# 卸载
apt remove --purge elasticsearch
# 删除配置文件和数据
rm -rf /etc/elasticsearch
rm -rf /var/lib/elasticsearch
rm -rf /var/log/elasticsearch
# 删除 elasticsearch 仓库
rm /etc/apt/sources.list.d/elastic-7.x.list
# 更新软件包列表
apt update
```
