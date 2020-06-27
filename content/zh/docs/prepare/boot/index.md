---
linkTitle: "安装系统"
title: "安装系统"
weight: 2
description: "为树莓派安装操作系统。"
---

因为我们没有准备 HDMI 连接线、显示器和外接键盘，因此无法使用有线方式登录树莓派的操作系统。因此我们将配置树莓派系统中的 WiFi 连接信息，让其在开机后自动接入家庭的 WiFi，然后通过路由器的后台页面获得树莓派的 IP 地址，再使用 SSH 登录树莓派。

## 准备的软件

在安装的操作系统前需要准备的有：

- [Raspberry Pi Imager](https://www.raspberrypi.org/downloads/)
- [Raspberry Pi OS (32-bit) with desktop and recommended software](https://www.raspberrypi.org/downloads/raspberry-pi-os/)

访问 <https://www.raspberrypi.org/downloads/> 下载 Raspberry Pi Imager 用于向存储卡写入操作系统。

手动下载树莓派 OS（32 位），该系统对硬件的兼容性最好，且支持的软件也更多，不推荐使用 Ubuntu 64 位系统。

系统下载完成后再使用 Raspberry Pi Imager 将系统写入存储卡。

## 配置 WiFi

在 boot 磁盘的根目录创建一个 `wpa_supplicant.conf` 文件，内容如下。

```ini
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=<Insert country code here>

network={
 ssid="<Name of your WiFi>"
 psk="<Password for your WiFi>"
}
```

其中：

-  `country` 为[国家代码](https://www.iso.org/obp/ui/)，中国大陆为 `CN`；
-  `ssid` 为 WiFi 名称；
-  `psk` 为 WiFi 密码；

## 开启 SSH

只需要在 boot 磁盘的根目录创建一个名为 `ssh` 的文件即可。

## 默认的账号密码

以下为树莓派操作系统默认的用户名和密码。

- 默认用户名：`pi`
- 默认密码：`raspberry`

## 获取树莓派的 IP 地址

查看家庭使用的路由器背面的连接信息，如果使用的是 TPLink 可以通过 <http://tplogin.cn> 登录路由器管理后台。

登录到后台后选择「设备管理」里面可以看到一个名为 `raspberrypi` 的设备，查看该设备的详细信息可以看到它的 IP 地址。

## 登录树莓派

当你的电脑跟树莓派连接的是同一个家庭 WiFi 的时候，可以使用下面的命令登录树莓派。

```bash
ssh pi@<树莓派的 IP 地址>
```

密码为 `raspberry`。