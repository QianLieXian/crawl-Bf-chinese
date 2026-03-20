[![Build Status](https://github.com/crawl/crawl/workflows/Build/badge.svg)](https://github.com/crawl/crawl/actions/)

# 地城爬行：石汤（Dungeon Crawl Stone Soup）

《地城爬行：石汤》（DCSS）是一款围绕地城探索、战术战斗与魔法构筑展开的经典 Roguelike。你将扮演不同种族与职业的冒险者，面对变化莫测的神祇、凶险的怪物与层层深入的迷宫。想要通关，你需要的不只是“数值强”，更是冷静判断、资源管理与临场应变。

如果你喜欢“每一步都很关键”的游戏体验，这就是那种会让你又紧张又上头的作品。

## 目录

1. [开始游玩](#开始游玩)
2. [中文汉化与打包（含 Windows 10）](#中文汉化与打包含-windows-10)
3. [社区与交流](#社区与交流)
4. [你可以如何参与](#你可以如何参与)
5. [许可证与项目历史](#许可证与项目历史)

## 开始游玩

安装方式请先阅读官方安装文档：[crawl-ref/INSTALL.md](crawl-ref/INSTALL.md)。

如果你想马上开一局，建议按这个顺序入门：

- 进入游戏后选择教程模式（Tutorial）；
- 阅读新手速通指南：[crawl-ref/docs/quickstart.md](crawl-ref/docs/quickstart.md)；
- 想系统学习机制，再看完整手册：[crawl-ref/docs/crawl_manual.rst](crawl-ref/docs/crawl_manual.rst)。

游戏内也提供常见问题列表：输入 `?Q` 即可查看。

### 在线游玩

你可以直接在线体验 DCSS，与其他玩家同服竞争、围观观战或复盘学习。前往官网 [crawl.develz.org](https://crawl.develz.org/)，点击 **“Play Online Now!”**，选择离你最近的服务器即可。支持浏览器游玩，也支持 SSH 连接。

### 离线游玩

DCSS 提供经典 ASCII 版本与图形 Tiles 版本，可在此下载（Linux / Windows / macOS）：
[https://crawl.develz.org/download.htm](https://crawl.develz.org/download.htm)

## 中文汉化与打包（含 Windows 10）

本仓库包含面向中文玩家的深度汉化，重点覆盖：

- 怪物名称与描述
- 战斗提示、状态文本
- 场景/分支说明
- UI 菜单与帮助文本
- 属性、技能、职业、种族等核心说明

主要汉化目录：

- `crawl-ref/source/dat/database/zh/`
- `crawl-ref/source/dat/descript/zh/`

如果你在游玩过程中发现漏翻、误译、术语不统一，欢迎提交 Issue 或 PR。

### 打包教程入口

- 中文打包文档（含 Windows 10）：[`PACKAGING_ZH.md`](PACKAGING_ZH.md)

### Windows 10 快速打包流程（简版）

如果你主要在 Windows 10 上构建，建议优先使用 **MSYS2 / MinGW64** 环境：

1. 安装 MSYS2，并打开 `MSYS2 MinGW 64-bit` 终端。
2. 安装基础工具链与常用依赖（`git`、`make`、`gcc`、`python`、`SDL2` 等）。
3. 进入 `crawl-ref/source`，执行图形版构建：
   ```bash
   make -j"$(nproc)" TILES=y
   ```
4. 构建完成后，连同可执行文件与运行所需资源目录一起打包分发。

> 详细步骤、注意事项与常见问题请以 `PACKAGING_ZH.md` 为准。

## 社区与交流

- 官方主页：[crawl.develz.org](https://crawl.develz.org/)
  - 在线 WebTiles
  - 各平台离线下载
  - 官方论坛：[tavern.dcss.io](https://tavern.dcss.io/)
- [/r/roguelikes Discord](https://discord.gg/S5F2H32)
- [/r/dcss subreddit](https://www.reddit.com/r/dcss/)
- IRC：Libera 上的 `#crawl`（开发相关可在 `#crawl-dev`）

## 你可以如何参与

如果你喜欢这款游戏，欢迎一起把它变得更好。完整协作流程请参考贡献指南：
[crawl-ref/docs/develop/contribution-process.md](crawl-ref/docs/develop/contribution-process.md)

### 反馈问题（Bug Report）

任何时候，稳定复现并清晰描述问题，都是最有价值的帮助之一。很多线上服务器运行的是持续更新的开发版，若发现 Bug，请提交到：
[https://github.com/crawl/crawl/issues](https://github.com/crawl/crawl/issues)

如果你有界面交互或玩法改进建议，也欢迎提出；但对于较大改动，通常先在社区讨论会更高效。

### 地图（Vault）制作

DCSS 的关卡由大量手工设计（同时支持随机变化）的 vault 组合而成。入门建议从简单的入口 vault 开始：
[crawl-ref/source/dat/des/arrival/simple.des](crawl-ref/source/dat/des/arrival/simple.des)

还可以参考关卡设计文档：
[crawl-ref/docs/develop/levels/introduction.txt](crawl-ref/docs/develop/levels/introduction.txt)

### 怪物台词与物品描述

怪物台词是游戏风味的重要来源。你可以参考格式说明：
[crawl-ref/docs/develop/monster_speech.txt](crawl-ref/docs/develop/monster_speech.txt)

物品描述可在游戏内通过 `?/` 查看，也可离线查看：
[crawl-ref/source/dat/descript/](crawl-ref/source/dat/descript/)

建议遵循这些写作原则：

- 突出风味，同时尽量体现关键优劣势；
- 避免堆砌具体数值；
- 引用可用，但尽量避免过于泛化、缺少辨识度的表达。

### 图块（Tiles）

无论是优化现有图块，还是制作常见元素（例如地板）的变体，我们都欢迎。你可以先在社区联系开发者，再通过 PR 提交作品。

### 代码补丁（Patches）

不论你是资深开发者还是刚开始接触项目，都可以 fork 源码后提交补丁。Bug 修复与新功能都很受欢迎。

对于规模较大的改动，建议先与开发团队沟通，确认方向与可合入性。

编码前建议先阅读：
[crawl-ref/docs/develop/coding_conventions.md](crawl-ref/docs/develop/coding_conventions.md)

## 许可证与项目历史

DCSS 使用 GPLv2+ 许可证，完整文本见：[LICENSE](LICENSE)

DCSS 源自 Linley 的 Dungeon Crawl。Linley 版最后一个 alpha（v4.1）由 Brent Ross 于 2005 年发布。自 2006 年起，Dungeon Crawl Stone Soup 团队持续维护与开发至今。完整贡献者名单见：
[crawl-ref/CREDITS.txt](crawl-ref/CREDITS.txt)

DCSS 使用了以下开源组件，感谢对应开发者：

- Lua 脚本语言（游戏内功能与宏）：[license](crawl-ref/docs/license/lualicense.txt)
- PCRE 正则库：[license](crawl-ref/docs/license/pcre_license.txt)
- SQLite 数据库：[license](https://www.sqlite.org/copyright.html)
- SDL / SDL_image（图形显示）：[license](crawl-ref/docs/license/lgpl.txt)
- libpng（图像加载）：[license](crawl-ref/docs/license/libpng-LICENSE.txt)

感谢你的关注，祝你每一局都有精彩瞬间，少一点“手滑送命”，多一点“绝境翻盘”。
