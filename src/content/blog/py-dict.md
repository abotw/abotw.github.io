---
title: Python Dict
description: Dict —— 一个以 O(1) 速度瞬间定位数据的魔法管家。
publishDate: 2025-12-08
---

在一个存了 10,000 个元素的列表中，试图找到“那个特定的数据”，是让人蛮绝望的。这就好比在乱糟糟的脏衣篓里找某只失踪的袜子——随着衣服（数据）越来越多，需要的时间呈线性增长。

但是 Python 有一个作弊神器：**字典 (Dictionary, 简称 dict)**。

如果说列表（List）是一排按顺序坐好的士兵，那么字典就是一个巨大的、带有魔法标签的储物柜。我们不需要知道东西放在第几个格子里，你只需要喊出标签的名字（Key），数据（Value）就会瞬间出现在我们面前。

## 1. 什么是字典？

在 Python 中，字典是一种**可变容器模型**，可存储任意类型对象。它的核心逻辑是：**Key-Value Pair（键值对）**。

-   **Key (键)**： 类似于现实生活中的“身份证号”或“用户名”。它是唯一的，而且必须是不可变的（比如字符串、数字、元组）。
-   **Value (值)**： 类似于“这个身份证号对应的人”。它可以是任何东西：数字、字符串、列表，甚至另一个字典。

创建字典的正确姿势：

```python
# 最常见的花括号写法
hero_profile = {
    "name": "Tony Stark",
    "alias": "Iron Man",
    "net_worth": 12400000000,
    "is_alive": False  # 剧透预警
}

# 也可以用 dict() 构造函数
empty_pocket = dict()
```

## 2. 查：优雅地获取数据

新手和老手的区别，往往体现在如何从字典里取值。

### A. 简单粗暴的方括号 `[]`

这就像不敲门直接踹门进房间。如果房间（Key）存在，皆大欢喜；如果不存在，Python 会直接给你甩一个 `KeyError` 让你程序崩溃。

```python
print(hero_profile["name"])  # 输出: Tony Stark
# print(hero_profile["girlfriend"]) # 报错！KeyError: 'girlfriend'
```

### B. 彬彬有礼的 `.get()`

这就像先敲门：“请问有人在吗？”。如果有，返回数据；如果没有，它会礼貌地返回 `None`（或者指定的默认值），绝不报错。

```python
# 安全获取
gf = hero_profile.get("girlfriend") # 返回 None，程序继续运行

# 带默认值的获取
weapon = hero_profile.get("weapon", "Fists") # 如果找不到 weapon，就假设是拳头
print(weapon) # 输出: Fists
```

## 3. 增与改：霸道的赋值

字典在“增”和“改”上表现得非常霸道且高效。不需要调用复杂的函数，只需要用方括号赋值即可。

-   **如果 Key 不存在**：那就是“新增”。
-   **如果 Key 已存在**：那就是“覆盖/更新”。

```python
# 新增一个键值对
hero_profile["location"] = "New York" 

# 修改已有的值 (Tony 复活了？)
hero_profile["is_alive"] = True 
```

由于字典的 Key 是唯一的，如果重复对同一个 Key 赋值，旧值会被无情地覆盖，找都找不回来。

## 4. 删：断舍离的艺术

不想要某个数据了，Python 提供了几种“分手”的方式。

-   **`pop(key)`**：这是最推荐的方式。它不仅会删除这对数据，还会把被删除的值“吐”出来给你，仿佛在说：“拿着你的东西，走！”
-   **`del dict[key]`**：这是核武器。直接从内存中抹去，不留痕迹。如果 Key 不存在，则会报错。
-   **`clear()`**：清空整个字典，只留下一个空壳 `{}`。

```python
# 拿走钱，然后删除 net_worth 条目
money = hero_profile.pop("net_worth") 
print(money) # 12400000000
print(hero_profile) # 此时字典里已经没有 net_worth 了
```

## 5. 遍历：在字典里散步

字典不像列表那样有顺序（注：Python 3.7+ 只有插入顺序），所以遍历时的思维方式略有不同。

```python
# 1. 最常用的：同时遍历 键 和 值
# .items() 会把字典变成一系列元组
for key, value in hero_profile.items():
    print(f"{key}: {value}")

# 2. 只想看有哪些 键 (Keys)
for key in hero_profile.keys():
    print(key)

# 3. 只想看有哪些 值 (Values)
for val in hero_profile.values():
    print(val)
```

## 6. 为什么字典这么快？

为什么字典查找速度比列表快？

这涉及到了**哈希表 (Hash Table)** 的概念。简单来说，列表查找是“翻书”，需要一页一页翻（时间复杂度 $O(n)$）；而字典查找是“查索引”，Python 通过计算 Key 的哈希值，直接算出数据在内存中的地址（平均时间复杂度 $O(1)$）。

无论字典里有 10 个数据还是 1000 万个数据，查找一个 Key 的时间几乎是一样的。这就是为什么在处理大量关联数据时，字典是绝对的王者。

## 7. 总结

Python 的字典是强大、灵活且高效的工具。

1.  **键必须唯一且不可变**。
2.  **善用 `.get()`** 避免程序崩溃。
3.  **理解 Key-Value 结构**，把数据看作带标签的储物柜。

