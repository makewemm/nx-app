# nx-app

支持vl.ss,vm.ss,哪吒，固定和临时隧道，支持订阅，支持ws直连

/start  进程检测

/info  系统信息

/哪吒key 订阅地址，仅vl-ss,需要vm-ss可手搓

需要root权限，不适合hugface这样的容器

# 环境变量


| 变量名称 | 说明 |
|---------------|-------------|
| PORT | web与直连端口，隧道端口均可（默认值：8080） |
| VPATH | vl-ss的路径（默认值：'vls'） |
| VL_PORT | vl-ss端口，隧道端口（默认值：8002） |
| MPATH | vm-ss的路径（默认值：'vms'） |
| VM_PORT | vm-ss端口，隧道端口（默认值：8001） |
| UUID | UUID（默认值：'3a8a1de5-7d41-45e2-88fe-0f538b822169'） |
| CF_IP | 优选（默认值：'ip.sb'） |
| SUB_NAME | 订阅名称（默认值：'NX-Argo'） |
| SUB_URL | 订阅URL（默认值：'无'） |
| NEZ_SERVER | Nezha监控服务器地址（默认值：'无'） |
| NEZ_KEY | Nezha监控服务器密钥（默认值：'无'） |
| NEZ_PORT | Nezha监控服务器端口（默认值：443） |
| NEZ_TLS | Nezha TLS选项（默认值：'--tls'） |
| FILE_PATH | 文件存储路径（默认值：'/tmp/'） |
| TOK | 固定隧道Token（默认值：空） |
| ARG_DOMAIN | 固定隧道域名，临时隧道不要设置（默认值：空） |
| WEB_FILENAME | xr.ay文件名（默认值：'webkgk122dm.sh'） |
| NEZHA_FILENAME | Nezha文件名（默认值：'nezdkd122ma.sh'） |
| CFF_FILENAME | 隧道文件名（默认值：'cffmghk102f.sh'） |
| NEZHA_URL_X64 | 哪吒客户端链接，默认即可 |
| NEZHA_URL_ARM64 | 哪吒客户端链接，默认即可 |
