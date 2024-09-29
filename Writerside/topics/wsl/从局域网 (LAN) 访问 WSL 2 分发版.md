- 下面是使用  [Netsh 接口 portproxy](https://learn.microsoft.com/zh-cn/windows-server/networking/technologies/netsh/netsh-interface-portproxy)  Windows 命令添加端口代理的示例，该代理侦听主机端口并将该端口代理连接到 WSL 2 VM 的 IP 地址
```powershell
netsh interface portproxy add v4tov4 listenport=<yourPortToForward> listenaddress=0.0.0.0 connectport=<yourPortToConnectToInWSL> connectaddress=(wsl hostname -I)
```
- 在此示例中，需要更新  `<yourPortToForward>`  到端口号，例如  `listenport=4000`。  `listenaddress=0.0.0.0`  表示将接受来自任何 IP 地址的传入请求。 侦听地址指定要侦听的 IPv4 地址，可以更改为以下值：IP 地址、计算机 NetBIOS 名称或计算机 DNS 名称。 如果未指定地址，则默认值为本地计算机。 需要将  `<yourPortToConnectToInWSL>`  值更新为希望 WSL 连接的端口号，例如  `connectport=4000`。 最后，`connectaddress`  值必须是通过 WSL 2 安装的 Linux 分发版的 IP 地址（WSL 2 VM 地址），可通过输入命令：`wsl.exe hostname -I`  找到。
- 要获取 IP 地址，请使用：
	- - `wsl hostname -I`  标识通过 WSL 2 安装的 Linux 分发版 IP 地址（WSL 2 VM 地址）
	- - `cat /etc/resolv.conf`  表示从 WSL 2 看到的 WINDOWS 计算机的 IP 地址 (WSL 2 VM)
- 使用  `listenaddress=0.0.0.0`  将侦听所有  [IPv4 端口](https://stackoverflow.com/questions/9987409/want-to-know-what-is-ipv4-and-ipv6#:%7E:text=The%20basic%20difference%20is%20the,whereas%20IPv6%20has%20128%20bits.)。
