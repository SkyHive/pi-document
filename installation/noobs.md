# NOOBS

**新的开箱即用的软件 (NOOBS)** 一个简单的树莓派操作系统安装管理器。

![NOOBS OS selection](images/noobs.png)

## 如何获取NOOBS

### 购买一个预装NOOBS的SD卡

可以从许多的经销商和独立的零售商买到预装NOOBD的SD卡，包括[Pimoroni](https://shop.pimoroni.com/products/noobs-8gb-sd-card), [Adafruit](https://www.adafruit.com/products/1583), and [Pi Hut](http://thepihut.com/collections/raspberry-pi-sd-cards-and-adapters/products/noobs-preinstalled-sd-card)。

### 下载

此外，NOOBS可以在树莓派官网下载：[raspberrypi.org/downloads](https://www.raspberrypi.org/downloads/)

#### 怎样把NOODS安装到SD卡中

下载好NOOBS的zip包，你需要把它拷贝到一张格式化后的SD卡。

空白SD卡安装NOOBS步骤:

- 格式化一张至少4G的SD卡为FAT格式。参见下面的说明。
- 下载并解压NOOBS的zip包。
- 拷贝文件到你刚格式化的SD卡。注意：某些情况下会拷贝进一个文件夹，请把文件夹里面的所有文件移动到SD卡的根路径。
- 初次启动FAT分区会自动调整为最小大小，并启动一个OS选择界面。

#### 如何格式化SD卡为FAT格式

**注意:**  如果你格式化的SD（或 micro SD）卡容量超过了 32GB（例如：64GB）请参考 [SDXC formatting](sdxc_formatting.md) 说明.

##### Windows系统

对于Windows用户，我们推荐使用SD Association提供的SD卡格式化工具, 可以从这里下载[sdcard.org](https://www.sdcard.org/downloads/formatter_4/). 你需要在"Options" 菜单中设置"FORMAT SIZE ADJUSTMENT" 为 "ON"， 保证格式化整个SD卡，而不是某个分区。

##### Mac OS系统

对于Mac用户来说 [SD Association格式化工具](https://www.sdcard.org/downloads/formatter_4/)也是可用的 , 同时Mac OS X 自带的 Disk Utility 也能格式化整个SD卡，选择SD卡的盘符，点击Erase并选择MS-DOS格式。

##### Linux系统

Linux用户推荐使用 `gparted` (或者 `parted`命令). Norman Dunbar 为Linux用户写了一个 [使用教程](http://qdosmsq.dunbar-it.co.uk/blog/2013/06/noobs-for-raspberry-pi/) 。

##  NOOBS中包含的操作系统

以下操作系统都包含在NOOBS中:

- [Raspbian](http://raspbian.org/)
- [Pidora](http://pidora.ca/)
- [LibreELEC](https://libreelec.tv/)
- [OSMC](https://osmc.tv/)
- [RISC OS](https://www.riscosopen.org/wiki/documentation/show/Welcome%20to%20RISC%20OS%20Pi)
- [Arch Linux](http://archlinuxarm.org/platforms/armv6/raspberry-pi)

在NOOBS v1.3.10 (2014年9月)中只包含有 Raspbian。 其他系统可以通过网络下载。

## NOOBS 和 NOOBS Lite

NOOBS有两种形式安装: 离线或在线安装, 仅在线安装.

完整版版包含了Raspbian镜像，你可以离线安装到SD卡。NOOBS Lite 安装操作系统需要在线下载。

注意：完整版本中包含的系统镜像可能不是最新的，但是如果你连上网，NOOBS会检查更新并提供一个在线下载新版本的选项。

## NOOBS 开发

### 最新 NOOBS 版本

最新 NOOBS版本 **v1.9.2**, 发布于**2016年5月31号**.

(在 NOOBS v1.4.0 版本之前, NOOBS Lite 只有两位版本数据, 比如. v1.4)

### NOOBS 文档

更综合的文档, 包括一些高级的NOOBS配置方法, 可以在[GitHub](https://github.com/raspberrypi/noobs/blob/master/README.md)上查看.

### NOOBS 源码

 NOOBS 源代码在[GitHub](https://github.com/raspberrypi/noobs).
