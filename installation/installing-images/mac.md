# 在Mac 电脑上安装树莓派镜像

在Mac系统上你可以选择`dd`命令行工具或者图形化工具ImageWriter将镜像写入到SD卡

## （大多数）图形化工具

- 使用外接读卡器连接到电脑，注意内存卡必须是FAT32的格式
- 从苹果的开始菜单，选择"About This Mac", 点击 "More info..."; 如果你使用 Mac OS X 10.8.x 或者更新的版本, 点击 "System Report".
- 点击 "USB" (如果是内置的读卡器选择 "Card Reader" ) 从右上角找到你的SD卡窗口. 单击, 然后在下面选项中找到 BSD名字 ; 比如 `diskn` ， `n` 是个整数 (比如： `disk4`). 确保你注意到了数字。
- 为了能够写入硬盘，先要卸载分区. 开打硬盘工具，卸载; 别拔下来否则你将要重新连接. 注意Mac OS X 10.8.x 版本, "Verify Disk" (在卸载之前) 将会显示 BSD 名字 比如 `/dev/disk1s1` 或者 类似的, 允许你跳过前两步.
- 从命令行终端运行以下命令:

    ```
    sudo dd bs=1m if=path_of_your_image.img of=/dev/rdiskn
    ```

    记得将 `n`替换为你的盘符!

   - 如果命令失败，使用 `disk` 替换 `rdisk`:
    
       ```
       sudo dd bs=1m if=path_of_your_image.img of=/dev/diskn
       ```

## 命令行

- 如果你熟练命令行，你将可以不需要其他软件直接将镜像写入到SD卡. 打开一个终端，输入:

    `diskutil list`

- 确认你的SD卡盘符（不是分区） 比如 `disk4`, 而不是 `disk4s1`.
- 通过SD卡盘符卸载SD卡，准备将数据复制到SD卡中:

    `diskutil unmountDisk /dev/disk<disk# from diskutil>`

     `disk` 是你的 BSD 名字 比如 `diskutil unmountDisk /dev/disk4`
    
- 将数据复制到SD卡:

    `sudo dd bs=1m if=image.img of=/dev/rdisk<disk# from diskutil>`

     `disk`是你的 BSD 名字 例如：`sudo dd bs=1m if=2016-05-27-raspbian-jessie.img of=/dev/rdisk4`

    - 如果你安装了GNU coreutils，可能会出现一个错误：``dd: invalid number '1m'`` 那种情况下，新需要将  `bs=` 选项改为`1M` , 如下:

       `sudo dd bs=1M if=image.img of=/dev/rdisk<disk# from diskutil>`

    这将要花费几分钟的时间，根据镜像文件的大小而定. 你可以通过发送 `SIGINFO` 信号 (按 `Ctrl+T`)检查程序的执行.
    
    - 如果这个命令依然失败, 试着使用`disk` 代替`rdisk`, 比如:
    
       ```
       sudo dd bs=1m if=2016-05-27-raspbian-jessie.img of=/dev/disk4
       ```
       或者
       ```
       sudo dd bs=1M if=2016-05-27-raspbian-jessie.img of=/dev/disk4
       ```

## 替代方案

**注意: 部分用户使用这个方法报告了问题**

以下命令需要管理员权限运行

- 从终端运行 `df -h`.
- 连接到插入SD卡的读取器
- 再次运行 `df -h` 查看新出现的设备。 记录下设备的文件系统分区名，比如 `/dev/disk3s1`.
- 卸载分区以便可以覆盖分区:

    ```
    sudo diskutil unmount /dev/disk3s1
    ```

    或者打开`Disk Utility`工具，`unmount`SD卡（不是 `eject`,否则你需要重新拔插SD卡）
- 从分区名称中分离出设备名：去掉末尾的s1，并用"rdisk"替换"disk"。这非常重要，如果你提供了错误的设备名，你将丢失硬盘上的所有数据。确保设备名描述整个SD卡，而不是其中的一个分区（例如：rdisk3，而不是rdisk3s1）。相似地，你的另一张SD卡设备名可能是rdisk2 或 rdisk4；在插入SD之前以及插入之后使用df -h命令，找出新增加的设备，分离出设备名。例如：/dev/disk3s1变为/dev/rdisk3。
- 在控制台使用下面的命令来向SD卡写入镜像，记住使用刚才获取的设备名。请咨询检查上面的步骤以确保设备名正确。
    
    ```
    sudo dd bs=1m if=2016-05-27-raspbian-jessie.img of=/dev/rdisk3
    ```

    如果命令出现错误：dd: bs: illegal numeric value，请用bs=1M替换bs=1m。

    如果命令出现错误：dd: /dev/rdisk3: Permission denied,表明SD卡上的分区被MacOS保护，你需要使用下面的命令来抹掉分区：
    
    ```
    sudo diskutil partitionDisk /dev/disk3 1 MBR "Free Space" "%noformat%" 100%
    ```
    
    这个命令同时为设备添加了可写权限。现在你可以使用dd命令了。

    注意：dd不会有任何的反馈，除非遇到错误或写入完成；一旦完成，dd会显示信息而SD卡将被重新加载。当然你也可以使用ctrl-T来查看进度；它发送SIGINFO信号到tty，然后进度信息将显示出来。
- 当dd执行完成，推出SD卡：

    ```
    sudo diskutil eject /dev/rdisk3
    ```

    或者打开 Disk Utilit 来推出 SD卡

---

*这篇文章使用了 eLinux wiki 页面 [RPi_Easy_SD_Card_Setup](http://elinux.org/RPi_Easy_SD_Card_Setup), 基于[Creative Commons Attribution-ShareAlike 3.0 Unported license](http://creativecommons.org/licenses/by-sa/3.0/)共享*
