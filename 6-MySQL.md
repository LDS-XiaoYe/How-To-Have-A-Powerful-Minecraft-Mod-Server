## 六、在 CentOS 系统上使用宝塔面板搭建并使用 MySQL

[宝塔面板](www.bt.cn) 是一个简单好用的服务器运维面板，你可以在你的独立机或 VPS 上安装，使用数据库，搭建网站等。面板形式，上手难度低。

Windows 版宝塔面板安装过于简单，这里不作介绍。只介绍 Linux 版。如果你需要在其它 Linux 发行版的安装方式，可自行到宝塔官网查询。

### Part 1 安装宝塔面板

1. 以 root 身份进入终端，输入 `yum update` 更新软件库。
2. 到宝塔官网找到一键安装指令，并执行。

附 CentOS 版安装命令：

```
yum install -y wget && wget -O install.sh http://download.bt.cn/install/install_6.0.sh && sh install.sh
```

安装宝塔面板需要几分钟的时间，请耐心等待。

安装完成后会提示一段信息。

[TODO]