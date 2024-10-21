# PyQt5-msm8953-Phones-Linux
为msm8953（主要是小米和红米手机的高通625机型）移植的PyQt5开发环境。触屏工作正常，显示分辨率一般为`1920*1080`
刷机包在[发行版](https://github.com/umeiko/PyQt5-msm8953-Phones-Linux/releases/tag/v24.04)里
![微信图片_20241021161124](https://github.com/user-attachments/assets/551ac425-92d7-41a5-be9d-e7360f345eba)

刷机完毕后，可以通过尾插usb连接电脑后，通过Putty连接到手机，然后运行以下命令通过WIFI联网：

```bash
sudu nmtui
```

成功联网后获取Ip地址

```bash
ip addr
```

然后通过SSH进行开发即可,推荐使用`VSCODE`的`Remote-SSH`插件。登录用户名`umeko`密码`1234`。

进入系统后，在`~/`目录下安放你的`PyQt5`项目文件夹，编写启动脚本，如`run.sh`，这里以我提供的一个示例项目为例:

```bash
git clone https://gitee.com/meiziyang2023/pyqt5_hk4117_gui.git
cd pyqt5_hk4117_gui
sudo startx ./run.sh
```

如果需要旋转屏幕方向，则运行`sudo nano /etc/X11/xorg.conf.d/00-rotate.conf`添加屏幕旋转的规则：

```
Section "InputClass"
	Identifier "libinput touchscreen catchall"
	Option "CalibrationMatrix" "0 1 0 -1 0 1 0 0 1"
	MatchIsTouchscreen "on"
	MatchDevicePath "/dev/input/event*"
	Driver "libinput"
EndSection
Section "Monitor"
	Identifier "DSI-1"
	Option "Rotate" "Right"
EndSection
```

保存后重启代码即可。
如果需要开机自动运行你的PyQt5代码，则编写`systemd`服务即可。
