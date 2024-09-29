###### 导入 GPG 密钥
```bash
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
```
###### 添加 Kibana 仓库
```bash
echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-7.x.list
```
###### 更新软件包列表
```bash
apt update
```
###### 安装 Kibana
```bash
apt install kibana
```
###### 启动和启用 Kibana
```bash
systemctl start kibana
systemctl enable kibana
```
###### 验证安装
```bash
curl -X GET "localhost:5601/"
```

###### 配置
- /etc/kibana/kibana.yml
```bash
# 允许外部访问
server.host: "0.0.0.0"
# 端口配置
server.port: 5601
# 配置 elasticsearch 地址
elasticsearch.hosts: ["http://localhost:9200"]
# 如果 Elasticsearch 运行在不同的主机或 IP 地址上，请将 localhost 替换为相应的地址。例如
elasticsearch.hosts: ["http://192.168.1.12:9200"]
# 配置身份验证(如果需要)
elasticsearch.username: "elastic"  # 替换为您的用户名
elasticsearch.password: "your_password"  # 替换为您的密码
# 本地化
i18n.locale: "zh-CN"
```
###### 卸载
```bash
# 停止服务
systemctl stop kibana
# 卸载
apt remove --purge kibana
# 删除篇日志文件
rm -rf /etc/kibana
# 删除 kibana 仓库
rm /etc/apt/sources.list.d/elastic-7.x.list
# 更新软件包列表
apt update
```