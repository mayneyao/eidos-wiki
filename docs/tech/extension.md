# 扩展机制

Eidos 十分重视可扩展性。Eidos Core 只会专注于文档和表格功能的开发，使其最小可用并且足够稳定。其它的上层应用统一通过扩展实现。

Eidos 提供了 2 种扩展模式：

1. App - 开发者可以用自己熟悉的 Web 技术栈编写任意 Web App, 只需要通过 Eidos SDK 和 Eidos 沟通数据即可。
2. Script - 脚本是 Eidos 中另外一种扩展功能的方式，它是一种无界面的 Extension，可以用来实现自动化、批量处理等功能，专注于数据处理和自动化。只需要了解 js/ts 就可以简单上手。

二者均依赖 Eidos SDK 运行，Eidos SDK 是和 Eidos 交互数据的核心方式，并且在 API/Extension/Script 中表现一致，公用同一套抽象接口。官方和第三方的功能开发都依附于 Eidos SDK，不同的是官方实现可能会依赖一致内置的接口，SDK 则会选择性的暴露接口。

## App

开发者使用任意的 web 技术栈编写 app，也可以把已经存在的 app 接入 Eidos SDK，将其转化为 Eidos App，实现对数据的操作和持久化。开发者无需关心部署问题，体验类似于浏览器扩展。

App 可以依附于 Eidos 运行，也可以不依赖于 Eidos 独立运行, 这种模式下 Eidos 仅仅作为零成本抽象的 Local-first App 数据基础层，让 Web App 具备数据持久化和 p2p 多设备同步的能力。

## Script

Script 也被称之为 Headless App。通过 js/ts 编写的函数，大概类似于 Cloudflare Worker 的开发体验。一些概念可以做类比：

| function | Cloudflare Worker | Eidos Script |
| -------- | ----------------- | ------------ |
| 逻辑处理 | `worker`          | `script`     |
| 数据存储 | `KV/D1`           | `table`      |
| 对象存储 | `R2`              | `OPFS`       |

Script 的开发设计参考了 Cloudflare Worker 的实现。大家都依附于 Web 生态运行，不同的是一个在边缘节点中，一个在本地浏览器中。一个是 web 通用型的解决方案，一个是仅服务于 Eidos 的解决方案。

通过编写 script，可以轻松定制自己的工作流。开发者可以分享自己的 Script 给其它用户使用。

### 参考

- https://github.com/mayneyao/eidos-script-template 编写 script 的模板仓库
