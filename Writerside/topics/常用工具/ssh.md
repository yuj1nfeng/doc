
## 生成密钥
```bash
ssh-keygen -t rsa -C youname@domain.com
```

## 免密登录
- linux
```bash
ssh-copy-id -i ~/.ssh/id_rda.pub root@120.0.0.1
```
- windows
```powershell
type $envUSERPROFILE/.ssh/id_rsa.pub | ssh 127.0.0.1 "cat >> .ssh/authorized_keys"
```
## 设置ssh默认终端为powershell
``` powershell
New-ItemProperty -Path "HKLM:\SOFTWARE\OpenSSH" -Name DefaultShell -Value "C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" -PropertyType String -Force
```
