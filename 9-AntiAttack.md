## 九、防御攻击

随着服务器的规模变大，你可能会被不怀好意的人攻击。

攻击的主要方式是 DDoS、压力测试（简称「压测」）。

通常压测分为以下两种：

- MOTD 压测
  
  > MOTD 就是在客户端的服务器列表中，服务器显示的标语。
  
  - 不断刷新你的 MOTD，消耗大量资源。
  - MOTD 就是打开 Minecraft 多人游戏服务器列表时，服务器显示的标语。
  
- 假人压测
  
  - 不断让假人进出服务器，消耗大量资源。

DDoS 的中文名是分布式拒绝服务，参考 [百度百科](https://baike.baidu.com/item/%E5%88%86%E5%B8%83%E5%BC%8F%E6%8B%92%E7%BB%9D%E6%9C%8D%E5%8A%A1%E6%94%BB%E5%87%BB/3802159) 的解释：

>分布式拒绝服务攻击可以使很多的计算机在同一时间遭受到攻击，使攻击的目标无法正常使用，分布式拒绝服务攻击已经出现了很多次，导致很多的大型网站都出现了无法进行操作的情况，这样不仅仅会影响用户的正常使用，同时造成的经济损失也是非常巨大的。
>
>分布式拒绝服务攻击方式在进行攻击的时候，可以对源IP地址进行伪造，这样就使得这种攻击在发生的时候隐蔽性是非常好的，同时要对攻击进行检测也是非常困难的，因此这种攻击方式也成为了非常难以防范的攻击。

有效防御此类攻击需要机房硬件支持。故本章仅介绍防御压测的方法。

受到 DDoS 攻击时，现象包括但不限于 CPU 占用 100%，后台连接卡顿。一旦发现此类攻击，请及时联系你的服务商。

### Part 1 方案一

本方案使用外置登录和蹦极端配合。

你需要具有的条件：

- 一台能建站的机器
- 如果要在大陆服务器上搭建网站，需要 ICP 备案和公安备案。不满足条件可搭建在境外服务器上。

我们需要搭建 [Blessing Skin](https://github.com/bs-community/blessing-skin-server) 皮肤站并使用 [authlib-injector](https://github.com/yushijinhun/authlib-injector) 以及皮肤站内的 Yggdrasil API 插件实现外置登录。

authlib-injector 通过劫持 Mojang 的正版验证 API 实现外置登录。因此，**一旦使用本方案的外置登录，正版用户将无法使用正版账号登录**。

目前大部分主流启动器如 HMCL 已经提供 authlib-injector 功能，直接使用即可。

#### Blessing Skin 搭建教程

你可以参阅 [Bleesing Skin 用户手册](https://blessing.netlify.app/) 来搭建 Blessing Skin 皮肤站。

#### 使用外置登录的 Waterfall 搭建步骤

蹦极端建议使用 [Waterfall](https://github.com/PaperMC/Waterfall)。

1. 到 Waterfall 官方下载网站下载最新版 Waterfall 核心。

2. 使用启动脚本启动 Waterfall 核心。

3. 到 Waterfall 的 `config.yml` 内配置子服务器，并将 `online-mode`  和 `ip-forward` 设为 `true`。

4. 将其他子服 `spigot.yml` 内的 `bungeecord` 设为 `true`，保持 `online-mode` 为 `false`。

5. 在 Waterfall 启动脚本内加入

   ```
   javaagent:./yourAuthlibInjectorFileName=https://yourWebsite.com/api/yggdrasil
   ```


至此，你可以使用支持 `authlib-injector` 的启动器登录你的皮肤站账号，并进入服务器。

### Part 2 方案二

方案二即使用 [Bot-Sentry](https://www.mcbbs.net/thread-915362-1-1.html) 等插件防御。效果通常不好，可能会阻碍正常玩家进入。因此本帖不介绍此类方案。