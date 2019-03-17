---
title: toml配置语言
tags: []
---

目前版本的问题:对中文的key和value都会编程/uxxx的形式.不能自动解码.  所以暂时还是用ini配置文件.

## TOML 的目标

TOML 的目标是成为一个极简的配置文件格式。TOML 被设计成可以无歧义地被映射为哈希表，从而被多种语言解析。

## 例子

```TOML
title = "TOML 例子"

[owner]
name = "Tom Preston-Werner"
organization = "GitHub"
bio = "GitHub Cofounder & CEO\nLikes tater tots and beer."
dob = 1979-05-27T07:32:00Z # 日期时间是一等公民。为什么不呢？

[database]
server = "192.168.1.1"
ports = [ 8001, 8001, 8002 ]
connection_max = 5000
enabled = true

[servers]

  # 你可以依照你的意愿缩进。使用空格或Tab。TOML不会在意。
  [servers.alpha]
  ip = "10.0.0.1"
  dc = "eqdc10"

  [servers.beta]
  ip = "10.0.0.2"
  dc = "eqdc10"

[clients]
data = [ ["gamma", "delta"], [1, 2] ]

# 在数组里换行没有关系。
hosts = [
  "alpha",
  "omega"
]

```

TOML 是大小写敏感的。

## 注释

使用 `#` 表示注释：

```TOML
# I am a comment. Hear me roar. Roar.
key = "value" # Yeah, you can do this.

```

## 字符串

字符串和 JSON 的定义一致，只有一点除外：　TOML 要求使用　UTF-8 编码。

注释以引号包裹，里面的字符必须是　UTF-8 格式。引号、反斜杠和控制字符（U+0000 到 U+001F）需要转义。

```TOML
"I'm a string. \"You can quote me\". Name\tJos\u00E9\nLocation\tSF."

```

常用的转义序列：

```TOML
\b     - backspace       (U+0008)
\t     - tab             (U+0009)
\n     - linefeed        (U+000A)
\f     - form feed       (U+000C)
\r     - carriage return (U+000D)
\"     - quote           (U+0022)
\/     - slash           (U+002F)
\\     - backslash       (U+005C)
\uXXXX - unicode         (U+XXXX)

```

使用保留的特殊字符，TOML　会抛出错误。例如，在　Windows 平台上，应该使用两个反斜杠来表示路径：

```TOML
wrong = "C:\Users\nodejs\templates" # 注意：这不会生成合法的路径。
right = "C:\\Users\\nodejs\\templates"

```

二进制数据建议使用　Base64　或其他合适的编码。具体的处理取决于特定的应用。

## 整数

整数就是一些没有小数点的数字。想用负数？按直觉来就行。整数的尺寸最小为64位。

## 浮点数

浮点数带小数点。小数点两边都有数字。64位精度。

```TOML
3.1415
-0.01

```

## 布尔值

布尔值永远是小写。

```TOML
true
false

```

## 日期时间

使用　ISO 8601　完整格式。

```TOML
1979-05-27T07:32:00Z

```

## 　数组

数组使用方括号包裹。空格会被忽略。元素使用逗号分隔。注意，不允许混用数据类型。

```TOML
[ 1, 2, 3 ]
[ "red", "yellow", "green" ]
[ [ 1, 2 ], [3, 4, 5] ]
[ [ 1, 2 ], ["a", "b", "c"] ] # 这是可以的。
[ 1, 2.0 ] # 注意：这是不行的。

```

数组可以多行。也就是说，除了空格之外，方括号间的换行也会被忽略。在关闭方括号前的最终项后的逗号是允许的。

## 表格

表格（也叫哈希表或字典）是键值对的集合。它们在方括号内，自成一行。注意和数组相区分，数组只有值。

```TOML
[table]

```

在此之下，直到下一个　table 或　EOF 之前，是这个表格的键值对。键在左，值在右，等号在中间。键以非空字符开始，以等号前的非空字符为结尾。键值对是无序的。

```TOML
[table]
key = "value"

```

你可以随意缩进，使用 Tab 或空格。为什么要缩进呢？因为你可以嵌套表格。

嵌套表格的表格名称中使用`.`。你可以任意命名你的表格，只是不要用点，点是保留的。

```TOML
[dog.tater]
type = "pug"

```

以上等价于如下的 JSON 结构：

```json
{ "dog": { "tater": { "type": "pug" } } }

```

如果你不想的话，你不用声明所有的父表。TOML　知道该如何处理。

```TOML
# [x] 你
# [x.y] 不需要
# [x.y.z] 这些
[x.y.z.w] # 可以直接写

```

空表是允许的，其中没有键值对。

只要父表没有被直接定义，而且没有定义一个特定的键，你可以继续写入：

```TOML
[a.b]
c = 1

[a]
d = 2

```

然而你不能多次定义键和表格。这么做是不合法的。

```TOML
# 别这么干！

[a]
b = 1

[a]
c = 2

```

```TOML
# 也别这个干

[a]
b = 1

[a.b]
c = 2

```

## 表格数组

最后要介绍的类型是表格数组。表格数组可以通过包裹在双方括号内的表格名来表达。使用相同的双方括号名称的表格是同一个数组的元素。表格按照书写的顺序插入。双方括号表格如果没有键值对，会被当成空表。

```TOML
[[products]]
name = "Hammer"
sku = 738594937

[[products]]

[[products]]
name = "Nail"
sku = 284758393
color = "gray"

```

等价于以下的　JSON 结构：

```json
{
  "products": [
    { "name": "Hammer", "sku": 738594937 },
    { },
    { "name": "Nail", "sku": 284758393, "color": "gray" }
  ]
}

```

表格数组同样可以嵌套。只需在子表格上使用相同的双方括号语法。每一个双方括号子表格回从属于最近定义的上层表格元素。

```TOML
[[fruit]]
  name = "apple"

  [fruit.physical]
    color = "red"
    shape = "round"

  [[fruit.variety]]
    name = "red delicious"

  [[fruit.variety]]
    name = "granny smith"

[[fruit]]
  name = "banana"

  [[fruit.variety]]
    name = "plantain"

```

等价于如下的　JSON 结构：

```json
{
  "fruit": [
    {
      "name": "apple",
      "physical": {
        "color": "red",
        "shape": "round"
      },
      "variety": [
        { "name": "red delicious" },
        { "name": "granny smith" }
      ]
    },
    {
      "name": "banana",
      "variety": [
        { "name": "plantain" }
      ]
    }
  ]
}

```

尝试定义一个普通的表格，使用已经定义的数组的名称，将抛出一个解析错误：

​                        

```TOML
# 不合法的　TOML

[[fruit]]
  name = "apple"

  [[fruit.variety]]
    name = "red delicious"

  # 和上面冲突了
  [fruit.variety]
    name = "granny smith"

```