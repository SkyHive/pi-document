# 为NOOBS格式化SDXC卡

根据[SD specifications](https://www.sdcard.org/developers/overview/capacity/), 中的描述，任何大于32G容量的SD卡都叫SDXC，它们必须格式化为exFAT文件系统。这意味着官方的SD卡格式化工具总是使用exFAT来格式化大于等于64GB的卡。

树莓派的bootloader（在GPU中，并且不能更改）仅支持读取FAT（FAT16 与 FAT32）文件系统，所以不能从exFAT启动。如果你准备使用一张大于等于64GB的卡来安装NOOBS，那么你需要先把SDXC卡格式化为FAT32，然后再拷贝NOOBS。

## Linux 和 Mac OS

系统自带的标准格式化工具支持创建FAT32分区（可能会显示为 FAT 或 MS-DOS）。在执行 [NOOBS instructions](noobs.md)的剩余步骤前，请先删除SDXC卡上已存在的exFAT分区，然后创建一个新的FAT32主分区。

## Windows

Windows内建的标准格式化工具只运行最大32GB的FAT32分区。为了格式化64GB大小的FAT32分区，你需要使用第三方格式化工具。 [FAT32 Format](http://www.ridgecrop.demon.co.uk/guiformat.htm) 是一个简单的格式化工具，下载之后得到一个单文件`guiformat.exe`，无需安装即可使用。

首先启动[SD Formatter](https://www.sdcard.org/downloads/formatter_4/) 设置"FORMAT SIZE ADJUSTMENT" 为 "ON" 来删除SD卡上的所有分区。然后运行 guiformat.exe，选择正确的驱动盘符，其它选项保持默认即可，点击 Start 开始格式化。等待格式化完成，之后你可以继续[NOOBS instructions](noobs.md)的剩余步骤。

如何 guiformat.exe 不能正确完成工作，你还可以选择 [MiniTool Partition Wizard Free Edition](http://www.minitool.com/partition-manager/partition-wizard-home.html) 和 [EaseUS Partition Master Free](http://www.easeus.com/partition-manager/epm-free.html)，它们是专业的全功能分区软件，意味着上手难度比较高。
