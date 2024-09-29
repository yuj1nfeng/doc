## 配置模板
```nginx
server {
    listen 80; # 监听80端口，可以根据需要改为443用于HTTPS

    server_name example.com; # 更换为你自己的域名

    location / {
        proxy_pass http://localhost:8080; # 转发到后端Java应用的地址和端口
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;

        # 可选：如果后端服务需要根据某些头信息做处理，可以在这里设置
        # 例如，下面这行告诉Spring Boot应用客户端实际使用的协议（HTTP或HTTPS）
        # proxy_set_header X-Forwarded-Proto https;
    }

    # 如果有静态资源直接由Nginx处理，可以添加如下配置
    # location /static/ {
    #     alias /path/to/static/files/;
    # }
}

# 如果有HTTPS配置，可以在这里添加
# server {
#     listen 443 ssl;
#     ...
#     # SSL证书和密钥的配置
# }
```
### 保存配置文件后,检查配置是否正确
```bash
sudo nginx -t
```
### 如果输出显示配置文件测试成功，重新加载或重启 Nginx 使配置生效
```bash
sudo nginx -s reload
```