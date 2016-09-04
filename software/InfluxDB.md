
# InfluxDB

时序数据库

1. 下载
    - 可以到官网下载最新版的[InfluxDB](https://influxdata.com/downloads/#influxdb),注意，请选择版本`Standalone Binaries (ARM)`。
    比如当前最新版为13.0，使用下面的命令下载：
    ```
    wget https://dl.influxdata.com/influxdb/releases/influxdb-0.13.0_linux_armhf.tar.gz
    ```
2. 安装
    - 解压下载的安装包：
    ```
    sudo tar xvfz influxdb-0.13.0_linux_armhf.tar.gz
    ```
    如果你想不依赖其他的软件，并且能够开机自启动，需要执行以下操作，当然，你也可以直接在解压好的目录下运行，使用`nohup`命令或者`supervisor`工具
    ```
    sudo cp -r influxdb-0.13.0-1/* /
    ```
    这条命令意思将解压好的文件目录下的文件复制到根目录，Influx默认是按照Linux目录结构存放的文件，注意解压的时候必须以sodu的权限解压，或者普通权限解压，然后使用
    ```
    sudo chown -R root:root influxdb-0.13.0-1
    ```
    递归将目录下的子文件全都更改为root权限
    ```
    sudo mkdir /usr/lib/systemd/system
    sudo cp  /usr/lib/influxdb/scripts/influxdb.service /usr/lib/systemd/system
    ```
    将系统服务的脚本放到`/usr/lib/systemd/system`目录下，然后将其中的`User`和`Group`都修改为`root`
    启动InfluxDB
    ```
    sudo systemctl start influxdb
    ```
    到此就安装完成了

3. 开机自启动
    ```
    sudo systemctl enable influxdb
    ```