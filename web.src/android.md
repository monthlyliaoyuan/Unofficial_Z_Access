# 安卓使用指南

***本指南极其复杂，在决定踏上这条路前请三思！***

本教程测试于MIUI14（国内版）。

**遇到类似不安全或病毒报警，请自行判断是否继续。**

为了省流，我不打算配图片

## 第一部分：准备文件

### 两个安装包

（`.apk`），提供的是两个链接，不保证可以下载。

+ [Termux](https://www.downkuai.com/android/140917.html)（知道F-droid的，推荐从Fdroid下载；如果你用电脑进行ADB，则不需要）
+ [AndroidGoogleChrome](https://www.onlinedown.net/soft/10107048.htm)（建议用链接里的版本，切记不要`安全下载`！否则后果自负）

### 一句命令

先关闭本软件，再点开本软件安装包同级目录下的`GetAndroidADBCommandLine.bat`，本软件会重新打开，然后复制上面的第一行内容（以`_`开头）

你会得到类似这样的东西：

```text
echo "_ --host-resolver-rules=\"MAP bu2021.xyz 172.64.145.17:443,MAP annas-archive.se 172.64.145.17:443\" -origin-to-force-quic-on=bu2021.xyz:443,annas-archive.se:443 --host-rules=\"MAP libgen.rs 193.218.118.42,MAP zh.singlelogin.re 176.123.7.105,MAP singlelogin.re 176.123.7.105\" --ignore-certificate-errors" > chrome-command-line
```

## 第二部分：开启ADB

这里提供一个MIUI下利用Termux作为终端的例子。

### 安装Termux并作准备

进入Termux后，是一个命令行界面。

你可以考虑换清华源，见[镜像站官方帮助文档](https://mirrors.tuna.tsinghua.edu.cn/help/termux/)

依次执行以下命令：（如果遇到提问，直接`Enter`走默认）

```bash
apt update
apt upgrade
pkg install android-tools
```

### 连接ADB

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

### 设置command-line

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
echo "$ (<chrome-command-line)
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

## 第三部分：打开ChromeFlag

还记得Chrome吗（必须要Chrome，其他浏览器一律不行）。

进入，一路瞎点。

地址栏输入

```text
chrome://flags/
```

搜索`Command`，找到`Enable command line on non-rooted devices`，设置为`Enabled`。

退出Chrome，**重启手机**。

## 第四部分：确认设置成功

重新打开Chrome。

地址栏输入

```text
chrome://version/
```

确认命令行栏有`_`打头。

## 第五部分：愉快上网

使用Chrome浏览器，键入`https://zh.singlelogin.re`

## The end.

如果出现问题，可以Github开Issue。

返回[首页](./index.html)
