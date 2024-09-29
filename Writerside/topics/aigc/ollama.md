### windows 部署
#### 下载 windows 安装包
![image.png](https://pic-1255826935.cos.ap-guangzhou.myqcloud.com/20240924172546.png)

#### 安装完成后打开终端
```bash
'[anaconda]'PS C:\Users\Administrator\projects> ollama
Usage:
  ollama [flags]
  ollama [command]

Available Commands:
  serve       Start ollama
  create      Create a model from a Modelfile
  show        Show information for a model
  run         Run a model
  pull        Pull a model from a registry
  push        Push a model to a registry
  list        List models
  ps          List running models
  cp          Copy a model
  rm          Remove a model
  help        Help about any command

Flags:
  -h, --help      help for ollama
  -v, --version   Show version information

Use "ollama [command] --help" for more information about a command.
```

#### 运行
```bash
'[anaconda]'PS C:\Users\Administrator\projects> ollama list
NAME            ID              SIZE    MODIFIED
gemma2:latest   ff02c3702f32    5.4 GB  15 minutes ago
qwen2.5:latest  845dbda0ea48    4.7 GB  16 minutes ago
llama3.1:latest 42182419e950    4.7 GB  38 minutes ago
llama3.1:8b     f66fc8dc39ea    4.7 GB  3 weeks ago
'[anaconda]'PS C:\Users\Administrator\projects> ollama run qwen2.5
>>> Send a message (/? for help)
```
#### 检查显卡支不支持
```bash
nvidia-smi
```
输出
```bash
Sun Sep 29 22:29:03 2024       
+-----------------------------------------------------------------------------------------+
| NVIDIA-SMI 561.09                 Driver Version: 561.09         CUDA Version: 12.6     |
|-----------------------------------------+------------------------+----------------------+
| GPU  Name                  Driver-Model | Bus-Id          Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |           Memory-Usage | GPU-Util  Compute M. |
|                                         |                        |               MIG M. |
|=========================================+========================+======================|
|   0  NVIDIA GeForce RTX 4060      WDDM  |   00000000:01:00.0  On |                  N/A |
| 30%   36C    P8             N/A /  115W |    1174MiB /   8188MiB |      2%      Default |
|                                         |                        |                  N/A |
+-----------------------------------------+------------------------+----------------------+

+-----------------------------------------------------------------------------------------+
| Processes:                                                                              |
|  GPU   GI   CI        PID   Type   Process name                              GPU Memory |
|        ID   ID                                                               Usage      |
|=========================================================================================|
|    0   N/A  N/A      1524    C+G   ...006.0_x64__8wekyb3d8bbwe\Photos.exe      N/A      |
|    0   N/A  N/A      1800    C+G   C:\Windows\System32\dwm.exe                 N/A      |
|    0   N/A  N/A      3576    C+G   ...crosoft\Edge\Application\msedge.exe      N/A      |
|    0   N/A  N/A      6776    C+G   ...s\System32\ApplicationFrameHost.exe      N/A      |
|    0   N/A  N/A      7324    C+G   C:\Program Files\PicGo\PicGo.exe            N/A      |
|    0   N/A  N/A      7680    C+G   ...siveControlPanel\SystemSettings.exe      N/A      |
|    0   N/A  N/A      9704    C+G   C:\Windows\explorer.exe                     N/A      |
|    0   N/A  N/A      9712    C+G   C:\Windows\System32\ShellHost.exe           N/A      |
|    0   N/A  N/A     10196    C+G   ...n\NVIDIA app\CEF\NVIDIA Overlay.exe      N/A      |
|    0   N/A  N/A     10628    C+G   ...n\NVIDIA app\CEF\NVIDIA Overlay.exe      N/A      |
|    0   N/A  N/A     12024    C+G   ...nt.CBS_cw5n1h2txyewy\SearchHost.exe      N/A      |
|    0   N/A  N/A     12116    C+G   ...2txyewy\StartMenuExperienceHost.exe      N/A      |
|    0   N/A  N/A     13324    C+G   ...on\129.0.2792.65\msedgewebview2.exe      N/A      |
|    0   N/A  N/A     14068    C+G   ...tionsPlus\logioptionsplus_agent.exe      N/A      |
|    0   N/A  N/A     14744    C+G   ...CBS_cw5n1h2txyewy\TextInputHost.exe      N/A      |
|    0   N/A  N/A     15356    C+G   ...m Files\TencentDocs\TencentDocs.exe      N/A      |
|    0   N/A  N/A     15636    C+G   ...voice\logioptionsplus_logivoice.exe      N/A      |
|    0   N/A  N/A     17316    C+G   C:\Program Files\Obsidian\Obsidian.exe      N/A      |
|    0   N/A  N/A     18100    C+G   ... 242.21870.138\bin\writerside64.exe      N/A      |
|    0   N/A  N/A     18768    C+G   ...nzyj5cx40ttqa\iCloud\iCloudHome.exe      N/A      |
|    0   N/A  N/A     19072    C+G   ...yj5cx40ttqa\iCloud\iCloudPhotos.exe      N/A      |
|    0   N/A  N/A     19804    C+G   ...on\129.0.2792.65\msedgewebview2.exe      N/A      |
|    0   N/A  N/A     20084    C+G   ...64__0srnedvzndzw6\TorrentClient.exe      N/A      |
|    0   N/A  N/A     20328    C+G   ...crosoft\Edge\Application\msedge.exe      N/A      |
+-----------------------------------------------------------------------------------------+
```