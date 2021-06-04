1.注册域名和购买非中国大陆地区的VPS

(1)注册域名

注册免费域名:freenom

解析免费域名:注册好域名之后，把域名解析到你要搭服务器所用VPS对应的IP地址，一般5分钟之内就可以生效，最迟72小时生效。使用 Cloudflare 管理域名.

(2)购买非中国大陆地区的VPS

非中国大陆vps:Vultr(支持免费更换ip)

2.远程连接并管理 Vultr VPS 服务器

个人推荐SSH客户端:Putty、FinalShell、Xshell.

手机端SSH客户端:JuiceSSH、ServerCat.


3一键搭建ShadowsocksR/SSR服务器教程

(1)安装 wget 命令

yum -y install wget #CentOS

sudo apt-get install wget #Debian/Ubuntu

逗比大神(ToyoDAdoubi)的ShadowsocksR/SSR一键搭建脚本（推荐-因为全中文界面，操作更加简单方便）

此一键安装脚本支持 CentOS 6+、Debian 7+、Ubuntu 12+ 及以上系统版本(推荐使用系统:Debian9).内存要求：≥128M，不支持“WS+TLS+CDN”，也不需要绑定域名.

wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubi/doubi/master/ssr.sh && chmod +x ssr.sh && bash ssr.sh

(2)安装 curl 命令

yum -y install curl #CentOS

apt -y install curl #Debian/Ubuntu

“ShadowsocksR+TLS+Web+CDN”模式SSR一键搭建脚本（推荐-需绑定域名）

此一键安装脚本支持的服务器操作系统：Debian 9、10，Ubuntu 16.04 、18.04、19.10，Centos 7、8.（推荐使用系统:Debian9-Centos可能会导致八合一脚本TLS证书失败)

bash -c "$(curl -fsSL https://raw.githubusercontent.com/JeannieStudio/all_install/master/SixForOne_install.sh)"

4.一键安装并开启BBR加速(Vultr自带锐速)

一键安装BBR加速脚本，执行如下命令：

wget --no-check-certificate -O tcp.sh https://github.com/cx9208/Linux-NetSpeed/raw/master/tcp.sh && chmod +x tcp.sh && ./tcp.sh

选择你想要的BBR加速-安装内核(重启)

wget --no-check-certificate -O tcp.sh https://github.com/cx9208/Linux-NetSpeed/raw/master/tcp.sh && chmod +x tcp.sh && ./tcp.sh

选择你想要的加速模块(无需重启)







