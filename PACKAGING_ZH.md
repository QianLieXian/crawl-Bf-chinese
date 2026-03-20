# 打包教程（中文）

本文档用于本仓库的汉化版本构建与打包。每次更新翻译文本后，都建议按下列步骤重新构建并验证。

## 1. 环境准备

- Linux（推荐 Ubuntu 22.04+）
- `git`
- `g++` / `clang++`
- `make`
- `pkg-config`
- `python3`
- SDL2 相关依赖（图形版需要）

可先阅读官方构建说明：`crawl-ref/INSTALL.md`。

## 2. 构建（Tiles 图形版）

```bash
cd crawl-ref/source
make -j"$(nproc)" TILES=y
```

构建产物通常位于：

- `crawl-ref/source/crawl`（可执行文件）
- 以及同目录下相关资源输出

## 3. 构建（控制台版）

```bash
cd crawl-ref/source
make -j"$(nproc)"
```

## 4. 翻译文本检查

每次合入新的中文文本后，至少检查以下目录中的文件是否存在并可正常读取：

- `crawl-ref/source/dat/database/zh/`
- `crawl-ref/source/dat/descript/zh/`

建议启动游戏并重点检查：

- 怪物名称与称号
- 战斗相关提示与状态描述
- 场景/分支说明
- UI 菜单和帮助文本
- 属性、技能、职业与种族描述

## 5. 打包建议

### 本地归档（快速分发）

```bash
cd crawl-ref
mkdir -p ../dist
# 仅示例：将 source 与 dat 目录按需归档
# 可按你的发布策略增减内容
tar -czf ../dist/dcss-ai-chinese-linux.tar.gz source
```

### 正式发布

如需制作系统级安装包（deb、AppImage、Windows 包等），请参考：

- `crawl-ref/docs/develop/release/`
- `crawl-ref/INSTALL.md`

## 6. 常见问题

- **出现英文回退文本**：优先检查对应 key 是否已在 `zh` 目录补齐。
- **启动后文本乱码**：确认文件为 UTF-8 编码。
- **构建失败**：先执行 `make clean` 后重试，并核对依赖版本。
