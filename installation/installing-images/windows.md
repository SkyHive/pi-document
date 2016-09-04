# 使用Windows安装树莓派系统

- 把SD卡插入读卡器并检查分配的盘符。你可以很容易的在Windows资源管理器的左列找到盘符（例如：`G:`）。您可以使用SD卡插槽（如果有）或廉价的USB SD卡适配器。
- 从[Sourceforge Project page](http://sourceforge.net/projects/win32diskimager/) 下载Win32DiskImager zip文件; 你可以从USB设备运行。
- 解压zip包，在 `Win32DiskImager` 上右键，点击 **Run as administrator** 已管理员身份启动 Win32DiskImager。
- 选择你解压好的树莓派镜像。
- 在磁盘列表中选择SD卡的盘符。请选择正确的盘符，否则你将丢失硬盘上的数据！如果 Win32DiskImager 中未找到SD卡，并且你使用了电脑的SD插槽，请尝试使用SD卡适配器。
- 点击`Write`按钮，等待写卡完毕。
- 退出程序，并卸载SD卡。

---

*这篇文章使用了eLinux wiki page [RPi_Easy_SD_Card_Setup](http://elinux.org/RPi_Easy_SD_Card_Setup)内容, 基于[Creative Commons Attribution-ShareAlike 3.0 Unported license](http://creativecommons.org/licenses/by-sa/3.0/)共享*
