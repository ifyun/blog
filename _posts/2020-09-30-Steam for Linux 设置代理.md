---
title: Steam for Linux 设置代理
date: 2020-09-30 16:00 +0800
categories: [Linux, Steam]
tags: [Linux, Steam]

---

## 用正确的姿势给 Steam for Linux 设置代理

## 为什么会有此文档？

在使用 Linux Mint 时，发现 Steam 客户端打不开社区，但是 Chrome 可以打开，于是去找 Steam 客服，
得到的回复是让我使用 Ubuntu，行吧，反正我正好有换 Ubuntu 的打算（Mint 的字体渲染不清晰）。

然而，Ubuntu 的 Steam 客户端依然打不开社区，客服说让去 GitHub 讨论，然后我分析了一下，破案了：

- 国内是无法访问 Steam 社区的，需要挂梯子（我确实挂了）
- Steam for Windows 默认使用 IE 的代理，因此，挂梯子有效
- **Steam for Linux 不能使用代理，也无法通过客户端设置**

## 解决方案（1）

既然 Steam 不能设置代理，那就用第三方的工具让它走代理咯～

### 1. 安装 proxychains

```
sudo apt-get install proxychains
```

编辑 `proxychains` 的配置文件（在 `/etc/proxychains.conf`），以下是示例：

```
socks5 	    127.0.0.1 7891
http		127.0.0.1 7890
```

我用的是 Clash，所以端口是 7890 和 7891，根据自己使用的代理软件来设置即可。

### 2. 修改 Steam 的桌面入口文件

文件的位置是：`/usr/share/applications/steam.desktop`

找到 `Exec` 部分，改为：

```
Exec=/usr/bin/proxychains /usr/games/steam %U
```

现在点击 Steam 图标启动就可以愉快地打开所有页面了。

> 注意：此方法会导致部分游戏打不开，建议单独使用浏览器去使用社区和创意工坊！

## 解决方案（2）

1. 把代理挂载路由器上，选择支持华硕固件、老毛子固件的路由器，有钱直接上 AC86U
2. 虚拟机跑软路由挂代理
3. Windows 它不香吗？