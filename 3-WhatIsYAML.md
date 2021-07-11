## 三、认识 YAML

我们用 [百度百科](https://baike.baidu.com/item/YAML/1067697) 的一段介绍引入话题。

> YAML是一个可读性高，用来表达数据[序列化](https://baike.baidu.com/item/序列化)的格式。YAML参考了其他多种语言，包括：[C语言](https://baike.baidu.com/item/C语言)、[Python](https://baike.baidu.com/item/Python)、[Perl](https://baike.baidu.com/item/Perl)，并从[XML](https://baike.baidu.com/item/XML)、电子邮件的数据格式（RFC 2822）中获得灵感。Clark Evans在2001年首次发表了这种语言，另外Ingy d?t Net与Oren Ben-Kiki也是这语言的共同设计者。当前已经有数种编程语言或脚本语言支持（或者说解析）这种语言。
> YAML是"YAML Ain't a Markup Language"（YAML不是一种[标记语言](https://baike.baidu.com/item/标记语言)）的[递归缩写](https://baike.baidu.com/item/递归缩写)。在开发的这种语言时，YAML 的意思其实是："Yet Another Markup Language"（仍是一种[标记语言](https://baike.baidu.com/item/标记语言)），但为了强调这种语言以数据做为中心，而不是以标记语言为重点，而用反向缩略语重命名。

大多数插件的配置文件是后缀名为 `.yml` 的YAML 文件 ，根据插件默认配置的格式修改配置文件即可。

### Part 1 举个例子

我们拿 ChestCommands 菜单插件来举例子。

```
test:
  NAME: '&atest'
  LORE:
    - 'test'
  ID: 1
  KEEP-OPEN: true
  POSITION-X: 1
  POSITION-Y: 1
```

观察后，我们可以发现此段配置具有以下特点：

- 每子项前有相同数量的空格
- 英文冒号后有一个空格
- 文字前后有引号

一般来说，按照插件生成的默认配置的格式继续写即可。

### Part 2 拓展

**如果您没有编程基础，可跳过此小节，不影响后续阅读。**

Java 有 8 种基础数据类型，如下：

- byte
  - 位
- short
  - 短整数
- int
  - 整数
- long
  - 长整数
- float
  - 单精度
- double
  - 双精度
- char
  - 字符
- boolean
  - 布尔值
