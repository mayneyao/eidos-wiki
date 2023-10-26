---
sidebar_position: 1
---

# Eidos 技术架构

Eidos 的核心基于 Web 构建，是一个完全运行在 Web 中的 app。我们把 "服务端" 和客户端一起放在 Web 中。并且力求尽可能少的引入第三方 SaaS 服务，以保证数据的安全性和隐私性。Eidos 是面向下一代的 Web App，大量使用全新的 Web API。

## 为什么是 Web

1. Web 的跨平台、免安装在软件分发上有天然的优势。
2. Web 正在成为桌面操作系统之上的另一层抽象。比操作系统更像操作系统，我们可以看到移动端操作系统对数据和隐私掌控，权限管控很重要。但是在野蛮生长的桌面操作系统中，还没有建立起类似的机制。Web 的沙盒隔离和权限管控正在填补这个空白。
3. Eidos 的核心计算层，以 WASM 的形式运行在 Web Worker 中。我们希望 Eidos 不仅能运行在每个人的浏览器中，也希望它可以部署在诸如 Cloudflare Worker、Deno Deploy 等围绕 Web Worker 打造的 Serverless 边缘计算环境中，更加方便地支持用户做自动化。

![eidos-infra](img/infra.png)

## 技术选型的原则

1. Web-first

   1. 通过 Web 跨平台，PWA 实现离线支持。
   2. 与传统 BS 架构不同，“服务端” 被实现在 web 的 worker 中。web client 才是本位。
      1. web client 没办法提供 http 的 api，所以我们通过 websocket 和一个 [api](api) agent 连接一次来提供 api 服务。api 依赖 web client 运行，而不是 client 依赖 server api 运行。你可以理解为 server 从云端转移到了 web worker 中。

2. Serverless

   1. 真正意义上的无服务器，没有 docker，不用启动数据库、启动服务器。
   2. 大量使用 WASM 技术，把服务端的功能移植到 web worker 中。
      1. 使用 sqlite-wasm 在 web worker 中运行数据库。
      2. 使用 hnswlib-wasm 在 web worker 中运行向量搜索，而不依赖外部的向量数据库
   3. 通过 P2P 实现多设备数据同步，尽量避免引入中心化的服务器。

3. Local-first
   1. 网络是可选项。对于无法只依赖本地 web 实现的功能，倾向于使用 serverless 服务实现。
      1. web 端没有办法跨域查看图片，所以我们通过 cf worker 实现图片的反代。图片缓存在 OPFS 中，保证离线时候的浏览体验。

## WASM & Worker

- sqlite-wasm
  - sqlite-wasm 的 vfs + web opfs，使得我们可以在 web 上存储大量数据，查询和计算都是基于 sqlite 来实现的。
- hnswlib-wasm
  - 处理向量搜索

## OPFS

[Eidos 如何存储数据](data-store)

## WebRTC

WebRTC 把 p2p 带到了 web 中，我们以此实现去中心化的数据同步和协作
