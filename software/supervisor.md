使用supervisor配置应用程序

http://supervisord.org/index.html

http://liyangliang.me/posts/2015/06/using-supervisor/

安装
```
sudo apt-get install supervisor
```
`supervisord`（supervisor 是一个 C/S 模型的程序，这是 server 端，对应的有 client 端：supervisorctl）和应用程序（即我们要管理的程序）。

显示示例配置

`echo_supervisord_conf`


默认的配置文件在/etc/supervisor/supervisord.conf下
如果需要从别的机器上查看管理页面，需要更改这样一行：
[inet_http_server]         ; inet (TCP) server disabled by default
port=*:9001        ; (ip_address:port specifier, *:port for all iface)

默认是只能本地访问

改好了之后使用 kill命名杀掉之前的进程，然后
sudo supervisord
重新启动
这样就能在别的机器上访问了

一个普通需要通过命令行启动的程序实例配置文件
```
[program:monitor-pi]
directory = /home/pi/super-pi/monitor-pi/ ; 程序的启动目录
command = python3 monitor-pi.py  ; 启动命令，可以看出与手动在命令行启>
动的命令是一样的
autostart = true     ; 在 supervisord 启动的时候也自动启动
startsecs = 5        ; 启动 5 秒后没有异常退出，就当作已经正常启动了
autorestart = true   ; 程序异常退出后自动重启
startretries = 3     ; 启动失败自动重试次数，默认是 3
user = pi          ; 用哪个用户启动
group = pi
redirect_stderr = true  ; 把 stderr 重定向到 stdout，默认 false
stdout_logfile_maxbytes = 20MB  ; stdout 日志文件大小，默认 50MB
stdout_logfile_backups = 1     ; stdout 日志文件备份数
; stdout 日志文件，需要注意当指定目录不存在时无法正常启动，所以需要手> 动创建目录（supervisord 会自动创建日志文件）
stdout_logfile = /var/log/super-pi/monitor-pi.log

; 可以通过 environment 来添加需要的环境变量，一种常见的用法是修改 PYTH ONPATH
; environment=PYTHONPATH=$PYTHONPATH:/path/to/somewhere
```

```
$ supervisorctl status                # 查看程序状态
$ supervisorctl stop usercenter       # 关闭 usercenter 程序
$ supervisorctl start usercenter      # 启动 usercenter 程序
$ supervisorctl restart usercenter    # 重启 usercenter 程序
$ supervisorctl reread                # 读取有更新（增加）的配置文件，不会启动新添加的程序
$ supervisorctl update                # 重启配置文件修改过的程序 如果是新增 将会读取配置并启动
```