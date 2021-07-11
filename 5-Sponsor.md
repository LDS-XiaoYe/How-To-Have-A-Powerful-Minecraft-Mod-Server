## 五、自动赞助系统

维持服务器必然需要一定的资金。建议各位服主不要被所谓的「情怀」束缚。随着你服务器规模的扩大，玩家赞助有时无法及时回应。这时，自动赞助系统就是你的好帮手。

### Part 1 准备工作

安装以下插件：

- [Vault](https://www.mcbbs.net/thread-703488-1-1.html)
  - 经济前置插件
- [PlayerPoints](https://www.mcbbs.net/thread-514161-1-1.html)
  - 点券插件
- [ChestCommands](https://www.mcbbs.net/thread-933158-1-1.html)
  - 菜单插件
- [CommandCode](http://www.mcbbs.net/thread-346482-1-1.html)
  - 激活码插件

在你的服务器安装好这些插件后，我们需要找一个靠谱的自动发卡平台。一定要靠谱。有条件的可以自己搭建一个发卡平台。

决定你的点券汇率，比如 1 元 = 10 点券，1 元 = 100 点券。根据你的喜好来。

### Part 2 自动发放点券

> 以生成 10 点券激活码为例。

使用 CommandCode 生成 100 条兑换 10 点券的激活码。

输入以下指令：

> 在控制台输入请删掉 "/"

```
/code create 100 points give %player% 10
```

生成完以后，输入

```
/code output 10 points give %player% 10
```

输入完后到 `plugins/CommandCode` 内可以找到 `10.txt`，里面就是你生成的激活码，导入到发卡平台即可。

现在玩家可以购买到卡密并兑换点券了。这样我们就可以写点券商城，让玩家消费了。

用 ChestCommands 写点券商城。ChestCommands 有编辑器，但我推荐初学者手写，熟练后，手写比编辑器还快。

放一个样例，以下是样例展示内容：

- 菜单显示 6 行。
- 菜单标题为「点券商城」
- 10 点券购买一个石头且购买后给予提示

```
name: '点券商城'
rows: 6
auto-refresh: 5
stone:
  COMMAND: 'give: 1, 1;tell: &b服务器&7>>>&a购买成功。'
  NAME: '&a购买石头'
  LORE:
  - '&7⊙ &f石头10点券/个'
  ID: 1
  POINTS: 10
  POSITION-X: 1
  POSITION-Y: 1
```

### Part 3 自动发放大量物品

我们知道，模组服务器的赞助礼包通常有大量物品。

本小节用 热力膨胀、CustomNPC 模组做示范，并使用 CommandCode，RPGItem，EasyKitsRel 插件配合。

1. 用 RPGItem 创建一个物品，并命名为兑换券。
2. 保证背包内只有一个兑换券，然后使用 EasyKitsRel 插件创建一个礼包。
3. 使用热力膨胀的谐振保险箱，并附魔扩容 IV，将保险箱扩容到最大容量。
4. 将你想发放的物品塞进去。然后打开并关闭一次保险箱，鼠标中键复制。
5. 在主城等地设置 NPC，使用兑换券兑换保险箱。
6. 用 CommandCode 插件，创建领取兑换券，切换权限组的激活码，然后上架发卡平台。

至此，你已经学会了如何自动发放物品。