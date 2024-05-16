# 命令行参数帮助

鉴于本应用名字较长，我强烈建议您把他的名字改短一点，比如`zlib.exe`。

默认接下来您已经进行了重命名。

## `-h`

打开帮助，也就是显示此文件。

## `-g url`

打开后跳转到url，而不是默认开始页。
注意：`url`必须带协议头，如：`https://1919810.com`。

## `-c [FILE]`

使用命令行配置文件。

如果有`[FILE]`，程序读取`FILE`，否则程序会尝试读取同一目录下的`CMDconfig.txt`。

该文件应当有两行。

1. `--host-resolver-rules`
2. `-origin-to-force-quic-on`

下面是一个可行的配置，用于访问`zh.z-library.se'`与`bu2021.xyz`。

```text
MAP zh.z-library.se [2606:4700:3033::ac43:aa46]:443,MAP bu2021.xyz [2606:4700:3033::6815:3e2]:443
zh.z-library.se:443,bu2021.xyz:443
```

## `-d`

根据域名进行配置，要求IP支持QUIC，且能访问（一般指ping得通）（**必须支持QUIC**）。

如果有`[FILE]`，程序读取`FILE`，否则程序会尝试读取同一目录下的`DOMAINconfig.txt`。

我们通过空行来分割多个IP的配置，每份配置的第一行是该IP（支持IPv6），接下来若干行是你的域名（不包含协议头，如`https://`）。**注意，该方法对域名极其敏感，子域名是不一样的域名。如`www.pixiv.net`和`pixiv.net`不一样，`z-library.se`和`zh.z-library.se`不一样，*请注意。***

洁净域名IP查询：[Whois365](https://www.whois365.com/)（非广告）

以CloudFlare为例你可以到[这里](https://www.cloudflare-cn.com/ips/)寻找一个CloudFlareCDN的IP。并请确保ping得通。（一般可以）

接下来任意多行是需要启用工具的域名，尽量不要太多，Windows命令行的长度是有限制的。（好像是$8192$个字符）

以下是一个可行的配置：（这两个IP分别是CloudFlare的IPv4与IPv6之一，为了演示分开）。

```plaintext
[2606:4700:3033::ac43:aa46]
zh.z-library.se
bu2021.xyz
annas-archive.se
longlivemarxleninmaoism.online
zlib-articles.se
zh.zlib-articles.se

172.64.145.17
www.pixiv.net
```

## `-o`

页面将显示打开此次程序的浏览器命令行参数。

# 域名添加指南

如果你发现了有一个域名无法连接，就可以加到配置列表里。

**注意子域名也要。**

如果还不行，那就是不行，子域名不支持QUIC。

如果出现HTTP协议，或者非标准端口，请采用`CMDconfig`

或者自己编写命令行。请参考：Chromium NewWork Configs Codes：

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

有问题请加Github issue。

---

返回[首页](./index.html)
