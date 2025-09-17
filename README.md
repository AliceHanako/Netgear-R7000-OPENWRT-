# Netgear R6900 R7000 Openwrt自用固件<br>
带Zerotier 1.16.0，argon主题。<br>
<br>
先用openwrt官方的chk文件配合nmrpflash刷入。<br>
https://github.com/jclehner/nmrpflash<br>
<br>
https://openwrt.org/toh/netgear/r7000<br>
<br>
Factory image:<br>
https://downloads.openwrt.org/releases/24.10.2/targets/bcm53xx/generic/openwrt-24.10.2-bcm53xx-generic-netgear_r7000-squashfs.chk<br>
<br>
再从系统——备份与升级——刷写新的固件<br>
（需要勾选不保留配置）<br>
<br>

# 过程经验：
- 新建一个文件夹，比如flash_openwrt
- 下载nmrpflash后，把该刷机程序放在flash_openwrtwen文件夹内
- [nmrpflash需要npcap驱动，在这里下载 (https://npcap.com/#download)选择installer版本，并勾选WinPcap。我用的Npcap 1.83 installer版本]
- 在该文件夹以管理员打开CMD
- 先用nmrpflash -L 确定网卡（网线接在LAN1口）
- 如果正常的情况下会出现net28  192.168.31.20    10:7c:xx:xx:xx:xx  () 之类的信息
- 我的网卡名是net28，这个端口后续命令要用
- 把官方给的工厂镜像放进去，例子：openwrt-24.10.2-bcm53xx-generic-netgear_r7000-squashfs.chk
- 然后输入命令：
- nmrpflash.exe -i net28 -f openwrt-24.10.2-bcm53xx-generic-netgear_r7000-squashfs.chk -vvv
- [-i 后面输入的是网卡名字，比如刚刚获取的net28]
- [-f 后面输入的是需要输入镜像的名字]
- [-vvv 刷入镜像时输出详细日志信息]
- 在网线没接入的情况下显示是 Waiting for Ethernet connection (Ctrl-C to skip).
- 在网线接入的情况下下显示是 Adding xxx.xxx.xxx.xxx to interface net28.
                            Advertising NMRP server on net26 ... /
- 这个时候可以把路由器接上电源，他就会开始刷入镜像了（需要在60秒内进行连接的操作，否则会取消刷入程序）

- 当出现.................
- << DATA(14588)
- >> ACK(14588)
- << DATA(14589)
- >> ACK(14589)
- << DATA(14590)
- >> ACK(14590)
- << DATA(14591)
- >> ACK(14591)
- << DATA(14592)
- >> ACK(14592)
- << DATA(14593)
- >> ACK(14593)
-  OK (7471162 b)
- Waiting for remote to respond.
- Received keep-alive request (7).
- Remote finished. Closing connection.
- Reboot your device now.

- 时候，就可以断开电源，等5秒后，再重新接上电源。
- 这时候等待路由器开机，没有意外的情况下，打开192.168.1.1，就能看到openwrt的luci登录界面了。

- 后续可以下载上面的chk固件，在“系统——备份与升级——刷写新的固件”上刷入，记得不保留任何配置，等待3-5分钟后，路由器自动重启后即可使用。
