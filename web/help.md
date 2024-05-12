# 命令行参数帮助

鉴于本应用名字较长，我强烈建议您把他的名字改短一点，比如`zlib.exe`。

默认接下来您已经进行了重命名。

## `-h`

打开帮助，也就是显示此文件。

## `-g url`

打开后跳转到url，而不是默认开始页。
注意：`url`必须带协议头，如：`https://1919810.com`。

## `-c`

使用命令行配置文件。

程序会尝试读取同一目录下的`CMDconfig.txt`。

该文件应当有两行。

1. `--host-resolver-rules`
2. `-origin-to-force-quic-on`

下面是一个可行的配置，用于访问'zh.z-library.se'于`bu2021.xyz`。

```text
MAP zh.z-library.se [2606:4700:3033::ac43:aa46]:443,MAP bu2021.xyz [2606:4700:3033::6815:3e2]:443
zh.z-library.se:443,bu2021.xyz:443
```

## `-d`

根据域名进行配置，只支持挂靠`CloudFlare CDN`的网站且使用CF默认配置（**必须支持QUIC**）。

程序会尝试读取同一目录下的`DOMAINconfig.txt`。

该文件的第一行是您当地可以访问的CloudFlareIP。

接下来任意多行是需要启用工具的域名，尽量不要太多，多了我不知道会出什么鬼问题。

以下是一个可行的配置：

```plaintext
[2606:4700:3033::ac43:aa46]
zh.z-library.se
bu2021.xyz
annas-archive.se
```

## 返回[首页](./index.html)
