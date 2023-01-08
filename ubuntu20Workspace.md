# keyboard
/etc/default/grub
i8042.dumbkbd
`GRUB_CMDLINE_LINUX_DEFAULT="quiet splash i8042.dumbkbd"`
sudo update-grub

# 开机黑屏
按 Fn+F2 进入grub中，输入用户名密码进入账户
然后: sudo service gdm3 restart 重启gdm3

# 连接第二块屏幕黑屏
Display里，修改第二块屏幕的refresh rate

# 屏幕亮度闪烁
power->关闭 automatic brightness

# tweak
sudo apt-get install gnome-tweak-tool

# apt-get add aliyun & tsinghua source
aliyun: https://developer.aliyun.com/mirror/ubuntu/
tsinghua: https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/

/etc/apt/sources.list

一定要记得 sudo apt-get update，不然装软件都会出问题（版本不对）

# vim 
sudo apt-get install vim

# git
sudo apt-get install git
初始化配置: https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%88%9D%E6%AC%A1%E8%BF%90%E8%A1%8C-Git-%E5%89%8D%E7%9A%84%E9%85%8D%E7%BD%AE

# ssh
参考: https://zhuanlan.zhihu.com/p/146976128
sudo apt-get install openssh-server
装好后默认自动启动ssh服务
查看ssh状态: sudo service ssh status
连接ssh: `ssh username@ip_address`
查看ip: ip -4 address
启用ssh: sudo systemctl disable --now ssh
或者: sudo service ssh start
禁用ssh: sudo systemctl enable --now ssh
或者: sudo service ssh stop

# chrome
```
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i xxx.deb
```
# Microsoft edge
官网下载deb安装包: https://www.microsoftedgeinsider.com/en-us/
sudo dpkg -i xxx.deb

将edge添加到桌面Favorite后发现，这个应用没有图标，使用的默认的小工具图标，手动来修改下:
sudo vim /usr/share/applications/microsoft-edge-beta.desktop
修改Icon一行指向你下载的edge的图标，比如我的是:
```
Icon=/usr/local/installedApp/edge-logo.jpeg
```
然后将该应用Remove From Favourite并重新添加到Favourite就好了

# java 

download jdk:
https://www.oracle.com/java/technologies/downloads/#java8
参考:
https://zhuanlan.zhihu.com/p/492149414


```
sudo mkdir /usr/lib/jdk
sudo tar -zxvf jdk-8u131-linux-x64.tar.gz -C /usr/lib/jdk
```
add the following to ~/.bashrc:
```
#set oracle jdk environment
export JAVA_HOME=/usr/lib/jdk/jdk1.8.0_131
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH
```

source ~/.bashrc



# idea
```
sudo tar xvzf ideaIU-*.tar.gz -C /usr/local/installedApp
```
首次启动
进入/usr/local/installedApp/ideaxxx/bin，执行./idea.sh

建立桌面快捷方式：
idea菜单栏->Tools->Create Desktop Entry


# maven

# golang

# vscode

# 输入法
听说20.04的版本安装搜狗输入法会遇到许多不兼容的问题（比如和idea打架:https://zhuanlan.zhihu.com/p/262125769），所以这次装了google pinyin输入法，也很好用
https://blog.csdn.net/a805607966/article/details/105874756

# surfshark
因为封锁原因，建议使用openvpn手动配置


* 修改dns
1. Update /etc/systemd/resolved.conf
[Resolve]
DNS=208.67.222.222 208.67.220.220

2. Restart system resolved: service systemd-resolved restart
3. Run systemd-resolve --status
4. change the link
https://bugs.launchpad.net/ubuntu/+source/systemd/+bug/1774632
$ sudo rm -f /etc/resolv.conf
$ sudo ln -s /run/systemd/resolve/resolv.conf /etc/resolv.conf

有时候dns还是有问题，网页打不开，打开/etc/resolv.conf，把`nameserver 192.168.xxx.xxx`前面加`#`屏蔽掉。

# clash
github上下载最新的安装包:
`https://github.com/Fndroid/clash_for_windows_pkg/releases`
下载要注意下载x64-linux.tar.gz的版本，amd64和x64都是给x86-64的，但是arm64是另一个架构，不要搞混
直接解压
`sudo tar xvzf xxx.tar.gz -C /usr/local/installedApp`
执行解压后包中的./cfw运行

* 给clash建立桌面快捷方式
sudo vim /usr/share/applications/Clash.desktop

因为clash包里没找到icon，所以自己网上找了个图标放进去

```
[Desktop Entry]
Name=Clash
Comment=Clash for Windows x64 Linux
Exec=/usr/local/installedApp/Clash-for-Windows-0.20.12-x64-linux/cfw
Icon=/usr/local/installedApp/Clash-for-Windows-0.20.12-x64-linux/clash-icon.jpeg
Type=Application
StartupNotify=true
``` 

# github
github升级后，https方式接入的不能使用用户名密码提交git了，要使用token的方式：
https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token
每次提交代码都得加上token，太麻烦了，以后还是用ssh吧

* ssh

先生成ssh密钥:
`ssh-keygen -t rsa -C "xxx@xx.com"`
默认生成到`~/.ssh`中，找到`id_rsa.pub`放到Github的`SSH and GPG keys`中


