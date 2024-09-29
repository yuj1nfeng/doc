### 基本语法
```sh
wget [选项]... [URL]...
```

### 主要参数

1. **基本配置**
   - `-O, --output-file=FILE`: 指定输出文件的名称。
     ```sh
     wget -O output.txt https://example.com/file.txt
     ```
   - `--no-check-certificate`: 忽略 SSL 证书验证，适用于不安全的 HTTPS 连接。
     ```sh
     wget --no-check-certificate https://example.com/file.txt
     ```

2. **重试机制**
   - `-t, --tries=NUMBER`: 设置最大重试次数（默认为20）。
     ```sh
     wget -t 5 https://example.com/file.txt
     ```
   - `--retry-connrefused`: 在连接被拒绝时重新尝试下载。
     ```sh
     wget --retry-connrefused https://example.com/file.txt
     ```

3. **代理设置**
   - `-e, --proxy=PROXY[:PORT]`: 设置HTTP或HTTPS代理服务器。
     ```sh
     wget -e http-proxy=http://10.10.1.10:3128 https://example.com/file.txt
     ```
   - `--no-proxy`: 关闭所有代理设置。
     ```sh
     wget --no-proxy https://example.com/file.txt
     ```

4. **下载选项**
   - `-c, --continue`: 恢复中断的下载（需要服务器支持）。
     ```sh
     wget -c https://example.com/file.txt
     ```
   - `--start-pos=OFFSET`: 从指定位置开始断点续传。
     ```sh
     wget --start-pos=1024 https://example.com/file.txt
     ```

5. **输出信息**
   - `-q, --quiet`: 不显示进度和消息，仅显示错误信息。
     ```sh
     wget -q https://example.com/file.txt
     ```
   - `--verbose`: 显示详细信息（默认行为）。
     ```sh
     wget --verbose https://example.com/file.txt
     ```

6. **认证**
   - `--http-user=USER`: 设置HTTP用户名。
     ```sh
     wget --http-user=myuser https://example.com/file.txt
     ```
   - `--http-password=PASSWORD`: 设置HTTP密码。
     ```sh
     wget --http-password=mypassword https://example.com/file.txt
     ```

7. **代理认证**
   - `--proxy-user=USER`: 设置代理用户名。
     ```sh
     wget --proxy-user=myproxyuser http://10.10.1.10:3128/https://example.com/file.txt
     ```
   - `--proxy-password=PASSWORD`: 设置代理密码。
     ```sh
     wget --proxy-password=myproxypassword http://10.10.1.10:3128/https://example.com/file.txt
     ```

8. **下载控制**
   - `-w, --wait=SECONDS`: 两次请求之间等待的秒数。
     ```sh
     wget -w 5 https://example.com/file.txt
     ```
   - `--random-wait`: 随机等待几秒钟，以模拟用户行为。
     ```sh
     wget --random-wait https://example.com/file.txt
     ```

9. **文件名处理**
   - `-nd, --no-directories`: 将远程目录结构转换为本地目录结构。
     ```sh
     wget -nd https://example.com/directory/file.txt
     ```
   - `--directory-prefix=PREFIX`: 设置下载的文件存放在指定的目录下。
     ```sh
     wget --directory-prefix=/path/to/download https://example.com/file.txt
     ```

10. **断点续传**
    - `-c, --continue`: 续传（需要服务器支持）。
      ```sh
      wget -c https://example.com/file.txt
      ```
    - `--start-pos=OFFSET`: 从指定位置开始断点续传。
      ```sh
      wget --start-pos=1024 https://example.com/file.txt
      ```

### 示例
```sh
# 下载文件并重命名为output.txt
wget -O output.txt https://example.com/file.txt

# 恢复中断的下载
wget -c https://example.com/file.txt

# 设置HTTP代理服务器
wget -e http-proxy=http://10.10.1.10:3128 https://example.com/file.txt

# 设置认证信息
wget --http-user=myuser --http-password=mypassword https://example.com/file.txt

# 设置等待时间
wget -w 5 https://example.com/file.txt
```

这些参数可以帮助你更灵活地控制 `wget` 的下载行为。如果你有特定的需求，可以结合使用不同的参数来实现复杂的下载任务。
