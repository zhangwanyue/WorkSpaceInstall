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

# 链接第二块屏幕，第一快屏幕闪烁
重新调节连接第二块屏幕时第一块屏幕的缩放比

# 屏幕亮度闪烁
power->关闭 automatic brightness

# tweak
sudo apt-get install gnome-tweak-tool

# 担心自动snap更新导致的问题
因为本机和一些高版本的gnome有一些不兼容，会导致黑屏，所以停止更新snap包
`snap refresh --hold`

参考: https://ubuntuhandbook.org/index.php/2022/11/turn-off-automatic-updates-snap-apps/
https://snapcraft.io/docs/keeping-snaps-up-to-date

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

# 隐藏桌面的Home和Trash图标
在Activities中找到Extension，点击Desktop Icons前面的齿轮图标，在新打开的窗口中，关闭'Show the personal folder in the desktop'和'Show the trash icon in the desktop'

# 视频播放器
推荐使用 SMPlayer，可以加速播放，并且内置了各种解码器，不需要再额外安装解码器
`sudo apt-get install smplayer`
使用的时候，在`Options->Preference`中可以看到加速减速的快捷键是'['和']'，可以自行修改

# docker
参考链接：https://yeasy.gitbook.io/docker_practice/install/ubuntu#shi-yong-apt-an-zhuang
## 使用APT安装
* 由于 apt 源使用 HTTPS 以确保软件下载过程中不被篡改。因此，我们首先需要添加使用 HTTPS 传输的软件包以及 CA 证书
```
$ sudo apt-get update

$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```
* 为了确认所下载软件包的合法性，需要添加软件源的 GPG 密钥
鉴于国内网络问题，强烈建议使用国内源，官方源请在注释中查看
```
$ curl -fsSL https://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# 官方源
# $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```
* 向 sources.list 中添加 Docker 软件源
```
$ echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://mirrors.aliyun.com/docker-ce/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null


# 官方源
# $ echo \
#   "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
#   $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
* 安装 Docker
```
$ sudo apt-get update

$ sudo apt-get install docker-ce docker-ce-cli containerd.io
```
## 使用脚本自动安装
在测试或开发环境中 Docker 官方为了简化安装流程，提供了一套便捷的安装脚本，Ubuntu 系统上可以使用这套脚本安装，另外可以通过 --mirror 选项使用国内源进行安装：
```
# $ curl -fsSL test.docker.com -o get-docker.sh
$ curl -fsSL get.docker.com -o get-docker.sh
$ sudo sh get-docker.sh --mirror Aliyun
# $ sudo sh get-docker.sh --mirror AzureChinaCloud
```
执行这个命令后，脚本就会自动的将一切准备工作做好，并且把 Docker 的稳定(stable)版本安装在系统中。
## 启动 Docker
```
$ sudo systemctl enable docker
$ sudo systemctl start docker
```
## 建立 docker 用户组
默认情况下，docker 命令会使用 Unix socket 与 Docker 引擎通讯。而只有 root 用户和 docker 组的用户才可以访问 Docker 引擎的 Unix socket。出于安全考虑，一般 Linux 系统上不会直接使用 root 用户。因此，更好地做法是将需要使用 docker 的用户加入 docker 用户组。
* 建立 docker 组：
`$ sudo groupadd docker`
* 将当前用户加入 docker 组：
`$ sudo usermod -aG docker $USER`
* 查看 docker 组的用户:
`$ getent group docker`
退出当前终端并重新登录，进行如下测试。
## 测试 Docker 是否安装正确
```
$ docker run --rm hello-world

Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
b8dfde127a29: Pull complete
Digest: sha256:308866a43596e83578c7dfa15e27a73011bdd402185a84c5cd7f32a88b501a24
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```
若能正常输出以上信息，则说明安装成功。

## docker 镜像加速
* 国内镜像加速器
阿里云(需要登录个人帐号获取)：
https://cr.console.aliyun.com/cn-hangzhou/instances
点击管理控制台->登录帐号(淘宝帐号)->左侧镜像工具->镜像加速器->复制加速器地址
网易云：
https://hub-mirror.c.163.com
百度云：
https://mirror.baidubce.com

* 首先执行以下命令，查看是否在 docker.service 文件中配置过镜像地址。
`$ systemctl cat docker | grep '\-\-registry\-mirror'`
如果该命令有输出，那么请执行 `$ systemctl cat docker` 查看 `ExecStart=` 出现的位置，修改对应的文件内容去掉 `--registry-mirror` 参数及其值，并按接下来的步骤进行配置。
如果以上命令没有任何输出，那么就可以在 `/etc/docker/daemon.json` 中写入如下内容（如果文件不存在请新建该文件）：
```
{
  "registry-mirrors": [
    "https://hub-mirror.c.163.com",
    "https://mirror.baidubce.com"
  ]
}
```

* 重启服务
```
$ sudo systemctl daemon-reload
$ sudo systemctl restart docker
```


