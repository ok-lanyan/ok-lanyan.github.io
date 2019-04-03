---
layout: post
title:  VPS搭建Shadowsocks服务
date:   2019-03-20 22:57:00 +0800
categories: 教程
tags: VPS Shadowsocks
---

* content
{:toc}


我们使用Shadowsocks服务来科学上网，它搭建过程主要从以下方面来说明：
1. SS原理，Shadowsocks缩写
2. 购买VPS主机
3. 在VPS上搭建SS服务端
4. 在本地安装SS客户端
5. 开启BBR加速

__本文的环境搭建在CentOS上，已具体说明如何在CentOS6和CentOS7搭SS服务端，但开启BBR部分出现了我暂时解决不了的问题，所以只完成了在CentOS7上的加速工作。__


一、SS原理			{#SSPrinciple}
====================================

在以前，我们访问互联网的资源都是简单而直接的，用户的请求发送到资源服务方，比如Google、Facebook等，然后资源服务方直接将内容响应给用户，世界多么美好。

{% include image.html
    img="/styles/images/20190320-vps-build-ss/0101.png"
    caption="" %}

但是，在1998年时候，中国创建了互联网边界审查系统，称之为中国国家防火墙（GFW），这堵墙横在了用户和互联网资源服务方之间，用于监控和过滤互联网国际出口上的内容，监控国际网关的通讯，对认为不匹配国家官方要求的传输内容，进行干扰、阻断、屏蔽。

{% include image.html
    img="/styles/images/20190320-vps-build-ss/0102.png"
    caption="" %}

从此之后好多有价值的网站就被堵在了墙后。

人们想到了绕过GFW的办法，那就是在境外搭建一个国内用户的代理，国内用户与代理之间建立加密的通道，由境外代理请求被墙的网络资源，再通过加密通道返回给国内用户。代理的类型也有多种，像HTTP、Socks、VPN、SSH等。以SSH隧道为例：

{% include image.html
    img="/styles/images/20190320-vps-build-ss/0103.png"
    caption="" %}

因为SSH本身基于RSA加密技术，所以GFW就无法对数据传输过程加密的数据进行分析，从而避免被重置链接、阻断、屏蔽等问题。

但是GFW也不会懵B一世，人家也会学习，由于在创建SSH隧道的过程中有较为明显的特性，所以GFW还是可以通过分析连接的特性进行干扰。

{% include image.html
    img="/styles/images/20190320-vps-build-ss/0104.png"
    caption="" %}

于是SS横空出世，分为客户端和服务端，确保经过GFW时是普通的TCP协议数据包，没有明显的特征，而且GFW也无法解密分析，从而实现绕墙访问资源。从技术上保证不会被和谐掉，安全性较高。

资料参考：[使用ShadowSocks科学上网及突破公司内网](http://www.devtalking.com/articles/shadowsocks-guide/)

二、购买VPS主机				{#BuyVPS}
====================================

搭建上图的ss local client和ss server，需要购买VPS，并在VPS上搭建SS服务，最后在本地电脑上装SS客户端。

网上找了一些[VPS测评文章](http://www.vpsdaquan.cn/vpslinodedovultrhengxiangceping.html)之后，选择尝试提供商Vultr，并在[Vultr](https://www.vultr.com/?ref=7972636-4F)上完成注册和充值。

{% include image.html
    img="/styles/images/20190320-vps-build-ss/0201.png"
    caption="" %}

Vultr采用计时收费模式，按使用时长扣费（以每小时为单位），也就是说使用一个小时就会扣除一小时的费用。停止计费的办法只有一个，就是“__Server Destroy__”彻底删除VPS，而“Server Stop”依旧占用IP，无法停止计费。

三、搭建SS服务端  {#BuildSS}
============================

首先部署服务器（Deploy new servers），然后在该服务器上安装SS服务端并配置参数。要留意是在服务器上，而不是本地~  血的教训……
## 3.1 创建服务器（Deploy new servers） {#deploy}
1. 选择Server所在的物理位置，可以随意选择东京、芝加哥等。

2. 选择操作系统类型，__建议选择CentOS7，原因在文章一开始已说明__。\\
Tips：留意Snapshots快照备份功能，可以选择已有备份，免去重复安装配置的工作，在Destroy Server后尤为高效

3. 选择大小，根据不同需求，我选了25G $5/月。直接Deploy Now，服务器就创建好了。

{% include image.html
    img="/styles/images/20190320-vps-build-ss/0301.png"
    caption="" %}

## 3.2 测试IP是否被封

__这一步骤非常之关键！我在初期探索的时候，没有测试IP，导致搭完服务依旧不能成功上网，懵逼很久依旧找不到原因，只以为是搭的过程出错，不断删了重新来，删了重新来……经验教训，所以千万要先测试。__

1. 本地使用ping和ssh命令检测：只有当两个命令均通过时，才能进行下一步操作。如果有一个不通过，重复[3.1 创建服务器](#deploy)。
Tips：不要边Deploy边Destroy服务器，Vultr有保留IP功能，使得用户在Destroy后继续使用，无法改变IP。

2. 前往[国内端口扫描站](https://www.vultrcn.com/goto/?url=aHR0cDovL2Nvb2xhZi5jb20vdG9vbC9wb3J0)检测端口是否被封：SSH连接默认端口是22，只有当端口状态为开放时，该IP没有被封，可用。如果状态为关闭，重复[3.1 创建服务器](#deploy)。\\
详细说明参考：[#教程# Vultr 能 Ping 但是 SSH 无法连接的解决办法](https://www.vultrcn.com/11.html)

{% include image.html
    img="/styles/images/20190320-vps-build-ss/0302.png"
    caption="- ping通的页面 -" %}

{% include image.html
            img="/styles/images/20190320-vps-build-ss/0303.png"
            caption="- ssh 连接成功的页面 -" %}

{% include image.html
            img="/styles/images/20190320-vps-build-ss/0304.png"
            caption="- 端口正常的页面 -" %}

## 3.3 SS服务端

在ssh连接成功的终端上输入以下命令

### 1. 安装SS
~~~ ruby
sudo yum -y install epel-release  # 首先安装epel扩展源
sudo yum -y install python-pip # 再安装pip
pip install shadowsocks
~~~

### 2. 配置参数
~~~ ruby
vi /etc/shadowsocks.json # 添加服务端信息

{
    "server":"0.0.0.0",
    "server_port":8388,
    "local_port":1080,
    "timeout":600,
    "method":"aes-256-cfb",
    "password”:"ABC123",
} 
# Esc回到命令模式，输入”:wq”保存并退出vi
~~~

### 3.4 系统设置（开机启动+防火墙）

在开机启动和防火墙的设置上，CentOS6和7略微有些差别，可以根据你实际的系统版本来选择。\\
开机启动：在重启服务端后，不需要再远程，执行打开服务的命令。\\
防火墙：防火墙会默认关闭端口，那么将无法使用SS服务，可以选择关闭防火墙，或者配置防火墙规则开放配置端口。

#### 1）CentOS 6
~~~ ruby
echo "ssserver -c /etc/shadowsocks.json -d start" >> /etc/rc.d/rc.local # 开机启动
chkconfig iptables off # 永久关闭防火墙，因为重启系统后会默认开启

# 不用输入，仅作防火墙相关命令的提示
service iptables start # 打开防火墙
service iptables stop # 临时关闭防火墙
service iptables status # 查看防火墙状态
~~~

#### 2）CentOS 7

此处/etc/shadowsocks.json中的server务必改为0.0.0.0，否则将不能实现开机启动，同时使用SnapShot后，不用再修改IP。

~~~ ruby
vi /etc/systemd/system/shadowsocks.service # 新建ss服务的systemd配置文件，并复制以下内容

[Unit]
Description=Shadowsocks

[Service]
TimeoutStartSec=0
ExecStart=/usr/bin/ssserver -c /etc/shadowsocks.json

[Install]
WantedBy=multi-user.target
# Esc回到命令模式，输入”:wq”保存并退出vi

systemctl enable shadowsocks # 设置ss为开启启动项
systemctl start shadowsocks # 启动ss
systemctl status shadowsocks -l # 查看ss服务的状态

# 配置防火墙规则，开放配置端口，即shadowsocks.json中的server_port
firewall-cmd --zone=public --add-port=8388/tcp --permanent
firewall-cmd --reload
~~~

#### 验证是否开机启动
服务器重启，使用“systemctl status shadowsocks -l”查看服务状态，如果已经启动，Active为active，如下图。

{% include image.html
    img="/styles/images/20190320-vps-build-ss/0305.png"
    caption="- 查看服务状态，服务已启动的页面 -" %}

如果Active为dead或者failed，则设置失败。

{% include image.html
    img="/styles/images/20190320-vps-build-ss/0306.png"
    caption="- 查看服务状态，服务开机启动失败的页面 -" %}

上图失败原因是socket绑定的地址正在使用，显示“socket.error: [Errno 98] Address already in use”。\\
解决方案是在sysctl.conf文件中，加入4行TCP连接参数配置，具体命令如下：
~~~ ruby
vi  /etc/sysctl.conf 
net.ipv4.tcp_syncookies = 1 # 当出现SYN等待队列溢出时，启用cookies来处理，可防范少量SYN攻击，默认为0，表示关闭
net.ipv4.tcp_tw_reuse = 1 # 开启重用，允许将TIME-WAIT sockets重新用于新的TCP连接，默认为0，表示关闭
net.ipv4.tcp_tw_recycle = 1 # 表示开启TCP连接中TIME-WAITsockets的快速回收，默认为0，表示关闭
net.ipv4.tcp_fin_timeout = 5 # 修改系统默认的超时时间
~~~

详细解释参见：[修改Linux内核参数，减少TCP连接中的TIME-WAIT](http://blog.csdn.net/chenyulancn/article/details/16338185)、[linux TCP连接配置](http://blog.csdn.net/chenyulancn/article/details/16339427)



四、本地安装SS客户端   {#LocalClient}
============================

1. 下载并安装ShadowsocksX-NG：[Mac下载地址](https://github.com/shadowsocks/ShadowsocksX-NG/releases)

2. 将3.3中的配置参数输入对应框中，并将选择当前新建的服务器进行连接。
{% include image.html
    img="/styles/images/20190320-vps-build-ss/0401.png"
    caption="" %}

3. 用浏览器连谷歌，能正常连接的，就大功告成啦！

如果还是不能上网，这篇[Mac操作系统上的ss客户端：ShadowsocksX-NG](https://www.twisted-meadows.com/shadowsocksx-ng/)这可以参考看看。




五、BBR加速  {#BBRSpeed}
============================

TCP BBR拥塞控制算法仅支持Linux Kernel 4.9以上，所以我们需要先升级内核，再更改设置开启BBR。\\
BBR的原理可以参考：[BBR与之前TCP拥塞控制相比有什么优势](https://www.zhihu.com/question/53559433)
## 5.1 升级Linux内核

CentOS6在升级过程中出现错误，一直找不到解决方法，如果是CentOS6，可以参考[CentOS6开启BBR加速](http://www.weninux.com/centos6%E5%BC%80%E5%90%AFbbr%E5%8A%A0%E9%80%9F)。

### 1）CentOS 6

~~~ ruby
yum update # 更新yum
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org # 安装ELRepo公钥
yum install https://www.elrepo.org/elrepo-release-6-8.el6.elrepo.noarch.rpm # CentOS6 安装ElRepo库

yum --disablerepo=\* --enablerepo=elrepo-kernel list available # 查看可安装的内核，没有kernel-ml
# 手动下载并安装
wget https://elrepo.org/linux/kernel/el7/x86_64/RPMS/kernel-ml-5.0.5-1.el7.elrepo.x86_64.rpm
wget https://elrepo.org/linux/kernel/el7/x86_64/RPMS/kernel-ml-devel-5.0.5-1.el7.elrepo.x86_64.rpm
rpm -ivh kernel-ml-5.0.5-1.el7.elrepo.x86_64.rpm # 出现依赖错误，一直没找到解决办法，就转CentOS7了
rpm -ivh kernel-ml-devel-5.0.5-1.el7.elrepo.x86_64.rpm
vim /boot/grub/grub.conf #修改为default=0，将新内核设置为默认选项
~~~

### 2）CentOS 7
~~~ ruby
yum update # 更新yum
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org # 安装ELRepo公钥
rpm -Uvh https://www.elrepo.org/elrepo-release-7.0-3.el7.elrepo.noarch.rpm # CentOS7 安装ElRepo库

yum --disablerepo=\* --enablerepo=elrepo-kernel list available # 查看可安装的内核，选择kernel-ml
yum --disablerepo=\* --enablerepo=elrepo-kernel install kernel-ml -y # 安装内核
grub2-set-default 0 # 将新内核设置为默认选项
~~~

下图是CentOS6一直未解决的问题，知道怎么解的兄嘚指导指导哈~\\
{% include image.html
    img="/styles/images/20190320-vps-build-ss/0501.png"
    caption="- CentOS 6 内核升级失败，未找到解决办法 -" %}


## 5.2 开启BBR，CentOS6和7都适用

~~~ ruby
# 在/etc/sysctl.conf后添加如下两行：
echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf
sysctl -p  #使 配置生效
reboot # 重启服务器

uname -r # 确认新内核是否生效，返回“5.0.4-1.el7.elrepo.x86_64”
lsmod | grep bbr # 查看BBR是否开启，返回“tcp_bbr                20480  6”
~~~

详细说明参考：[CentOS7开启BBR加速]([http://www.weninux.com/centos7%E5%BC%80%E5%90%AFbbr%E5%8A%A0%E9%80%9F])