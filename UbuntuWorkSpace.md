# ubuntu 16.04/18.04 install

### vim

```
sudo apt-get install vim
```

### git

```
sudo apt-get install git
```

### ssh

```
sudo apt-get install openssh-server
ssh-keygen -t rsa -C "xxx@qq.com"
```

### chrome

```
sudo wget http://www.linuxidc.com/files/repo/google-chrome.list -P /etc/apt/sources.list.d/
wget -q -O - https://dl.google.com/linux/linux_signing_key.pub  | sudo apt-key add -
sudo apt-get update
sudo apt-get install google-chrome-stable
```

* run

```
/usr/bin/google-chrome-stable 
```

### `SwitchyOmega_Chromium`

* 打开`Extensions->Developer mode`

* 直接把`SwitchyOmega_Chromium.zip`拖拽到Extensions中 

* 如果直接拖拽不成功，则选择load unpacked

```
unzip SwitchyOmega_Chromium.zip -d SwitchyOmega_Chromium
```

选择解压的`SwitchyOmega_Chromium`文件

### shadowsocks-qt5

```
sudo apt-add-repository ppa:hzwhuang/ss-qt5
```

对于18.04的系统，需要修改/etc/apt/sources.list.d/hzwhuang-ubuntu-ss-qt5-bionic.list:
将bionic改为xenial:
```
deb http://ppa.launchpad.net/hzwhuang/ss-qt5/ubuntu xenial main
# deb-src http://ppa.launchpad.net/hzwhuang/ss-qt5/ubuntu xenial main
```

然后:
```
sudo apt-get update
sudo apt-get install shadowsocks-qt5
```

### sougou

download link:
https://pinyin.sogou.com/linux/?r=pinyin
```
sudo dpkg -i xxx.deb
sudo apt-get install -f
sudo dpkg -i xxx.deb
```
系统设置->语言支持（`System->Language Support`），将键盘输入法系统由默认的iBus设置为fcitx。
注销，重新登录。（有时可能需要重启电脑）
点击右上角的输入法图标，点击设置，进入设置界面，这个时候没有看到搜狗输入法，点击左下角的加号，然后注意先要去掉”只显示当前语言的输入法”前面那个勾，然后再搜索”sogo”，这个时候就看到sogo pinyin了，接着添加就可以了，然后就可以切换输入法了。

### java

```
sudo mkdir /usr/lib/jvm
sudo tar -zxvf jdk-8u131-linux-x64.tar.gz -C /usr/lib/jvm
```
add the following to ~/.bashrc:
```
#set oracle jdk environment
export JAVA_HOME=/usr/lib/jvm/jdk1.8.0_131
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH
```

### android studio

```
sudo apt-get install libz1 libncurses5 libbz2-1.0:i386 libstdc++6 libbz2-1.0
```

向`~/.bashrc`中添加：
```
export ANDROID_HOME=~/Android/Sdk/
export PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools
sudo unzip android-studio-ide-xxx-linux.zip -d /usr/local/installedApp
```

* gradle下载不了东西：

修改`~/.gradle/gradle.properties`中的代理配置

### gitbook-editor

```
sudo dpkg -i xxx.deb
```
安装完之后发现不能正常点击应用图标启动，就是点击一下没反应。
于是查看了一下`/usr/share/applications/gitbook-editor.desktop`启动图标时启动的是哪个可执行文件，然后发现是`/opt/gitbook-editor/editor`，手动执行该可执行文件，发现报出`error while loading shared libraries: libgconf-2.so.4: cannot open shared object file: No such file or directory`的错误，搜索该错误之后找到解决方法：
`sudo apt-get install libgconf-2-4`
参考链接: https://github.com/postmanlabs/postman-app-support/issues/4514

但是gitbook-editor打开的时候，加载账户和书籍内容可能需要翻墙，尝试成功的解决办法时使用privoxy将socks代理转为http代理，然后修改.bashrc，使用http代理：

```
export http_proxy=127.0.0.1:8118
export https_proxy=127.0.0.1:8118
```

可是发现有时候用privoxy+http代理反倒打不开，再换成单纯的socks代理试试可能（有一定的概率……）会好：
```
## shadowsocks
export socks_proxy=socks5://127.0.0.1:1080
```

### privoxy

```
sudo apt-get install privoxy
```

配置Privoxy, `vim /etc/privoxy/config`:
```
forward-socks5 / 127.0.0.1:1080 .
listen-address 127.0.0.1:8118
```

重启privoxy服务：
`sudo systemctl restart privoxy`

### clion

```
sudo apt-get install gcc
sudo apt-get install build-essential
sudo tar xvzf CLion-*.tar.gz -C /usr/local/installedApp
```

### idea

```
sudo tar xvzf ideaIU-*.gz -C /usr/local/installedApp
```

### pycharm

```
sudo tar -zxvf pycharm-professional-*.tar.gz -C /usr/local/installedApp/
```

### 创建桌面图标

Android Studio/idea/clion > Tools > Create Desktop Entry
创建到了/home/vera/.local/share/applications

### maven

官网下载Binary tar.gz archive

```
tar -zxvf apache-maven-*-bin.tar.gz 
sudo mv apache-maven-*/ /usr/local/bin/
```

如果直接`sudo tar xvzf apache-maven-*/ -C /usr/local/bin/`会导致文件所有者和所在组都是root，不方便使用，当然也可以后期再该组权限:`sudo chown vera:vera -R apache-maven-*/`
修改`~/.bashrc`
```
# maven
export MAVEN_HOME=/usr/local/bin/apache-maven-*
export PATH=$MAVEN_HOME/bin:$PATH
```

如果使用的是`sudo apt-get install maven`安装的maven，那配置文件(比如`settings.xml`)在`/etc/maven`下。

### nodejs & npm

* nodejs官网下载

```
tar -xvf node-*-linux-x64.tar.gz
sudo mv node-*-linux-x64 /usr/local/bin/
```

* 修改`~/.bashrc`

```
export NODEJS_HOME=/usr/local/bin/node-*-linux-x64
export PATH=$NODEJS_HOME/bin:$PATH
```

### tmux

```
sudo apt-get install tmux
```

### mysql

```
sudo apt-get install mysql-server
sudo apt-get install mysql-client
sudo apt-get install mysql-workbench
```

* 设置权限: `sudo mysql_secure_installation`

* 登录: `sudo mysql -u root -p`

* 解决`Access denied for user 'root'@'localhost'`问题:

参考链接:https://stackoverflow.com/a/53487418

```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'xxx';
FLUSH PRIVILEGES;（该条命令的作用是：将grant tables的信息提取到内存里）
```

* 修改mysql root密码:

```
UPDATE mysql.user SET authentication_string=PASSWORD('xxx') WHERE user='root';
FLUSH PRIVILEGES;
```

* 查看用户表中的信息（用户，被验证插件处理后的验证密码串，验证插件，host）:

```
SELECT user,authentication_string,plugin,host FROM mysql.user;
```

* 查看`validate_password`相关信息:

```
SHOW VARIABLES LIKE 'validate_password%';
set global validate_password_policy=0;
```

* 新建用户

```
CREATE USER 'vera'@'localhost' IDENTIFIED BY 'xxx';
```

将xxx数据库的各种权利赋予vera用户:
```
GRANT ALL ON xxx.* TO 'vera'@'localhost';
```
