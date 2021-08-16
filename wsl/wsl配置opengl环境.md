## 配置OpenGL依赖
```
sudo apt-get install libgl1-mesa-dev freeglut3-dev libglu1-mesa-dev

sudo apt-get install libsoil-dev libglm-dev libassimp-dev libglew-dev libglfw3-dev libxinerama-dev libxcursor-dev libxi-dev
```

## 测试OpenGL连接
```
sudo ldconfig -p | grep GL
```

## 提示没有找到-libfreetype
```
sudo apt install libfreetype6-dev
```
## 提示没有-lXxf86vm
```
sudo apt install libxxf86vm-dev
```

## 安装图行界面
windowsx端下载安装VcXsrv`https://sourceforge.net/projects/vcxsrv/`

注：在wsl2中属于远程连接，在VcXsrv中的Extra settings中勾选 `Disable access control`

### 在wsl中在`~/.bashrc`文件末尾加入
```
#ip在windows的cmd中使用ipconfig查看，找到输入wsl的网卡的ip地址，port填0
#windows ip使用命令替代
export WINDOW_IP=$(awk '/nameserver / {print $2; exit}' /etc/resolv.conf 2>/dev/null)
export DISPLAY=ip:port.0
#wls中安装想x11-apps测试x11是否正常
sudo apt install x11-apps mesa-utils
glxgears
```
如果正常会出现此轮图像窗口
## 配置OpenGL版本
默认WSl使用OpenGL1.4版本，使用命令`glxinfo | grep "OpenGL version"`查看

修改使用高版本，在`~/.bashrc`文件末尾加入
```
export MESA_GL_VERSION_OVERRIDE=3.3
unset LIBGL_ALWAYS_INDIRECT #必须设置
```
同时在VcXsrv中Extra settings中去除 `Native opengl` 选项

## 设置VcXsrv默认启动配置文件
在配置配置完 Extra settings后，在下一步中可以保存配置文件，将配置文件保存至VcXsrv根目录，然后在桌面的启动图标右键选择属性，在`目标`一栏后面追加 `-run "配置文件路径"`
