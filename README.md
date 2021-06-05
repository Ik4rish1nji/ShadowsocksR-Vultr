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

### （1）安装 wget 命令

```bash
yum -y install wget #CentOS
sudo apt-get install wget #Debian/Ubuntu
```

### （2）ShadowsocksR/SSR一键搭建脚本（无需绑定域名）

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










