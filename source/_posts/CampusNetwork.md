---
title: 与校园网斗智斗勇
date: 2022-04-04 15:13:35
tags: 校园网多设备
categories: 校园网
cover: /img/CamNet.png
---

{% note blue 'fas fa-bullhorn' flat %}本篇文章并非原创{% endnote %}

# 目前已知的（可能）校园网共享上网检测机制有：

- 基于 IPv4 数据包包头内的 TTL 字段的检测

- 基于 HTTP 数据包请求头内的 User-Agent 字段的检测

- DPI (Deep Packet Inspection) 深度包检测技术

- 基于 IPv4 数据包包头内的 Identification 字段的检测

- 基于网络协议栈时钟偏移的检测技术

- Flash Cookie 检测技术

## 基于 IPv4 数据包包头内的 TTL 字段的检测

> 存活时间（Time To Live，TTL），指一个数据包在经过一个路由器时，可传递的最长距离（跃点数）。 每当数据包经过一个路由器时，其存活次数就会被减一。当其存活次数为0时，路由器便会取消该数据包转发，IP网络的话，会向原数据包的发出者发送一个ICMP TTL数据包以告知跃点数超限。其设计目的是防止数据包因不正确的路由表等原因造成的无限循环而无法送达及耗尽网络资源。

这是一个比较有效且合理的检测技术，IPv4数据包下存在 TTL（Time To Live）这一字段，数据包每经过一个路由器（即经过一个网段），该TTL值就会减一。

不同的操作系统的默认 TTL 值是不同的，Windows 是 128， macOS/iOS、Linux 是 64。

因此如果我们自己接入路由器到校园网，我们的通过路由器的数据包会变为 127 或 63，一旦校园网抓包检测到这种数据包TTL不是128或64，就会判定为用户接入了路由器。

## 基于 HTTP 数据包请求头内的 User-Agent 字段的检测

HTTP数据包请求头存在一个叫做 User-Agent 的字段，该字段通常能够标识出操作系统类型，例如：

> Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.72 Safari/537.36 Edg/89.0.774.45

> Mozilla/5.0 (iPad; U; CPU OS 3_2_1 like Mac OS X; en-us) AppleWebKit/531.21.10 (KHTML, like Gecko) Mobile/7B405

校园网会通过多次抓包检测此字段，若发现同时出现例如Windows NT 10.0 iPad 的字段，则判定存在多设备上网。

## DPI (Deep Packet Inspection) 深度包检测技术

这个检测方案比较先进，检测系统会抓包分析应用层的流量，根据不同应用程序的数据包的特征值来判断出是否存在多设备上网。

具体可参考：[基于dpi技术的网络共享设备检测方法及系统](https://patents.google.com/patent/CN106411644A/zh)

此种方式已确认在锐捷相关设备上应用，当由于此项功能极耗费性能，因此有些学校可能不会开启此项功能。

## 基于 IPv4 数据包包头内的 Identification 字段的检测

IP报文首部存在一个叫做 Identification 的字段，此字段用来唯 一标示一个IP报文，在实际的应用中通常把它当做一个计数器，一台主机依次发送的IP数据包内的 Identification 字段会对应的依次递增，同一时间段内，而不同设备的 Identification 字段的递增区间一般是不同的，因此校园网可以根据一段时间内递增区间的不同判断出是否存在多设备共享上网。

具体可以参考此专利：[基于ipid和概率统计模型的nat主机个数检测方法](https://patents.google.com/patent/CN104836700A/zh)

不过经过我的抓包分析，Windows 的TCP/IP协议栈对 Identification 字段的实现是递增，而 iOS 的实现是保持全0，因此校园网是否使用了该检测机制有待商榷。

## 基于网络协议栈时钟偏移的检测技术

不同主机物理时钟偏移不同，网络协议栈时钟与物理时钟存在对应关系，不同主机发送报文频率与时钟存在统计对应关系，通过特定的频谱分析算法，发现不同的网络时钟偏移来确定不同主机。

具体可以参考此专利：[一种基于时钟偏移的加密流量共享检测方法与装置](https://patents.google.com/patent/CN111970173A/zh)

此种方式具有一定的实验性，因此我不认为此种方式投入了商用。

## Flash Cookie 检测技术

这个技术已经用不到了，Flash都凉了。。不过还是提一下。

Flash Cookie会记录用户在访问 Flash 网页的时候保留的信息，只要当用户打开浏览器去上网，那么就能被 AC 记录到 Flash Cookie 的特征值，由于 Flash Cookie 不容易被清除，而且具有针对每个用户具有唯一，并且支持跨浏览器，所以被用于做防共享检测。

具体参考：[深信服防共享测试指导书](https://bbs.sangfor.com.cn/plugin.php?id=sangfor_databases:index&mod=viewdatabase&tid=6273)

# 防共享上网检测的解决方案

对于校园网重重的检测，我们似乎已经不可能从终端级提出一个完美的解决方案，因此，如果想要完美的解决方案需要基于网关级来进行配置。但经过测试在终端也有简单的不完美的方案，大概隔五六个小时可能会被检测到，全凭运气

## 基于 HTTP 数据包请求头内的 User-Agent 字段的检测

我们需要一种更加简单的方案，既能无需网关级编译OpenWrt，又能更好的满足我们的需求。

我们可以通过加密流量来实现防检测，因为进行全局加密网络流畅度影响太大， 而进行部分加密目前市面上还没有很好的解决方案（之前是这么认为），目前大多数加密软件都是基于规则的加密，但支持的多为针对域名的加密。

然而我们的需求是针对http应用层的加密，这类加密方案目前支持的不多。

经过我深入了解，Clash 中 DstPort 是我们最理想的规则选项，我们可以指定代理目标端口为http的80端口从而实现http应用层的加密。

此外，除了针对http的加密外，我们还可以通过支持Mitm的网络调试工具对http中UA进行重写以达到修改UA的目的。

基于上面的分析，我总结了以下方案：

### Windows 用户

使用Clash，添加规则：

```cmd
- DST-PORT,80,proxy
```

加入以上规则即可实现针对80端口的加密

### Andorid 用户

使用Clash，添加规则：

```cmd
- DST-PORT,80,proxy
```
{% note info flat %}注意：proxy是策略组名字{% endnote %}

加入以上规则即可实现针对80端口的加密

### iOS 用户

使用Quantumult X/Surge等支持重写的工具，添加重写规则：

```cmd
# Quantumult X
^http:// url request-header (\r\n)User-[A|a]gent:.+(\r\n) request-header $1User-Agent: F$2

# Surge
^http:// header-replace User-Agent F
```
加入以上规则即可实现针对UA的重写

### Mac 用户

使用Quantumult X/Surge等支持重写的工具，添加重写规则：

```cmd
# Quantumult X
^http:// url request-header (\r\n)User-[A|a]gent:.+(\r\n) request-header $1User-Agent: F$2

# Surge
^http:// header-replace User-Agent F
```

加入以上规则即可实现针对UA的重写

# 通过代理绕过检测

## 使用clash的创建代理

> 电脑连接校园网认证，能够正常使用网络

打开clash中的允许局域网连接的功能

![clash](/img/clash.png "clash")

打开之后，记住端口的名字`7890`,和WLAN的IP地址

## 使用手机连接代理

> 手机连接校园网WiFi，不进行认证，意思就是使用代理需要处在同一个局域网环境下

![修改网络](/img/daili1.jpg "修改网络")

长按修改网络，然后代理选择手动，服务器主机就是WLAN的IP，端口就是`7890`

![连接代理](/img/daili2.jpg "连接代理")

> 这个代理只能浏览网页，因为系统自带的代理服务有限制，经搜素好像可以使用软件进行全局的代理，但没有测试
> 因为本人没有资金，无力购买设备，没有一个可以供我玩耍的路由器，等以后购入后就不会使用这种方法了，这种方法太不稳定

{% tip %}
本文引用的文章
https://www.sunbk201.site/posts/change-ua-by-proxy.html
https://www.sunbk201.site/posts/crack-campus-network.html
{% endtip %}

