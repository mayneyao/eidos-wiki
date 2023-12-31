---
sidebar_position: 2
---

# 什么是 Eidos

柏拉图有一个经典的洞穴理论，人类的认知能力类似于被困在一个洞穴中的囚徒。这个洞穴只有一个入口，外部世界的光线透过这个入口照射到洞穴内。囚徒身后有一堵墙，墙上有一系列移动的影子。囚徒从出生开始就一直被束缚在这个洞穴中，只能看到墙上的影子。因此，他们把这些影子当作真实世界的全部。柏拉图提出了理型世界的概念，认为现实世界是理型世界的投影。

Eidos 一词出自古希腊语 εἶδος（eîdos），即理型。

![洞穴理论](img/allegory_of_the_cave.webp)

## 现实世界是理型世界的投影

我有个很喜欢钓鱼的叔叔，他会制作钓鱼用的秤砣。在沙地上挖一个倒圆锥形的坑，垂直插一根牙签在中心，然后把铅水倒进去，等铅水凝固后，再把它挖出来，抽掉牙签就得到了一个圆锥形的秤砣，把鱼线穿进去，然后固定在鱼钩上面一点，这样就可以让鱼钩下沉到合适的位置。

模板+材料=产品，在现代工厂中是十分常见的生产模式。3D 打印更是将这种模式推向了极致。造房子的图纸，造汽车、飞机的蓝图，都是模板。模板是一种抽象，对物质的抽象，不依附于任何材料，它是一种纯粹的思维。它可以存在于人脑中，可以存在于纸张上，也可以存在于按照某种格式编码的二进制数据中。

![Barnsley_fern](img/barnsley_fern.webp)
[巴恩斯利蕨](https://en.wikipedia.org/wiki/Barnsley_fern) 是一个分形，它的生成算法是这样的：

```python
import matplotlib.pyplot as plt
import random

x = [0]
y = [0]


def f1(x, y):
    return 0, 0.16 * y


def f2(x, y):
    return 0.85 * x + 0.04 * y, -0.04 * x + 0.85 * y + 1.6


def f3(x, y):
    return 0.2 * x - 0.26 * y, 0.23 * x + 0.22 * y + 1.6


def f4(x, y):
    return -0.15 * x + 0.28 * y, 0.26 * x + 0.24 * y + 0.44


weights = [0.01, 0.85, 0.07, 0.07]

funcs = [f1, f2, f3, f4]
for _ in range(100000):
    func = random.choices(funcs, weights=weights, k=1)[0]
    x1, y1 = func(x[-1], y[-1])
    x.append(x1)
    y.append(y1)

plt.scatter(x, y, s=0.1, color="green")
plt.axis("off")
plt.savefig("barnsley_fern.png", dpi=300)
plt.show()
```

似乎在理型空间就就存在着它的原型，而描述这种原型方式也已经被人们找到。大自然只需要使用某方式打印出来，它就可以和现实世界的我们相见。**人们通过归纳抽象思考，由现实接近理型。**

## UI 是数据的投影

Figma 有个插件，可以结合 google sheet 的数据和 Figma 组件批量生成内容。设计师设计一个精美的组件模板，然后用一行一行的数据填充。这种模式可以高效的生产出大量的内容，而且保证了形式的一致性，比如打印工牌、节日贺卡等。

如果你用过多维表格，你应该能体会到它的要点：一份数据，不同的视图，不同的展示形式，以满足不同的需求。你可能也见过一份大纲式的 markdown， 转化为 mindmap。这些都是数据的不同投影。

React 社区中有着 ui = f(data) 的说法，数据驱动 UI。数据经过某种映射变成 UI，当数据变化时，UI 随之改变。f 就是我们写的代码。function 更像是一种 map，按照某种规则把数据转化为 UI。

近年来业界也逐渐盛行 headless cms 的模式，把内容和样式分离。让创作者更加关注内容而不是样式，这样在迁移的时候，能够得到一份原始的数据，而不是内容和样式耦合的难以处理的杂糅。这也是很多笔记爱好者推崇 markdown 的原因。

数据库在软件开发中扮演着重要的角色，它是数据存储和管理的中心。面向用户的是 UI。它通常是一种确定性的映射，受到供应商的限制。只有当用户能接触到[原始数据](/vision/raw-data-now)时，才能发挥数据的最大价值，但是这通常是不被允许的。

## 什么是 Eidos

Eidos 把自己定义为 all-in-one 的工作站，更加具体是说，是一个专注于提供优秀数据库表格和文档体验的工具。 可为什么是表格和文档？为什么不是思维导图？为什么不是白板？为什么不是...

### 表格 —— 抽象和计算

数据库、Excel 是很好的抽象和计算工具。建模建表就是你思考的体现，当你见识了很多信息，你会自然而然的类比它们是否有相同的特点，把它们归纳总结，抽象成一张表。这里有面向对象的意思，人们通常会按照不同的**维度**（特征）将事物抽象成一组数据，进而转化为可计算的数学表达。

![abstraction-and-map](img/abstraction-and-map.png)

从火箭升空探索宇宙到菜市场买菜都离不开计算。Excel 为使用者提供了实用的计算服务，信息时代工作的人们大部分都是围绕着数据库和 Excel 展开智力活动。因此数据表格是非常重要的功能，在针对事物不停的建模、抽象、计算和思考中，加深我们对事物的理解，以此由表象接近本质，由现实接近理型。

### 文档 —— 语言和表达

2023 年是 AI 的一年，不管是文本生成还是图像生成都给人留下深刻的印象。我之前会思考为什么我可以在本地的消费级设备上轻松运行 stable diffusion 生成图像，但是在跑 llm 时就捉襟见肘。后来我懂了，一个是视觉，另一个则是灵魂。二者不是一个量级的东西的。

你现在读到的文字是我的观点。柏拉图的思想也通过文字记录传承了下来，我们没有见过他，但是我们可以通过文字了解他的思想。文字记录是一个古来有之的需求，大到文明传承，小到个人表达，都离不开它。

> language is information and information is everything

## 理型空间

Airtable、Notion 之类的优秀产品从一定程度上替代了 Office 三件套，但是却把人们引入了 SaaS，也让用户逐渐失去了对自己数据的掌控。如果使用 Excel，那么数据量取决于个人设备的性能，但是在 SaaS 服务中却不是这样，你的数据是存储在别人的服务器上的，存在限制、被别人掌控。local-first 的本质是对数据的掌控，藏在云后的各种数据服务便是信息时代的洞穴。

如果只是回归到 Word、Excel 并不足以满足当下的需求。数据库和 Excel 结合的多维表格是更好的选择，Block-Styled 的文本编辑器相比于 Word 也更加简单易用。很大程度上，不规范的 Excel 使用（在表格旁边写一堆五颜六色的注意事项）、 复杂的 Word 排版，都是为了满足和他人协作的需求。但是在个人数据管理的场景下，我们完全可以更加关注数据内容的本质，而不是表象。

文档和表格都是帮助我们更好思考的工具，也是承载我们经历和思想的载体。Eidos 不会有方法论的预设，你把它当作简单的文档和表格工具即可。eidos.space 即理型空间，我们希望打造一个完全由**个人**掌控的数字空间，让每个人都能更好的记录和创作自己的内容。
