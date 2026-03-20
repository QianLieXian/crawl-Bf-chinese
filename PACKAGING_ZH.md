# 打包教程（中文）

本文档用于本仓库汉化版本的构建与打包。每次更新翻译文本后，建议按下列步骤重新构建并验证。

## 1. 环境准备

### Linux（推荐 Ubuntu 22.04+）

- `git`
- `g++` / `clang++`
- `make`
- `pkg-config`
- `python3`
- SDL2 相关依赖（图形版需要）

### Windows 10（推荐 MSYS2 MinGW64）

- 安装 [MSYS2](https://www.msys2.org/)
- 使用 **MSYS2 MinGW 64-bit** 终端
- 安装基础依赖（示例）：

```bash
pacman -Syu
pacman -S --needed \
  git \
  make \
  mingw-w64-x86_64-gcc \
  mingw-w64-x86_64-python \
  mingw-w64-x86_64-SDL2 \
  mingw-w64-x86_64-SDL2_image
```

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

## 4. Windows 10 打包建议

在 Windows 10 上，建议按“可执行文件 + 必要资源目录 + 运行依赖 DLL”进行最小可运行打包。

### 建议包含

- 游戏可执行文件（例如 `crawl.exe` 或对应构建产物）
- `dat/` 等运行期资源目录（按实际构建产物校验）
- MSYS2/MinGW 运行所需 DLL（如 `libstdc++-6.dll`、`libgcc_s_seh-1.dll`、`SDL2.dll` 等，具体以 `ldd` 结果为准）

### 依赖检查（示例）

```bash
cd crawl-ref/source
ldd crawl.exe
```

### 分发形式建议

- 内部测试：ZIP 压缩包（便于快速迭代）
- 对外发布：附带版本号与更新说明（可选再加校验值）

## 5. 翻译文本检查

每次合入新的中文文本后，至少检查以下目录中的文件是否存在并可正常读取：

- `crawl-ref/source/dat/database/zh/`
- `crawl-ref/source/dat/descript/zh/`

建议启动游戏并重点检查：

- 怪物名称与称号
- 战斗相关提示与状态描述
- 场景/分支说明
- UI 菜单和帮助文本
- 属性、技能、职业与种族描述

## 6. 本地归档（快速分发）

```bash
cd crawl-ref
mkdir -p ../dist
# 仅示例：将 source 目录按需归档
# 可按你的发布策略增减内容
tar -czf ../dist/dcss-ai-chinese-linux.tar.gz source
```

Windows 下可改为：

- 使用资源管理器右键压缩为 ZIP；
- 或在 MSYS2 中执行：

```bash
cd crawl-ref
mkdir -p ../dist
zip -r ../dist/dcss-ai-chinese-windows10.zip source
```

## 7. 正式发布

如需制作系统级安装包（deb、AppImage、Windows 包等），请参考：

- `crawl-ref/docs/develop/release/`
- `crawl-ref/INSTALL.md`

## 8. 常见问题

- **出现英文回退文本**：优先检查对应 key 是否已在 `zh` 目录补齐。
- **启动后文本乱码**：确认文件为 UTF-8 编码。
- **构建失败**：先执行 `make clean` 后重试，并核对依赖版本。
- **Windows 10 启动缺少 DLL**：根据 `ldd crawl.exe` 输出补齐依赖，避免只拷贝 exe。
