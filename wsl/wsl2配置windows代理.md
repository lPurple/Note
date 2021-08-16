windows代理软件打开`允许来自局域网请求`,windows防火墙对代理软件放行
## wsl建立脚本
``` bash
#!/bin/bash
PROXY_PORT=1080
WINDOWS_IP=`cat /etc/resolv.conf | grep nameserver | awk '{print $2}'`
ALL_PROXY=$WINDOWS_IP:$PROXY_PORT

case $1 in
        start)
            export http_proxy=$ALL_PROXY
            export https_proxy=$ALL_PROXY
        ;;
        stop)
            unset http_proxy
            unset https_proxy
        ;;
        status)
            echo "http_proxy:" $http_proxy
            echo "https_proxy:" $https_proxy
        ;;
esac
```
在`~/.bashrc`文件中加入`alias proxy="source ~/.bin/set-wsl2-proxy.sh"`

注：请填入具体脚本的路径，使用`chmod +x`给建立的脚本添加可执行权限






