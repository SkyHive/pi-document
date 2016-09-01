
# 设置

设置树莓派指南

## 需要的设备

### 必选 (对大部分用户)

- [SD卡](../installation/sd-cards.md)
    - 推荐 8GB class 4 SD卡 - 可以理想预装 [NOOBS](../installation/noobs.md).
- [显示器与接口](monitor-connection.md)
    - 任何HDMI/DVI显示器以及TV都可以作为树莓派的显示设备. 为了显示最好的效果，建议使用HDMI输入, 对于旧的设备其他的方式也是可以的.
- 键盘鼠标
    - 任何带有标准USB接口的鼠标和键盘都能在树莓派上很好地工作
    - 无线键盘鼠标配对后也能使用
    - 键盘布局配置参考 [raspi-config](../configuration/raspi-config.md).
- [电源](../hardware/raspberrypi/power/README.md)
    - 树莓派使用Micro USB接口供电(跟大多数标准手机接口一样).
    - 你需要提供至少2A-5V高质量的电源给Model 3B供电, 或者700mA-5V给早期的产品.
    - 低电流(~700mA)只能满足基本使用，突发更高的供电需求可能将导致树莓派重启。

### 可选

- 网线 [仅限Model B/B+]
    - 网线可以使树莓派连接到局域网和互联网。
- [无线网卡](../configuration/wireless/README.md)
    - 此外，你可以通过配置无线网卡来连接到网络。
- 音频
    - 音频可以通过标准的3.5mm插孔传输到扬声器或耳机播放。
    - 没有HDMI电缆，播放声音需要音频导线。
    - 如果使用HDMI线，那么就不需要音频线了，因为HDMI能同时传输音频和视频；当然你也可以同时插入音频导线以便向另一个扬声器输出音频，但这需要[配置](../configuration/audio-config.md).

## 故障排除

设置过程中的任何问题, 可以通过搜索 [the forums](https://www.raspberrypi.org/forums/) 找到解决办法. 如果没有找到，请提交你的问题，并尽可能提供细节.
