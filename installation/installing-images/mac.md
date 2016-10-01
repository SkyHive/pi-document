# 在苹果操作系统上安装树莓派镜像

在苹果操作系统上你可以选择命令行工具 `dd` 或者图形化工具 ImageWriter 将镜像写入到SD卡。

## （大多数）图形界面

- 将带有SD卡的读卡器连接到电脑。注意内存卡必须格式化成FAT32的格式。(译注：[mac上将内存卡格式化成FAT32格式]())
- 从开始菜单，选择"关于本机", 然后点击"概览"; 如果你使用 Mac OS X 10.8.x 或者更新的版本, 点击 "系统报告..."。
- 点击"USB"（如果是内置的读卡器,选择 "读卡器"），然后从右上角选择窗口寻找到你的SD卡（译注：我用的是读卡器，从"存储"中找到的）。单击选中, 然后在右下选项中找到BSD名称 ; 看起来类似`diskn`的格式，`n`是个数字（比如：`disk4`）。请确保你注意到了数字。
- 先要卸载分区，你才被允许重新将数据写入SD卡。打开磁盘工具，卸载SD卡; 不是弹出，否则你将要重新连接。注意Mac OS X 10.8.x 版本, "磁盘工具" (在卸载之前) 将会显示BSD名称，类似于`/dev/disk1s1`, 你可以跳过前两步操作.
- 从命令行终端运行以下命令:

    ```
    sudo dd bs=1m if=path_of_your_image.img of=/dev/rdiskn
    ```

    记得将`n`替换为你之前记录的盘符!

   - 如果命令执行失败，使用`disk`替换`rdisk`:
    
       ```
       sudo dd bs=1m if=path_of_your_image.img of=/dev/diskn
       ```

## 命令行

- 如果你熟练命令行，你可以不需要任何其他软件直接将镜像写入到SD卡。打开一个终端，运行:

    `diskutil list`

- 确认你的SD卡盘符（不是分区）例如`disk4`, 而不是`disk4s1`。
- 通过SD卡盘符卸载SD卡，准备将数据复制到SD卡中:

    `diskutil unmountDisk /dev/disk<disk# from diskutil>`

    `disk`是你的BSD名称，例如：`diskutil unmountDisk /dev/disk4`
    
- 将数据复制到SD卡:

    `sudo dd bs=1m if=image.img of=/dev/rdisk<disk# from diskutil>`

    `disk`是你的BSD名称，例如：`sudo dd bs=1m if=2016-05-27-raspbian-jessie.img of=/dev/rdisk4`

    - 如果你安装了GNU coreutils，可能会出现一个错误：``dd: invalid number '1m'`` 此时，需要将`bs=`选项改为`1M`，例如:

       `sudo dd bs=1M if=image.img of=/dev/rdisk<disk# from diskutil>`

    这将要花费几分钟的时间，根据镜像文件的大小而定。你可以通过发送`SIGINFO`信号（按 `Ctrl+T`）检查程序的执行的进度。
    
    - 如果这个命令依然失败, 试着使用`disk`代替`rdisk`, 例如:
    
       ```
       sudo dd bs=1m if=2016-05-27-raspbian-jessie.img of=/dev/disk4
       ```
       或者
       ```
       sudo dd bs=1M if=2016-05-27-raspbian-jessie.img of=/dev/disk4
       ```

## 替代方法

**注意: 部分用户使用这个方法创建SD卡镜像时除了问题**

以下命令需要管理员权限运行。

- 在终端运行`df -h`。
- 连接到插入SD卡的读取器。
- 再次运行`df -h`，找到之前没有列举的新的设备。记录下设备的文件系统分区名称，例如`/dev/disk3s1`。
- 先要卸载分区，你才被允许重新将数据写入SD卡。:

    ```
    sudo diskutil unmount /dev/disk3s1
    ```

    或者打开`磁盘工具`，`卸载`SD卡，不是`弹出`，否则你需要重新连接SD卡。
- 从分区名称中分离出设备名：去掉末尾的s1，并用`rdisk`替换`disk`。这非常重要，如果你输入了错误的设备名，你将丢失硬盘上的所有数据。确保设备名称如上所说的描述整个SD卡，而不是其中的一个分区（例如：应该是`rdisk3`而不是`rdisk3s1`）。类似的，你的另一张SD卡设备名可能是`rdisk2`或`rdisk4`；在将SD读卡器插入电脑前后，再分别使用`df -h`命令检查。例如：`/dev/disk3s1`应该是`/dev/rdisk3`。
- 在控制台使用下面的命令来向SD卡写入镜像，使用刚才获取的设备名称。请仔细阅读上面的步骤，以确保你使用的是正确的设备名称。
    
    ```
    sudo dd bs=1m if=2016-05-27-raspbian-jessie.img of=/dev/rdisk3
    ```

    如果命令出现错误：`dd: bs: illegal numeric value`，请用`bs=1M`替换`bs=1m`。

    如果命令出现错误：`dd: /dev/rdisk3: Permission denied`，意味着SD卡上的分区表被Mac OS保护，禁止写入数据。你需要使用下面的命令来抹掉分区：
    
    ```
    sudo diskutil partitionDisk /dev/disk3 1 MBR "Free Space" "%noformat%" 100%
    ```
    
    这个命令同时为设备添加了写权限。现在你可以再次使用`dd`命令了。

    注意：`dd`命令不会有任何的反馈信息，除非遇到错误或写入完成；一旦完成，将会显示写入完成信息，SD卡也将被重新挂载。如果你想查看进度，你也可以使用`ctrl-T`，它发送SIGINFO，程序的进度信息和终端的状态参数将显示出来。

- 当`dd`执行完成，推出SD卡：

    ```
    sudo diskutil eject /dev/rdisk3
    ```

    或者打开磁盘工具来推出SD卡。

---

*这篇文章使用了 eLinux wiki 页面 [RPi_Easy_SD_Card_Setup](http://elinux.org/RPi_Easy_SD_Card_Setup)内容, 基于[Creative Commons Attribution-ShareAlike 3.0 Unported license](http://creativecommons.org/licenses/by-sa/3.0/)共享*
