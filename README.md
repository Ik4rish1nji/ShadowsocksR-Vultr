# [ShadowsocksR/SSR搭建教程2021]使用 Vultr VPS 自建SSR服务器及ShadowsocksR节点配置客户端实现科学上网

本系列教程适合新手小白，当然老鸟也可以看看，也许会有你还不知道的黑科技。一灯不是和尚手把手教你搭建SS/SSR/V2Ray/Trojan节点服务器并实现科学上网，这可能是史上最全、最简单、最适合小白萌新的ShadowsocksR/SSR搭建教程。本教程内容包括购买域名和VPS，远程连接并管理VPS和一键搭建ShadowsocksR/SSR服务器，并开启BBR加速以及ShaodowsocksR/SSR客户端配置方法。

## 1、注册域名和购买非中国大陆地区的VPS
### （1）注册域名:如果你使用“SSR+TLS+Web+CDN”模式的话，就需要用域名伪装成网站，否则不需要域名。注册域名有两种途径：注册国外免费域名和付费购买域名。

1）注册免费域名

注册免费域名请参考文章[2020年最新的国外免费顶级域名网站Freenom注册免费域名教程与Cloudflare托管解析的方法](https://iyideng.net/welfare/freenom-free-domain-register.html)

2）购买付费域名

购买付费域名推荐 [NameSilo(推荐)](https://ad.bgfw.me/NameSilo)、[Namecheap](https://ad.bgfw.me/Namecheap)或[Name.COM](https://www.name.com/zh-cn/referral/3933a3)，大部分域名一般不到4美元/第1年，像 .xray 和 .top 这样顶级域名还不到1美元/年，非常划算，第2年重新注册一个新的就可以了。

如果你打算在 NameSilo 注册域名的话，请参考文章:[NameSilo – 美国知名域名注册商 | 仅年付0.99/1.99美元 | 域名购买与账户注册图文教程](https://iyideng.net/note/namesilo-domain-registrar.html)

3）解析域名

注册好域名之后，请把域名解析到你要搭建SSR服务器所用VPS对应的IP地址，一般5分钟之内就可以生效，最迟72小时生效。我一直推荐大家使用 Cloudflare 管理域名，解析速度快，基本秒生效，非常方便快捷，而且 Cloudflare 的免费 CDN 很好用，而且搭建自用SS/SSR/V2Ray/Trojan机场经常会用到。

关于互联网域名注册、购买与添加DNS域名解析记录的详细操作教程，请参考文章:[互联网域名注册、服务购买与添加域名解析记录及更改DNS服务器的详细图文教程](https://iyideng.net/note/domain-name-registration-buy-resolution-and-change-dns.html)

### （2）购买非中国大陆地区的VPS
关于 Vultr 的账户注册、套餐购买和VPS服务器系统安装与远程管理的详细使用教程，请参考:[最新Vultr账户注册、VPS套餐购买与服务器系统安装以及SSH远程管理的详细图文教程](https://iyideng.net/special/vps/latest-vultr-vps-registration-purchase-and-installation-system-tutorial.html)鉴于图文教程已经非常详尽，我这里就不再赘述，我后面的图文教程均以 Vultr VPS 为例进行演示。

1）为什么要购买非中国大陆地区的VPS？

因为中国大陆经营的正规VPS提供商都在国家正规备案的，不允许你搭建ShadowsocksR/SSR节点服务器，一旦发现你违规使用会停掉你的VPS，还可能不退款。另外，即使你可以搭建科学上网服务器，而且没有被发现，那么也可能被监控，并有隐私泄露的风险，因为像国内大厂的云产品上面都有监控代码，你未必能清理干净。鉴于以上原因，我建议你选择非天朝公司且不在大陆备案经营的VPS提供商。

2）使用香港或者澳门公司的VPS怎么样？

当然是可以的，但是他们都很贵，而且仍是天朝下辖地区，还是不碰为好。我推荐你选择美国、台湾、日本、新加坡、韩国等地区机房的VPS，甚至欧洲公司的产品，毕竟中国台湾还没有被统一，天朝直接管不了。

通过以上分析和介绍，我相信你也不愿意选择阿里云、腾讯云、百度云和华为云等这样的国内大公司的VPS，最好选择美国西海岸、日本东京或新加坡机房的VPS。

3）用什么VPS搭建SSR最划算？

国外VPS哪家好？搭建ShadowsocksR/SSR服务器推荐你使用[Vultr](https://iyideng.net/special/vps/latest-vultr-vps-registration-purchase-and-installation-system-tutorial.html)、[BandwagonHOST](https://ad.bgfw.me/BandwagonHOST)、[Hostwinds](https://ad.bgfw.me/Hostwinds)等大公司的VPS，其中Vultr是最为推荐的，因为它可以非常方便且无限制地免费更换IP，而且在全球拥有17个数据中心；其次，推荐你使用 BandwagonHOST(搬瓦工)，速度稳定，而且性价比非常高，缺点是换IP比较贵；鉴于 Host winds IP地址资源比较少，不再推荐。如果你是老鸟的话，使用哪一家VPS都不错，新手的话还是推荐 Vultr，毕竟免费换IP是杀手锏，以前BandwagonHOST(搬瓦工) 也是这么起家的。

## 2、远程连接并管理 Vultr VPS 服务器

关于 Xshell/Putty 远程连接并管理 Vultr VPS 服务器的详细使用教程，请参考[最新Vultr账户注册、VPS套餐购买与服务器系统安装以及SSH远程管理的详细图文教程，鉴于图文教程](https://iyideng.net/special/vps/latest-vultr-vps-registration-purchase-and-installation-system-tutorial.html#5SSH_lian_jie_yuan_cheng_Vultr_VPS)已经非常详尽，我这里就不再赘述。

当完成 Vultr 账户注册、套餐购买并成功连接到远程 VPS 之后，我们就可以继续下面的步骤了。

## 3、一键搭建ShadowsocksR/SSR服务器教程

我这里选择 Vultr VPS 服务器位置在 Seattle(美国西雅图)，安装 CentOS 7 X64 系统，使用 Xshell 远程登陆 Vultr VPS 进行操作，然后我们就可以一键搭建ShadowsocksR/SSR服务器了。具体操作步骤如下：

#### （1）安装 wget 命令

```bash
yum -y install wget #CentOS
sudo apt-get install wget #Debian/Ubuntu
```

#### （2）ShadowsocksR/SSR一键搭建脚本（无需绑定域名）

我们一键搭建ShadowsocksR/SSR服务器有2款一键脚本可以使用，分别是 秋水逸冰(Teddysun) 和 逗比大神(ToyoDAdoubi) 的作品，我建议你使用SSR一键搭建脚本最新的版本。其中，逗比大神(ToyoDAdoubi) 的作品是全中文安装选项的一键脚本，而且支持多用户、多端口和限流等功能，管理功能也更强大，很适合小白萌新用户使用。

### 1）秋水逸冰(Teddysun)的ShadowsocksR/SSR一键搭建脚本

此一键安装脚本支持 CentOS 6+、Debian 7+、Ubuntu 12+ 及以上系统版本，内存要求：≥128M，不支持“WS+TLS+CDN”，也不需要绑定域名。

```bash
wget --no-check-certificate -O shadowsocks-all.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-all.sh
chmod +x shadowsocks-all.sh
./shadowsocks-all.sh 2>&1 | tee shadowsocks-all.log
```

将以上命令粘贴到 Xshell 窗口，回车执行代码，然后输入“2”（即选择“2) ShadowsocksR”安装选项），回车后进入搭建ShadowsocksR/SSR服务器向导。如下图所示：

![一键搭建ShadowsocksR-SSR服务器4合1一键安装脚本](https://user-images.githubusercontent.com/76632179/120875604-40c58f00-c5df-11eb-8686-221294cb0436.png)

我这里以选择“**2) ShadowsocksR**”为例进行演示，输入数字“2”后回车，然后进入ShadowsocksR服务器的参数配置选项，依次为“服务器连接密码”、“服务器端口”、“数据加密方式”、“数据传输协议”和“混淆方式”（图中红杠和箭头标识的内容仅为演示，请根据你自己的需求输入即可）。其中，我这里建议你选择chacha20相关的加密方式（因为这些新加密方式的抗封锁效果更好）。如下图所示：

![一键搭建ShadowsocksR-SSR服务器4合1一键安装脚本配置选项](https://user-images.githubusercontent.com/76632179/120875658-87b38480-c5df-11eb-8834-d4101ab505b2.png)

当以上参数选项都输入完毕后，回车。然后系统会提示“Press any key to start…or Press Ctrl+C to cancel“，即按任意键继续。当我们按任意键之后，系统会进入安装ShadowsocksR/SSR服务的过程，稍等片刻即可完成。安装ShadowsocksR服务成功完成后，如下图所示：

![一键搭建ShadowsocksR-SSR服务器4合1一键安装脚本执行完毕](https://user-images.githubusercontent.com/76632179/120875669-939f4680-c5df-11eb-96e7-be7bf11c4091.png)

如上图所示，其中各项参数释义如下：

- Your Server IP :你的服务器 IP 地址；
- Your Server Port :你的服务器端口；
- Your Password :你的连接密码；
- Your Protocol : 你的数据传输协议；
- Your obfs : 你的混淆方式；
- Your Encryption Method:你的加密方式；
- Your QR Code:你的SSR链接；
- Your QR Code has been saved as a PNG file path:你的SSR链接二维码图片的存放位置。

至此，你已经成功搭建ShadowsocksR/SSR服务器，现在就可以科学上网了，但启用BBR加速后效果更好。

### 2）逗比大神(ToyoDAdoubi)的ShadowsocksR/SSR一键搭建脚本（推荐）

我推荐新手小白用户使用逗比大神(ToyoDAdoubi)的SSR一键搭建脚本，因为全中文界面，操作更加简单方便。

`我推荐新手小白用户使用逗比大神(ToyoDAdoubi)的SSR一键搭建脚本，因为全中文界面，操作更加简单方便。`

此一键安装脚本支持 CentOS 6+、Debian 7+、Ubuntu 12+ 及以上系统版本，内存要求：≥128M，不支持“WS+TLS+CDN”，也不需要绑定域名。

```bash
wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubi/doubi/master/ssr.sh && chmod +x ssr.sh && bash ssr.sh
```

将以上命令粘贴到 Xshell 窗口，回车执行代码，然后出现“ShadowsocksR 一键管理脚本”的管理菜单。如下图所示：

![逗比大神ToyoDAdoubi-的ShadowsocksR-一键管理脚本](https://user-images.githubusercontent.com/76632179/120875807-54252a00-c5e0-11eb-96a6-d2eb0a0f3591.png)

我们输入数字“1”后，回车进入安装ShadowsocksR服务器的参数配置选项，依次为“服务器端口”、“服务器连接密码”、“数据加密方式”、“混淆方式”（图中红杠和箭头标识的内容仅为演示，请根据你自己的需求输入即可）。其中，我这里建议你选择chacha20相关的加密方式（因为这些新加密方式的抗封锁效果更好）。如下图所示：

![逗比大神ToyoDAdoubi-的一键搭建ShadowsocksR-SSR服务器4合1一键安装脚本配置选项1](https://user-images.githubusercontent.com/76632179/120875821-630bdc80-c5e0-11eb-8c55-fcf6c7a23bec.png)

![逗比大神ToyoDAdoubi-的一键搭建ShadowsocksR-SSR服务器4合1一键安装脚本配置选项2](https://user-images.githubusercontent.com/76632179/120875838-7d45ba80-c5e0-11eb-81a5-d8faff8f40e3.png)

当以上参数选项都输入完毕后，敲击回车键，然后系统会提示“[ 信息 ] 开始安装/配置 ShadowsocksR依赖…“。安装过程中，如果遇到“Is this ok？”提示，输入“y”回车即可，稍等几分钟即可完成安装。成功安装后，如下图所示：

![逗比大神ToyoDAdoubi-的一键搭建ShadowsocksR-SSR服务器4合1一键安装脚本安装完成](https://user-images.githubusercontent.com/76632179/120875856-8b93d680-c5e0-11eb-9e51-6aca6e18a636.png)

以上所有参数信息都是中文，一看便懂，我这里就不再一一解释了。如果你要对SSR服务器参数进行调整，请再次执行一键安装脚本代码，即可进入ShadowsocksR服务器管理菜单。

### （3）“ShadowsocksR+TLS+Web+CDN”模式SSR一键搭建脚本（推荐，需绑定域名）

此一键安装脚本支持的服务器操作系统：Debian 9、10，Ubuntu 16.04 、18.04、19.10，Centos 7、8，我这里以Web服务器Caddy进行演示，你也可以使用安装Nginx，但是我推荐你使用Caddy，因为更轻量，而且会自动申请并更新HTTPS证书。

#### 1）安装 curl

```bash
yum -y install curl #CentOS
apt-get update #Debian/Ubuntu
apt -y install curl #Debian/Ubuntu
```
#### 注意事项：
如果您正在使用Debian/Ubuntu服务器系统，一灯不是和尚建议您先执行“apt-get update”命令，否则可能会出现提示“Unable to fetch some archives, maybe run apt-get update or try with –fix-missing?”。

#### 2）执行“8合1一键安装脚本”命令

```bash
bash -c "$(curl -fsSL https://raw.githubusercontent.com/JeannieStudio/all_install/master/SixForOne_install.sh)"
```

粘贴上述命令并回车，会显示此 SSR/V2Ray/Trojan+TLS+Web服务器8合1脚本 的功能菜单。如下图所示：

![SSR、V2Ray、Trojan-TLS-Web服务器-8合1一键脚本](https://user-images.githubusercontent.com/76632179/120876042-2e4c5500-c5e1-11eb-8c03-191765790b21.png)

我们选择“**7**”即可，然后回车，即“安装**ssr+tls+caddy**”，安装过程比较慢，大约需要近20分钟。安装期间，一共出现4次交互，第1次交互需要输入绑定的域名，输入完成后回车。如下图所示：

![安装ssrtlscaddy期间输入要绑定的域名](https://user-images.githubusercontent.com/76632179/120876098-710e2d00-c5e1-11eb-864c-d8aea5c497b4.png)

第2次交互是需要从十多个Caddy安装源中选择任意一个安装即可，输入数字后回车。

第3、4次交互是在一键安装脚本末尾的时候，根据自己的需要修改服务器端口号和连接密码。如下图所示：

![安装ssrtlscaddy脚本后修改服务器端口和连接密码](https://user-images.githubusercontent.com/76632179/120876106-79666800-c5e1-11eb-961b-8b01e3bff00a.png)

当自定义服务器端口和连接密码完成后，回车。稍等片刻即可完成整个安装过程，安装成功后，显示完整的SSR服务器配置信息，如下图所示：

![安装ssrtlscaddy脚本成功后配置信息](https://user-images.githubusercontent.com/76632179/120876113-82573980-c5e1-11eb-96d1-84d1b894e495.png)

至此，你已经使用以上3种方法成功搭建ShadowsocksR/SSR服务器，现在就可以科学上网了，但安装 BBR 一键加速后速度会更快。此一键脚本的好处就是可以套Cloudflare的免费CDN，更好地保护VPS的真实IP地址，而且免费使用CDN流量，极大地节省了带宽流量。

## 4、一键安装并开启BBR加速

一键安装BBR加速脚本，执行如下命令：

```bash
cd /usr/src && wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
```

执行以上安装命令后，如下图所示：

![BBR加速TCP加速-一键安装管理脚本](https://user-images.githubusercontent.com/76632179/120876148-b03c7e00-c5e1-11eb-9d0e-aa7f9c591bd9.png)

我这里选择“**2**”，“安装 BBRplus版内核”加速。在安装过程中，可能会出现如下提示，用右方向键选“<No>”，然后回车。如下图所示：
  
![TCP加速-一键安装管理脚本-移除原内核警示](https://user-images.githubusercontent.com/76632179/120876170-cb0ef280-c5e1-11eb-81c2-5a392b91a6de.png)

安装完成后会提示重启服务器，这时候输入字母“y”，回车后，重启服务器。当服务器启动后，我们再次执行安装命令，选择“7”启用“使用BBRplus版加速”。

## 5、ShadowsocksR/SSR客户端配置



  



























