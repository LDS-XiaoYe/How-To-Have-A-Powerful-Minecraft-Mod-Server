## 二、认识服务端

问：论坛服务端整合包版有很多优秀的服务端整合包，为什么我要自己制作？

答：因为自己制作服务端可以让你自己知道在哪里做过什么。如果直接使用现成的服务端，小白很难理解各个插件的作用，怎么配置，也不会提高你的技术水平。自己的经历是无价之宝。

### Part 1 服务端核心

我们回家需要钥匙。开启服务端也需要钥匙，而服务端核心就是这把“钥匙”。服务端核心是一个 jar 文件。由于本帖主要讨论模组服，这里仅介绍模组服主流版本的服务端核心。

- 1.7.10
  - [Uranium](https://www.mcbbs.net/thread-723871-1-1.html)
- 1.12.2
  - [CatServer](https://catserver.moe/)
  - [Mohist](https://www.mcbbs.net/thread-916340-1-1.html)

### Part 2 了解 EULA

下载完服务端核心和及其所需的 `libraries` 后，将其移动至同一文件夹。并在此文件夹内创建一个名为 `eula.txt` 的文件。再打开这个文本文件，写入

```
eula=true
```

保存，关闭即可。

EULA 是 End User Licence Agreement 的缩写。翻译为中文就是「最终用户许可协议」。同意了 Mojang 的最终用户许可协议才可以继续启动服务端。

至于最终用户许可协议的具体内容，自行前往 Mojang 官网寻找。

### Part 3 了解启动脚本

顾名思义，启动脚本是用来启动服务端的。运行了正确的启动脚本后，你的服务端将启动。初次启动后，将生成一些文件并加载。第二次及以后的启动，会加载你服务端的数据。加载数据需要一定的时间，模组服的加载时间比纯净服长。

初学者听到脚本这样的名词，可能会觉得困难。其实写启动脚本并不需要水平多么高的编程基础。写完后也就是调整一下内存等，改动不大。当然你也可以参考现成的，基本上复制后简单修改一下就可以用。

Windows 系统步骤如下：

1. 创建一个名为 `start.bat` 的文件。
2. 写入脚本，后保存

就这么简单，你学会~~废~~了吗？

我这里展示一份启动脚本，`rem` 后是注释，可以删除。你可以修改此脚本后直接使用。

```
@echo off
:head
set memory=4
title Minecraft xxx 已分配内存:%memory%G
echo 已设置内存为%memory%G
rem 这里是注释，上面的数字是分配的内存，单位为GB，自行修改上面即可，不需要改启动代码
set mainfile=xxx
rem 上面是服务端核心名字，不需要加文件后缀名，修改后不需要改启动代码
java -Xms%memory%G -Xmx%memory%G -XX:+UseG1GC -jar %mainfile%.jar -nogui
echo 服务器已关闭，将于10秒后重启
ping -n 10 127.0.0.1>nul
goto head
rem 跳回head，继续执行，达到崩服自动重启的效果
pause
```

保证启动脚本位于服务端根目录。运行后会弹出一个黑框框，不断的提示一些英文。最后看到 `Done` 就说明启动成功了。

这时候可以输入一些指令测试一下，如

```
say test
```

你将看到控制台显示 `[Server]test` 。然后你就可以输入 `/stop` 关服并安装你的插件、Mod 了。

### Part 4 服务端启动后生成了什么，有什么用？

| 文件名               | 备注                                                         |
| -------------------- | ------------------------------------------------------------ |
| bukkit.yml           | Bukkit 配置文件，关闭服务器，因白名单而被断开连接，服务器满员等文本可以在这里修改。Bukkit 系服务端会生成此文件。 |
| spigot.yml           | Spigot 配置文件，以 Spigot 为基础的服务端核心会生成此文件。有一些与优化相关的配置项目。 |
| ops.json             | 这里有服务器 OP 的 UUID 等信息。                             |
| server.properties    | 服务端配置文件。可以在这里面修改端口等。                     |
| whitelist.json       | 白名单。                                                     |
| bannned-players.json | 已封禁的玩家的 UUID 等信息。                                 |
| banned-ips.json      | 已封禁的 IP。                                                |
| config               | Mod 的配置文件夹。里面将包含所有已添加的 Mod 的配置文件。    |
| logs                 | 存储服务端日志。                                             |
| libraries            | 服务端库文件。                                               |
| plugins              | 插件文件夹。                                                 |

### Part 5 一般服务器必装插件

- [EssentialsX](http://www.mcbbs.net/thread-619883-1-1.html)
  - 基础插件，有 `/tpa` 指令那个。
- [PlugMan](https://www.mcbbs.net/thread-954532-1-1.html)
  - 可以不关服加载、卸载插件。
  - Mohist 等自带此功能的服务端核心可以不加此插件。
- [AuthMe](http://www.mcbbs.net/thread-442729-1-1.html) 
  - 登录插件
  - 使用正版登录或外置登录的服务器可不加此插件。

- [DoubleLoginFix](http://www.mcbbs.net/thread-817128-1-1.html)
  - 修复登录插件的 Bug。

因为本帖主要讨论模组服，插件就不多说了。有意者可浏览论坛服务端插件版块。