# 在Linux上安装树莓派系统镜像

请注意 `dd` 工具将会覆盖你机器上的所有分区。 如果你在下面的命令中输入了错误的设备号，你可能删除你的Linux主分区。 请务必小心。

- 运行 `df -h` 查看当前有哪些设备挂载了。

- 如果你的电脑有SD卡卡槽, 插入SD卡。 如果没有，把SD卡插入到SD卡读卡器，再讲读卡器连接到电脑。

- 再次运行 `df -h` 命令. 新出现的设备就是你的SD卡. 左边一列显示SD卡的设备名; 类似于 `/dev/mmcblk0p1` 或者 `/dev/sdd1`. 设备的最后一部分 (`p1` 或者 `1` ) 是分区号, 不过我们要写入的是整个SD卡，而不是一个分区. 你需要删除设备名的最后那部分，比如 `/dev/mmcblk0` or `/dev/sdd` 将SD卡作为一个整体。 注意，同一张SD卡可能在 `df` 显示多次; 一张已经写入了树莓派镜像的SD卡也是这样，因为镜像将SD卡分成了多个分区。

- 现在你已经知道了SD卡的设备名，你需要先卸载SD卡保证写入镜像期间，SD卡不可以读写。

- 运行 `umount /dev/sdd1`命令, 用你的SD卡设备名替换 `sdd1` (包括分区编号).

- 如果你的SD卡由于有多个分区显示了不止一次 `df` , 你需要卸载所有的分区。

- 在终端使用以下命令向SD卡写入镜像，请确保你已经用你自己的`.img`文件名替换 `if=`参数, 以及你自己的SD卡设备号`/dev/sdd` 替换`of=` 参数. 务必使用正确的设备号，否则你将失去磁盘上所有的数据. 确保SD卡是整个设备名而不是其中一个分区; 比如说, `sdd`, 而不是 `sdds1` 或者 `sddp1`、 `mmcblk0`, 以及 `mmcblk0p1`.

    ```bash
    dd bs=4M if=2016-05-27-raspbian-jessie.img of=/dev/sdd
    ```

- 请注意，大部分情况下`4M`的块的大小都能正常工作 ; 如果不行的话，请使用`1M`, 这将会花费更长的时间.

- 同时注意，如果你不是使用的root账号登录的话，你需要在命令前面加上`sudo`.

- `dd`命令在运行的时候不会显示进度，所有有可能会冻结 ; 大概需要超过五分钟的时间将镜像写入到SD卡. 如果你的SD卡读卡器有LED指示灯的话，在写入的进程中会不断闪烁. 为了查看复制的进度 可以使用 `pkill -USR1 -n -x dd` 命令在另一个终端,如果不是root账号登录的，需要前面在`sudo` . 进度显示在原来的复制窗口，而不是运行`pkill` 命令的窗口; 由于缓存可能有延迟.

- 使用`dcfldd`代替`dd`; 将会显示写入的进度。

- 你可以使用`dd`把SD卡上的数据回写到硬盘上的一个镜像文件，然后使用`diff`或`md5sum`与原镜像进行比对。

- SD卡镜像可能比原始镜像大, 因为 `dd` 拷贝整个内存卡. 我们必须裁剪导出的镜像让它和原始镜像一样大。确保`if=`的参数替换为正确的设备号。`diff`命令将报告两个镜像是一致的。

    ```bash
    dd bs=4M if=/dev/sdd of=from-sd-card.img
    truncate --reference 2016-05-27-raspbian-jessie.img from-sd-card.img
    diff -s from-sd-card.img 2016-05-27-raspbian-jessie.img
    ```

- 运行 `sync`命令; 确保缓存数据都写入到了硬盘，之后可以安装卸载SD卡.

- 从读卡器取出SD卡.

---

*这篇文章使用了 eLinux wiki 页面 [RPi_Easy_SD_Card_Setup](http://elinux.org/RPi_Easy_SD_Card_Setup), 基于[Creative Commons Attribution-ShareAlike 3.0 Unported license](http://creativecommons.org/licenses/by-sa/3.0/)*
