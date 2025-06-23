---
title: "如何逃离Unity中国特供版 – 朝露碎梦"
source: "https://aibofan.com/how-to-escape-from-the-unity-china-special-edition/"
description: "Unity中国做过的恶心事各位开发者肯定有所耳闻或者正深受其害。在和中国特供版的Unity Hub以及Unit…"
date: 2025-03-31
draft: "false"
tags:
---
Unity中国做过的恶心事各位开发者肯定有所耳闻或者正深受其害。在和中国特供版的Unity Hub以及Unity斗智斗勇中研究了一天后，本人终于成功逃离了中国特供版的魔爪，现记录一下。

### 挂代理

代理是下面所有操作的前提，即使你通过其他渠道成功下载到了国际版的UnityHub安装程序，后续如果没有代理的话，账号登陆也只能走中国区。

如果你用的VPN，可以安心继续下面的步骤。

如果你使用的是SS/V2/小猫咪这些，只是修改浏览器的HTTP/HTTPS代理，那么需要做两件事：

1. 将unity.com和unity3d.com后缀的网址加入代理列表
2. 在安装完UnityHub后新建一个启动脚本

Windows为

```
@echo off
set HTTP_PROXY=http://127.0.0.1:1080
set HTTPS_PROXY=http://127.0.0.1:1080
start "" "C:\Program Files\Unity Hub\Unity Hub.exe"
```

Mac则是在终端中运行下面脚本，然后把生成的launchUnityHub.command挪到一个方便的位置（比如桌面）

```
echo '#!/bin/bash
export HTTP_PROXY=http://127.0.0.1:1080
export HTTPS_PROXY=http://127.0.0.1:1080
nohup "/Applications/Unity Hub.app/Contents/MacOS/Unity Hub" &>/dev/null &' > launchUnityHub.command
chmod +x launchUnityHub.command
```

其中的127.0.0.1:1080就是你的浏览器代理地址，根据实际情况做改动。

### 下载国际版UnityHub

如果代理设置完成，直接访问 [下载地址(Win)](https://public-cdn.cloud.unity3d.com/hub/nuo/UnityHubSetup.exe) / [下载地址(Mac)](https://public-cdn.cloud.unity3d.com/hub/prod/UnityHubSetup.dmg) 下载UnityHub，并安装。

[Unity Hub 3.1.1阿里云盘备份](https://www.aliyundrive.com/s/7LJyi8qJ6qF)

如果有已安装的UnityHub版本，先卸载，为以防万一，卸载之后删除

~/AppData/Roaming

这个目录下的UnityHub和Unity Hub目录。然后再安装。

### 通过上面的脚本启动UnityHub

一定要使用上面的脚本启动！否则UnityHub启动时不会读取系统代理，在登陆时会跳转到https://id.unity.cn/。

![](https://aibofan.com/how-to-escape-from-the-unity-china-special-edition/)

上图就是直接运行UnityHub后登陆时的界面，跳转的地址是https://id.unity.cn/

![](https://aibofan.com/how-to-escape-from-the-unity-china-special-edition/)

这个图是通过脚本启动UnityHub后的登陆页面，跳转的地址是https://id.unity.com/，Sign in with google终于能用了。

### 安装Unity Editor

接下来安装Unity Editor，有下面几种方式

#### 直接通过UnityHub安装

既然代理都设置好了，直接下载，也不用担心下载到特供版啦。

#### 通过唤起链接安装

可以直接参考 [知乎大佬的帖子](https://zhuanlan.zhihu.com/p/106132063)

#### 通过官方的Unity Editor Download Assistant下载

官方有安装辅助工具，可以在不安装UnityHub的情况下直接安装Unity Editor，之后再到Unity Hub中添加即可。

[链接可以在这里找到](https://unity3d.com/unity/qa/lts-releases) 。

### Done

Enjoy designing your game without the disgusting unity cn.

---

转载自： [如何逃离Unity中国特供版 – Logiconsole](https://www.logiconsole.com/fuck-unity-cn/)