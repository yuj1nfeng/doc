###### 安装 Samba
```bash
apt update
apt install samba
```
###### 创建共享目录
```bash
mkdir -p /srv/samba/share
chown nobody:nogroup /srv/samba/share
chmod 0755 /srv/samba/share
```
###### 配置 Samba
- 编辑 Samba 配置文件 /etc/samba/smb.conf
```bash
vim /etc/samba/smb.conf
```
- 在文件末尾添加以下内容:
```conf
[share]
path = /srv/samba/share
browseable = yes
read only = no
guest ok = yes
```
###### 重启服务
```bash
systemctl restart smbd
systemctl enable smbd
```
###### 设置防火墙(如果启用了防火墙)
```bash
ufw allow 'Samba'
```
###### 访问共享
- 在  Windows 上，可以通过  //samba_ip/share  访问共享目录
- 在 Linux 上，可以使用以下命令挂载共享目录：
```bash
mount -t cifs //samba_ip/share /mnt -o guest
```


###### windows 系统将 SMB 共享挂载到本地磁盘
一、打开 “此电脑”
在 Windows 桌面上找到并打开 “此电脑”。
二、映射网络驱动器
在 “此电脑” 窗口中，点击菜单栏中的 “计算机” 选项卡，然后选择 “映射网络驱动器”。
三、设置映射
在弹出的 “映射网络驱动器” 窗口中，选择一个未被占用的驱动器盘符，比如 “Z:” 等。
在 “文件夹” 一栏中，输入 SMB 共享的路径格式为 “\ 服务器地址 \ 共享文件夹名称”。例如，如果服务器地址是 192.168.1.100，共享文件夹是 data，则输入 “\192.168.1.100\data”。
可以根据需要勾选 “登录时重新连接”，这样在每次系统启动时会自动重新连接该网络驱动器。
四、提供凭证（如果需要）
如果访问 SMB 共享需要用户名和密码，系统会在点击 “完成” 后弹出一个对话框要求输入用户名和密码。输入具有访问权限的用户名和密码后点击确定。
完成上述步骤后，SMB 共享就会被映射为本地磁盘，可以像访问本地磁盘一样访问该共享文件夹