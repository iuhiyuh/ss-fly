# ss-fly

> 备份下来防丢

## 一键搭建SS/搭建SSR服务

**1. 运行搭建ss脚本代码**

```bash
git clone https://github.com/suniceman/ss-fly
```

如果提示 `bash: git: command not found`，则先安装git：
Centos执行这个：

```bash
yum -y install git
```

Ubuntu/Debian执行这个：

```bash
apt-get update && apt-get -y install git
```

**2. 运行搭建ss脚本代码**

```bash
ss-fly/ss-fly.sh -i password port
```

注：如果需要改密码或者改端口，只需要重新再执行一次搭建ss脚本代码就可以了，或者修改/etc/shadowsocks.json这个配置文件。  

**3. 相关ss操作**

```bash
启动：/etc/init.d/ss-fly start
停止：/etc/init.d/ss-fly stop
重启：/etc/init.d/ss-fly restart
状态：/etc/init.d/ss-fly status
查看ss链接：ss-fly/ss-fly.sh -sslink
修改配置文件：vim /etc/shadowsocks.json
```

**4. 卸载ss服务**

```bash
ss-fly/ss-fly.sh -uninstall
```

## 一键搭建shadowsocksR

再次提醒，如果安装了SS，就不需要再安装SSR了，如果要改装SSR，请按照上一部分内容的教程先卸载SS！！！

**1. 下载一键搭建ssr脚本**

```bash
git clone https://github.com/suniceman/ss-fly
```

**2. 运行搭建ssr脚本代码**

```bash
ss-fly/ss-fly.sh -ssr
```

输入对应的参数执行完上述的脚本代码后，会进入到输入参数的界面，包括服务器端口，密码，加密方式，协议，混淆。可以直接输入回车选择默认值，也可以输入相应的值选择对应的选项.

全部选择结束后，会看到如下界面，就说明搭建ssr成功了：
```
Congratulations, ShadowsocksR server install completed!
Your Server IP        :你的服务器ip
Your Server Port      :你的端口
Your Password         :你的密码
Your Protocol         :你的协议
Your obfs             :你的混淆
Your Encryption Method:your_encryption_method
 
Welcome to visit:https://shadowsocks.be/9.html
Enjoy it!
```

1. 相关操作ssr命令
    ```
    启动：/etc/init.d/shadowsocks start
    停止：/etc/init.d/shadowsocks stop
    重启：/etc/init.d/shadowsocks restart
    状态：/etc/init.d/shadowsocks status
    配置文件路径：/etc/shadowsocks.json
    日志文件路径：/var/log/shadowsocks.log
    代码安装目录：/usr/local/shadowsocks
    ```

1. 卸载ssr服务
    ```
    ./shadowsocksR.sh uninstall
    ```

## 一键开启BBR加速

> BBR是Google开源的一套内核加速算法，可以让你搭建的shadowsocks/shadowsocksR速度上一个台阶，本一键搭建ss/ssr脚本支持一键升级最新版本的内核并开启BBR加速。<br/>
BBR支持4.9以上的，如果低于这个版本则会自动下载最新内容版本的内核后开启BBR加速并重启，如果高于4.9以上则自动开启BBR加速，执行如下脚本命令即可自动开启BBR加速：

```bash
ss-fly/ss-fly.sh -bbr
```

装完后需要重启系统，输入y即可立即重启，或者之后输入`reboot`命令重启。

判断BBR加速有没有开启成功。输入以下命令：
```
sysctl net.ipv4.tcp_available_congestion_control
```
如果返回值为：
```
net.ipv4.tcp_available_congestion_control = bbr cubic reno
```
后面有bbr，则说明已经开启成功了。
