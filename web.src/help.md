## 访问更多域名

如果你是从github直接下载的release，exe同级目录下应该提供了`DragTheDomainConfigFileHere.bat`。

这会使用一个我自用的配置文件，也就是同目录下的`DOMAINconfig.txt`。这样可以访问更多网站，注意其对子域名敏感（子域名需要单独配置）。

对于该文件`DOMAINconfig.txt`的编辑，请往下翻。

## 命令行参数帮助

鉴于本应用名字较长，我强烈建议您把他的名字改短一点，比如`zlib.exe`。

默认接下来您已经进行了重命名。

### `-h`

打开帮助，也就是显示此文件。

### `-g url`

打开后跳转到url，而不是默认开始页。
注意：`url`必须带协议头，如：`https://1919810.com`。

### `-c [FILE]`

使用命令行配置文件。

如果有`[FILE]`，程序读取`FILE`，否则程序会尝试读取同一目录下的`CMDconfig.txt`。

该文件包含命令行。（通常用于开发人员）

```text
--host-resolver-rules="MAP zh.z-library.re [2606:4700:3033::ac43:aa46]:443,MAP bu2021.xyz [2606:4700:3033::6815:3e2]:443" -origin-to-force-quic-on=zh.z-library.se:443,bu2021.xyz:443
```

### `-d`

根据域名进行配置，要求IP支持QUIC，且能访问（一般指ping得通）（**必须支持QUIC**）。

如果有`[FILE]`，程序读取`FILE`，否则程序会尝试读取同一目录下的`DOMAINconfig.txt`。

我们通过空行来分割多个IP的配置，每份配置的第一行是该IP（支持IPv6），接下来若干行是你的域名（不包含协议头，如`https://`）。**注意，该方法对域名极其敏感，子域名是不一样的域名。如`www.pixiv.net`和`pixiv.net`不一样，`z-library.se`和`zh.z-library.se`不一样，*请注意。***

由于`-origin-to-force-quic-on`不支持通配符，所以除非你理解这个程序在干什么，不建议使用类似`*.114514.com`之类的通配符。

接下来任意多行是需要启用工具的域名，尽量不要太多，Windows命令行的长度是有限制的。（好像是$8192$个字符）

这个域名有两个工具选择，QUIC和丢弃sni。

+ 如果是QUIC，直接写上来。
+ 如果是丢弃sni，在行首加上`^`。（这是因为严格上来讲丢弃sni是非正常做法，所以使用特殊标识）
+ 如果只是修改dns，在行首加上`-`

以下是一个可行的配置：（这两个IP分别是CloudFlare的IPv4与IPv6之一，为了演示分开）。

```plaintext
[2606:4700:3033::ac43:aa46]
zh.z-library.se
bu2021.xyz
annas-archive.se
longlivemarxleninmaoism.online
zlib-articles.se
zh.zlib-articles.se

114.250.70.34
-www.recaptcha.net

172.64.145.17
www.pixiv.net

116.202.120.165
^www.torproject.org
```

### `-o`

页面将显示打开此次程序的浏览器命令行参数。

### `-a`

显示Android开启设置文本。

见Android设置帮助。

## 使用自己的浏览器

给你的浏览器（比如说`chrome.exe`）传参打开即可。

比如

```bash
chrome.exe --host-resolver-rules="MAP zh.z-library.re [2606:4700:3033::ac43:aa46]:443,MAP bu2021.xyz [2606:4700:3033::6815:3e2]:443" -origin-to-force-quic-on=zh.z-library.se:443,bu2021.xyz:443 --host-rules="MAP libgen.rs 193.218.118.42,MAP zh.singlelogin.re 176.123.7.105,MAP singlelogin.re 176.123.7.105" --ignore-certificate-errors
```

## 安卓配置指南

***本指南极其复杂，在决定踏上这条路前请三思！***

本教程测试于MIUI14（国内版）。

**遇到类似不安全或病毒报警，请自行判断是否继续。**

为了省流，我不打算配图片

### 第一部分：准备文件

#### 两个安装包

（`.apk`），提供的是两个链接，不保证可以下载。

+ [Termux](https://www.downkuai.com/android/140917.html)（知道F-droid的，推荐从Fdroid下载；如果你用电脑进行ADB，则不需要）
+ [KiWiBrowser](https://www.onlinedown.net/soft/10107048.htm)（建议用链接里的版本，切记不要`安全下载`！否则后果自负）（其他基于Chromium的浏览器也可，比如Chromium, Chrome, UngoogledChromium, Bromite，我之所以推荐kiwi是因为他支持扩展，这也是我自用的浏览器之一，且是最常用的浏览器）

#### 一句命令

先关闭本软件，再点开本软件安装包同级目录下的`GetAndroidADBCommandLine.bat`，本软件会重新打开，然后复制上面的第一行内容（以`_`开头）

你会得到类似这样的东西：

```text
echo "_ --host-resolver-rules=\"MAP bu2021.xyz 172.64.145.17:443,MAP annas-archive.se 172.64.145.17:443\" -origin-to-force-quic-on=bu2021.xyz:443,annas-archive.se:443 --host-rules=\"MAP libgen.rs 193.218.118.42,MAP zh.singlelogin.re 176.123.7.105,MAP singlelogin.re 176.123.7.105\" --ignore-certificate-errors" > chrome-command-line
```

### 第二部分：开启ADB

这里提供一个MIUI下利用Termux作为终端的例子。

#### 安装Termux并作准备

进入Termux后，是一个命令行界面。

你可以考虑换清华源，见[镜像站官方帮助文档](https://mirrors.tuna.tsinghua.edu.cn/help/termux/)

依次执行以下命令：（如果遇到提问，直接`Enter`走默认）

```bash
apt update
apt upgrade
pkg install android-tools
```

#### 连接ADB

其他系统（UI）请自行搜索或探索办法。

请务必连上WIFI（其实不重要，但是MIUI无线调试必须连wifi才能开启，所以这个网慢不慢不重要，其实这个操作根本不用连网）

1. 点开`设置`
2. 点开`我的设备`
3. 点开`全部参数于信息`
4. 快速点击`MIUI版本`五次，会看到消息框`您现在处于开发者模式！`
5. 不停点击返回回到`设置`根菜单
6. 找到`更多设置`，进入
7. 进入`开发者选项`
8. 找到`无线调试`，进入，启用
9. 与之前开启的`Termux`窗口分屏（小窗也可以，不能切后台，重要！）
10. 点开使用配对码配对设备
11. 会弹出来一个报告小窗窗，上面有`WLAN配对码`，是6个数字，记下来，比如说是`114514`；还有一个`IP地址和·端口`（显示在报告小窗上那个），记下来，比如说是`192.168.2.114:42257`
12. 进入`Termux`，打命令并`Enter`
    
    ```bash
    adb pair 192.168.2.224:42257 114514
    ```
    
    根据上一步得到数据自行修改）。然后应该会显示类似`Pair Successfully`之类的，你没看到`Error`或者`ERR`就行。
13. 回到无线调试设置，你应该会看到一个已配对设备，继续。这次我们选在主窗口上的`IP地址和端口`，记下来，比如说是`192.168.2.114:42819`。
    键入并`Enter`
    
    ```bash
    adb connect 192.168.2.114:42819
    ```
    
    应该返回`Connected Successfully`之类的，然后无线调试窗口的已配对设备会显示已连接，连接完成。`Termux`不要退出。

#### 设置command-line

上一步完成后，继续键入命令并`Enter`（比如说在`Termux`里）。

```bash
adb shell
cd /data/local/tmp
```

然后把你之前获取的那段命令键入并`Enter`，比方说

```bash
echo "_ --host-resolver-rules=\"MAP bu2021.xyz 172.64.145.17:443,MAP annas-archive.se 172.64.145.17:443\" -origin-to-force-quic-on=bu2021.xyz:443,annas-archive.se:443 --host-rules=\"MAP libgen.rs 193.218.118.42,MAP zh.singlelogin.re 176.123.7.105,MAP singlelogin.re 176.123.7.105\" --ignore-certificate-errors" > chrome-command-line
```

接下来

```bash
echo "$(<chrome-command-line)"
```

会输出类似这样的内容：

```text
_ --host-resolver-rules="MAP bu2021.xyz 172.64.145.17:443,MAP annas-archive.se 172.64.145.17:443" -origin-to-force-quic-on=bu2021.xyz:443,annas-archive.se:443 --host-rules="MAP libgen.rs 193.218.118.42,MAP zh.singlelogin.re 176.123.7.105,MAP singlelogin.re 176.123.7.105" --ignore-certificate-errors
```

OK，键入

```bash
exit
adb disconnect
```

关闭无线调试，关闭开发者模式，关闭Termux。

### 第三部分：打开ChromeFlag

还记得Kiwi吗。

进入，一路瞎点。

地址栏输入

```text
chrome://flags/
```

搜索`Command`，找到`Enable command line on non-rooted devices`，设置为`Enabled`。

退出Kiwi，杀掉所有进程，**重启手机**。

### 第四部分：确认设置成功

重新打开Kiwi。

地址栏输入

```text
chrome://version/
```

确认命令行栏有`_`打头，如果没有，再次杀掉所有进程，重启，不断重复知道出现`_`。

### 第五部分：愉快上网

使用KiWi浏览器，键入`https://zh.singlelogin.re`

## 安卓更新指南

1. 重新连接adb（如果你没有卸载Termux，不用`pair`，直接`connect`即可）。
2. 设置command-line。
3. 退出Kiwi，杀掉所有进程，重启手机。

## 域名添加与访问指南

如果你发现了有一个域名无法连接，可以尝试配置。

### 首先你要找到域名对应的IP

#### 网站查询

洁净域名IP查询：[Whois365](https://www.whois365.com/)（非广告）

接下来，确保ping通这个IP（请自行查找ping的方式）。

或者，如果你明确该域名使用了cdn，可以尝试自选ip。

以CloudFlare为例你可以到[这里](https://www.cloudflare-cn.com/ips/)寻找一个CloudFlareCDN的IP。并请确保ping得通。（一般可以）

#### 浏览器查询

由于Whois365有的域名查不到，也可以浏览器查。

先将dns换为Cloudflare DoH，打开[Chrome内置DNS查询](chrome://net-internals/#dns)

输入，查询即可。再将得到的IP丢Whois365里查。

### 明确过墙的方式

这里有两种方式：QUIC与丢弃SNI。

一一尝试。

### 访问域名

注意，当你跳转的时候，对域名和协议极其敏感。

**注意子域名[^1]也要。**

**如果还不行，那一般就是不行。**

> 我这里收集了上述特殊情况：
> 
> + Pornhub的IP是可以直连的，但是用HostRules实现的域前置使用了IP作为sni，而这个ip在黑名单里。
> + Odysee的账号网址`odysee.tv`使用了Cloudfare CDN，无法域前置，但是手动关闭了QUIC。
> + TorProject的域前置实现比较魔幻，有的时候会当成IP直连，甚至因服务器IP而异。

### 其他情况

如果出现HTTP协议，或者非标准端口，请采用`CMDconfig`。

<details>
<summary>或者自己编写命令行。请参考：Chromium NewWork Configs Codes：</summary>

```java
// from: https://chromium.googlesource.com/chromium/src/+/refs/heads/main/components/network_session_configurator/common/network_switch_list.h
// Copyright 2017 The Chromium Authors
// Use of this source code is governed by a BSD-style license that can be
// found in the LICENSE file.
// This file deliberately has no header guard, as it's inlined in a number of
// files.
// no-include-guard-because-multiply-included
// Disables the QUIC protocol.
NETWORK_SWITCH(kDisableQuic, "disable-quic")
// Disables the HTTP/2 protocol.
NETWORK_SWITCH(kDisableHttp2, "disable-http2")
// Enables Alternate-Protocol when the port is user controlled (> 1024).
NETWORK_SWITCH(kEnableUserAlternateProtocolPorts,
               "enable-user-controlled-alternate-protocol-ports")
// Enables the QUIC protocol.  This is a temporary testing flag.
NETWORK_SWITCH(kEnableQuic, "enable-quic")
// Ignores certificate-related errors.
NETWORK_SWITCH(kIgnoreCertificateErrors, "ignore-certificate-errors")
// Specifies a comma separated list of host-port pairs to force use of QUIC on.
NETWORK_SWITCH(kOriginToForceQuicOn, "origin-to-force-quic-on")
// Disables known-root checks for outgoing WebTransport connections.
NETWORK_SWITCH(kWebTransportDeveloperMode, "webtransport-developer-mode")
// Specifies a comma separated list of QUIC connection options to send to
// the server.
NETWORK_SWITCH(kQuicConnectionOptions, "quic-connection-options")
// Specifies a comma separated list of QUIC client connection options.
NETWORK_SWITCH(kQuicClientConnectionOptions, "quic-client-connection-options")
// Specifies the maximum length for a QUIC packet.
NETWORK_SWITCH(kQuicMaxPacketLength, "quic-max-packet-length")
// Specifies the version of QUIC to use.
NETWORK_SWITCH(kQuicVersion, "quic-version")
// Allows for forcing socket connections to http/https to use fixed ports.
NETWORK_SWITCH(kTestingFixedHttpPort, "testing-fixed-http-port")
NETWORK_SWITCH(kTestingFixedHttpsPort, "testing-fixed-https-port")
// Comma-separated list of rules that control how hostnames are mapped.
//
// For example:
//    "MAP * 127.0.0.1" --> Forces all hostnames to be mapped to 127.0.0.1
//    "MAP *.google.com proxy" --> Forces all google.com subdomains to be
//                                 resolved to "proxy".
//    "MAP test.com [::1]:77 --> Forces "test.com" to resolve to IPv6 loopback.
//                               Will also force the port of the resulting
//                               socket address to be 77.
//    "MAP * baz, EXCLUDE www.google.com" --> Remaps everything to "baz",
//                                            except for "www.google.com".
//
// These mappings apply to the endpoint host in a net::URLRequest (the TCP
// connect and host resolver in a direct connection, and the CONNECT in an http
// proxy connection, and the endpoint host in a SOCKS proxy connection).
//
// TODO(mmenke): Can we just remove this?  host-resolver-rules is more generally
// useful.
NETWORK_SWITCH(kHostRules, "host-rules")
// Enable "greasing" HTTP/2 frame types, that is, sending frames of reserved
// types.  See https://tools.ietf.org/html/draft-bishop-httpbis-grease-00 for
// more detail.
NETWORK_SWITCH(kHttp2GreaseFrameType, "http2-grease-frame-type")
// If request has no body, close the stream not by setting END_STREAM flag on
// the HEADERS frame, but by sending an empty DATA frame with END_STREAM
// afterwards.  Only affects HTTP/2 request streams, not proxy or bidirectional
// streams.
NETWORK_SWITCH(kHttp2EndStreamWithDataFrame, "http2-end-stream-with-data-frame")
```

</details>

## 有问题请加Github issue。

## 版权声明

本文档除引用的Chromium源码外部分按照[GFDL](https://www.gnu.org/licenses/fdl-1.3.html#license-text)提供。

[^1]: 比如说，`www.pixiv.net`和`pixiv.net`不一样，`z-library.se`和`zh.z-library.se`不一样。

