# SD 卡

树莓派能与兼容的SD卡工作，但这里一些需要遵循的准则:

##SD 卡大小 (容量).

安装NOOBS最少需要8GB，其它镜像建议最小4GB；一些操作系统可以工作在更小的卡上，例如 OpenElec 和 Arch。

##SD 卡种类.

SD卡的class。class决定了SD卡的写入速度；class 4 写入速度可以达到 4MB/s，而 class 10 可以达到 10MB/s。但这并不意味着class 10在任何情况下都比 class 4优秀，因为写入速度的提升通常以牺牲读取速度和寻道时间为代价。

##SD 卡尺寸.

最初的 [Raspberry Pi Model A](https://www.raspberrypi.org/products/model-a/) 和 [Raspberry Pi Model B](https://www.raspberrypi.org/products/model-b/)需要全尺寸SD 卡. 新版的 [Raspberry Pi Model A+](https://www.raspberrypi.org/products/model-a-plus/), [Raspberry Pi Model B+](https://www.raspberrypi.org/products/model-b-plus/), [Raspberry Pi 2 Model B](https://www.raspberrypi.org/products/raspberry-pi-2-model-b/), [Raspberry Pi Zero](https://www.raspberrypi.org/products/pi-zero/), and [Raspberry Pi 3 Model B](https://www.raspberrypi.org/products/raspberry-pi-3-model-b/) 需要micro-SD卡.

##排除故障

我们建议购买[here](https://shop.pimoroni.com/products/noobs-8gb-sd-card), 它是一张8GB clas 6 的 microSD卡，并配备了一张全尺寸SD卡套，十分超值。

如果你在使用SD卡中遇到任何的数据损坏问题，确保你遵循了以下步骤：

1. 请确保您使用的是正品SD卡。有很多廉价的SD卡，容量比广告宣称的小，并且寿命有限。
2. 请确保你使用的是品质优良的电源。你可以检测树莓派上TP1和TP2之间的电压，如果高负荷情况下电压低于4.75V，那么这个电源是不合格的。
3. 确保你使用了优质的USB线缆来供电。当使用了优质电源后，TP1->TP2之间的电压依然低于 4.75V。这有可能是线缆的质量导致；为了节省成本USB线可能使用小铜芯，有可能1V的电源损失在线缆上。
4. 确保你在关闭电源之前已正确关闭树莓派。键入sudo halt来关机，一但关机完成LED等会闪烁，这时候你可以安全的关闭电源了。
5. 最后，超频可能导致数据损坏。这个问题之前已经修复，虽然采用的解决方法意味着它仍然有可能发生。如果遵循上述步骤后仍然数据损坏问题，请告诉我们。
