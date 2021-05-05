# 前言

为什么要做这个库？因为有句话说“不会翻墙的程序员不是好程序员”，但是某些原因，翻墙可是越来越难了，我之前是用某灯，但是自从上个月开始某灯也不稳定了；我还以为可以和某灯相宿相飞一段时间的，后来就投靠了Shadowsocks了，为什么会选择Shadowsocks呢，因为可以自己搭建服务器，不再受牵制，而且由于是个人服务器被封IP的几率也不会很大；当然你也可以和自己信任的人共享使用，但是Shadowsocks的教程网络上真是参次不齐，很容易误导那些只想翻墙而不是要了解它原理的人，所以我就蹦出个想法：做个几乎是一键式的傻瓜Shadowsocks（以下简称ss）搭建教程给小白们，让大家都能共享自由的互联网。

# 开始

## 购买VPS服务器

俗话说，万事起头难。想想倒也是这样，也不是说购买VPS服务器有多难，是接受它比较难，我当时也是一个还没买过服务器的小白，对于第一次尝试的东西都没有底，怎么敢随意下手。好了，你现在可以放心了，据我使用，Vultr和DigitalOcean这两个服务商都是可以随时部署随时摧毁服务器，是按每小时计费的，一个月是5美金，大概0.007美金一小时，就算你创建一个服务器IP刚好是被某墙屏蔽了，那就删掉也只是扣0.1美金，作为一个穷学生的我都能接受了，你还犹豫吗？

### 1、注册并登录

Vultr推荐链接：https://www.vultr.com/?ref=7738153

这里我比较推荐Vultr，为什么呢？因为他有日本服务器，延迟低，掉包也低；**但是后面我会推荐大学生使用DigitalOcean（以下简称DO），因为Github学生包有DO优惠劵，但是只限于大学生领取，如果是学生可以关注后面。**注册登录后先充值5美金，用paypal绑定国内银行卡可以最低充值5美金，当然也有支付宝，支付宝要最低10美金。

![](./images/1.png)

### 2、部署服务器

第一步：在个人页面点击Servers然后再点右面的➕号按钮添加一个服务器

![](./images/2.png)

第二步：在打开的页面选择Tokyo日本服务器，如果喜欢其他服务器也可以选择，后续操作是一样一样的

![](./images/3.png)

第三步：接下来要注意了，系统最好选择CentOS 6，点击CentOS可以下拉选择6

![](./images/4.png)

第四步：选择套餐，当然ss不需要配置太高的服务器，最低配置5美金一个月的就可以了，反正我每次看2.5美金都是卖光的，如果你能看到那赶紧选啊，千年一遇。

![](./images/5.png)

第五步：接着就是部署起来了，当然你也可以给服务器起个名字再部署

![](./images/6.png)

第六步：接着等待服务器启动完成，看到Status是绿色的Running就是启动完成了，这个过程大概需要1-3分钟。

![](./images/7.png)

第七步：复制IP地址和密码，后面有用

![](./images/8.png)

第八步：启动完成后，当然测试一下有没有被封掉IP了，打开命令管理器或者终端，输入 ping+你的IP地址，例如我服务器IP是8.8.8.8，则ping 8.8.8.8，如果出现下图的返回信息则这个IP是可以用的，偶尔一个request timeout也是可以的，是掉包现象，如果出现一直request timeout就把这服务器删掉重新部署吧。

![](./images/10.png)

好了，到此为止最困难的事情已经过去了，后面都是一键式的了，喝杯茶🍵再继续。

## 在服务器安装ss

因为我是用mac的，考虑到大多数人还是使用windows为主，我就把我的旧电脑给翻出来开机继续做教程。基于windows 7。

**如果你是用mac，那恭喜你，下面连接的步骤直接打开终端输入 **

**`ssh root@你的服务器IP地址`**

**连接就可以，然后可以跳过安装并运行xshell这个步骤**

### 安装并运行xshell

windows下ssh连接需要下载Xshell，百度搜一搜就能下载了，当然你也可以用其他的，这里以Xshell为例，安装好Xshell后点击文件-新建

![](./images/w-1.png)

接下来配置连接,名称随便起，主机填写你的服务器IP地址，下面都默认就好

![](./images/w-2.png)

接下来在弹出的窗口填root（默认服务器用户名）

![](./images/w-3.png)

这里就要填入你在上篇复制的服务器密码了

![](./images/w-4.png)

### 安装ss

上面登录成功后如图所示

![](./images/w-5.png)

下面就是精髓的部分了，感谢[@teddysun](https://github.com/teddysun)大佬制作的一键安装脚本，具体更多细节可查看博客：https://teddysun.com/486.html

```
wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh && chmod +x bbr.sh
./bbr.sh
lsmod | grep bbr

wget --no-check-certificate -O shadowsocks-all.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-all.sh
chmod +x shadowsocks-all.sh
./shadowsocks-all.sh 2>&1 | tee shadowsocks-all.log
```

复制粘贴上面代码到xshell，在xshell要右键粘贴，然后就会有一大串不知名代码蹦出，停在这里了

![](./images/w-6.png)

这时候按一下Enter回车键它又可以继续了～

接着又蹦出些东西，是让我们选择ss的服务器端，这里我选择go版本的，输入3按回车

![](./images/w-7.png)

如同往常，接下来是要填入ss客户端登录的密码，这里我随意填：abc123456

![](./images/w-8.png)

接下来是输入端口号（1-65535任意数字），这里我填默认的

![](./images/w-9.png)

接下来是选择加密方式，默认就好，按回车

![](./images/w-10.png)

接着又是反手一个回车就好

![](./images/w-11.png)

这里可能需要等待一会，看到下图就是大功告成了。干杯🍻！

这个最好截图一下，以防忘记了。

我就当大家英文水平还好吧，下面说的就是你的服务器IP，服务器端端口，密码，加密方式。

![](./images/w-12.png)

## 下载客户端

如果你跟着我到了这一步就代表安装好了服务器端，但是我们的电脑手机作为客户端也是需要安装客户端软件的。下面是各个终端的下载地址（我用过Windows,MAC,Android,IOS操作起来都是差不多的。）：

Windows：https://github.com/shadowsocks/shadowsocks-windows/releases

MAC:https://github.com/shadowsocks/ShadowsocksX-NG/releases

Android:https://github.com/shadowsocks/shadowsocks-android/releases

Linux:https://github.com/shadowsocks/shadowsocks-qt5/wiki/Installation

IOS: 

由于国区APP下架VPN类APP，包括支持ss类的APP，所以需要切换账号

建议注册一个国外账号，不要国内账号换区，这样既可以需要下载国内APP时切换国区账号，需要下载国外APP时切换外区账号。

步骤：

1.获取一个国区以外的账号

注册国外appid教程：https://www.zhihu.com/question/26458172

（相关注册外区账号教程很多，可以自行搜索）

**由于苹果的新政策，注册apple id在付款方式选择的时候非当地ip无法选择none选项，例如我注册英国区账号，需要ip为英国才可以。即在注册时要搭梯子，对应ip注册。**

2.在APPStore中切换为国区以外账号

3.在AppStore搜索**Potatso Lite**安装

注：或者其他支持shadowsocks的APP也可以，这里比较推荐Potatso Lite
- [Potatso Lite](https://itunes.apple.com/us/app/potatso-lite/id1239860606?mt=8)
- [Wingy](https://itunes.apple.com/us/app/wingy-http-s-socks5-proxy-utility/id1178584911)
- [Big Boss](http://apt.thebigboss.org/onepackage.php?bundleid=com.linusyang.shadowsocks)



下面以windows为例演示：

打开上方网址下载客户端：

![](./images/w-13.png)

接着安装打开后配置服务器：

还记得上面建议保存的图片吗？这里就用到了，服务器IP，端口，密码，加密方式，然后点击确定

![](./images/w-14.png)



接着启用系统代理：

![](./images/w-15.png)



- 这里简要说一下PAC模式和全局模式问题：

PAC模式就是访问国内网站会走国内IP，访问被封的网站走服务器IP

全局就是全部走服务器IP

这里建议选择PAC模式，PAC的地址都是保存在[gfwlist](https://github.com/gfwlist/gfwlist)

希望大家遇到PAC无法访问的网站多上去提issues。

### 神圣时刻

接着最神圣的时刻来了，在浏览器输入google.com，回车，蹦，谷歌回来了

![](./images/w-16.png)

# 最后

最后，这里我们的任务完成了，但是如果你想优化一下服务器连接，可以安装BBR加速。具体可以看这篇文章尾部：[文章](https://github.com/Alvin9999/new-pac/wiki/%E8%87%AA%E5%BB%BAss%E6%9C%8D%E5%8A%A1%E5%99%A8%E6%95%99%E7%A8%8B)

> 连接服务器ip，登录成功后，在命令栏里粘贴以下代码：
>
> 【谷歌BBR加速教程】
>
> yum -y install wget
>
> wget --no-check-certificate <https://github.com/teddysun/across/raw/master/bbr.sh>
>
> chmod +x bbr.sh
>
> ./bbr.sh
>
> 把上面整个代码复制后粘贴进去，不动的时候按回车，然后耐心等待，最后重启vps服务器即可。

# 更新
## 180624更新
如果要PAC自定义规则，即譬如你要上的网站不在PAC目录里，可以自己添加
譬如我要加github进入PAC自定义协议里
格式如下：

```
||github.com
```

添加进去后,**记得重启一下Shadowsocks让它生效**

api.github.com 

github.com/zhaoweih

等等包含github.com的URL都会走服务器IP


# 建议

如果大家对这篇文章有任何疑问都可以提[issues](https://github.com/zhaoweih/Shadowsocks-Tutorial/issues)，如果你有其他更简单或者其他方法翻墙也可以pull requests。

**关于大学生领取Github包50美金DO优惠劵教程过阵子再更新。有感兴趣的同学可以自行搜索查看先。**

# 关于

我是一名普通的大三学生，一个追求自由的少年，如果想要找我，可以给我发邮件📧

📮我的邮箱：zhaoweihao.dev@gmail.com



# 赞赏

作为学生我目前生活还是蛮自如的，有吃的有喝的，就不用赞赏了。喜欢就给我个star或者fork一下吧❤️，谢谢！
