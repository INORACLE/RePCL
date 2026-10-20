<div align="center">

# RePCL

**基于 Plain Craft Launcher 2 开源版二次构建的定制启动器**

[![Platform](https://img.shields.io/badge/platform-Windows-0078D4?logo=windows&logoColor=white)](https://github.com/INORACLE/RePCL)
[![.NET](https://img.shields.io/badge/.NET%20Framework-4.8-512BD4?logo=dotnet&logoColor=white)](https://dotnet.microsoft.com/)
[![Language](https://img.shields.io/badge/language-Visual%20Basic%20.NET-512BD4?logo=visualbasic&logoColor=white)](https://github.com/INORACLE/RePCL)
[![License](https://img.shields.io/badge/license-Custom-blue)](./PCL-main/LICENCE)

一个开箱即用、去除了联网限制、内置赞助特性并拥有柔和淡粉色外观的 Minecraft 启动器。

</div>

---

## 📖 简介

**RePCL** 以 [Plain Craft Launcher 2](https://github.com/Hex-Dragon/PCL2) 的开源版本为基础构建，在保留其全部核心功能的前提下，针对自用场景做了若干定制：解除 MC 下载限制、内置正版登录与 CurseForge 凭据、解锁全部赞助特性、内置背景图，并采用淡粉色主题。

> ⚠️ 本项目仅供学习交流，请勿用于商业用途。PCL 版权归原作者 **龙腾猫跃** 所有。

---

## ✨ 特性

| 特性 | 说明 |
| --- | --- |
| 🎨 **淡粉色主题** | 主界面采用柔和的淡粉色配色（色相 330°，低饱和度） |
| 🏷️ **RePCL 品牌** | 窗口标题与左上角标题栏默认显示 **RePCL** |
| 🔓 **解除 MC 下载限制** | 移除 `RestrictMcDownload` 限制，可正常下载 Minecraft |
| 🔑 **内置正版登录** | 内置微软登录 Client ID，支持正版账号登录 |
| 🧩 **内置 CurseForge** | 内置 CurseForge API Key，模组/整合包搜索下载可直接使用 |
| 💎 **赞助特性全解锁** | 主题切换、隐藏主题、快照提示等赞助功能全部开放 |
| 🖼️ **内置背景图** | 内置一张默认背景图，无需手动配置 |
| 🚫 **去除更新与遥测** | 断开自动更新与联网通知，去除匿名数据上报 |

---

## 🚀 快速开始

### 方式一：直接运行（推荐）

1. 前往本仓库的 [**Releases**](../../releases) 页面，下载最新版本的 `RePCL.exe`。
2. 将 `RePCL.exe` 放入任意**空文件夹**（建议避开系统盘根目录与受保护目录）。
3. 双击运行即可。

> 💡 首次启动需要联网以初始化部分资源。

### 方式二：从源码构建

**环境要求**

- Windows 10 / 11
- Visual Studio 2022（含 **.NET 桌面开发** 工作负载）
- .NET Framework 4.8 开发工具包
- .NET SDK（用于还原 NuGet 包）

**构建步骤**

```powershell
# 1. 还原 NuGet 依赖
dotnet restore "PCL-main/PCLCS/PCLCS.csproj"

# 2. 编译主项目（Release）
& "C:/Program Files/Microsoft Visual Studio/2022/Community/MSBuild/Current/Bin/MSBuild.exe" `
  "PCL-main/Plain Craft Launcher 2/Plain Craft Launcher 2.vbproj" `
  -p:Configuration=Release -m

# 3. 生成物位于
# PCL-main/Plain Craft Launcher 2/bin/Plain Craft Launcher 2.exe
```

---

## 🧾 相对原版的改动

主要改动集中在 `PCL-main/Plain Craft Launcher 2/Modules/ModSecret.vb` 等文件：

| 文件 | 改动 |
| --- | --- |
| `Modules/ModSecret.vb` | `RestrictMcDownload = False`；解除下载限制 |
| `Modules/ModSecret.vb` | 内置 `OAuthClientId`（微软登录） |
| `Modules/ModSecret.vb` | 内置 `CurseForgeAPIKey` |
| `Modules/ModSecret.vb` | `CurrentRank` 返回 `Rank98`，解锁赞助功能 |
| `Modules/ModSecret.vb` | 默认配色改为淡粉色（`ColorHue=330`, `ColorSat=35`） |
| `Modules/ModSecret.vb` | `VersionBranchMain = "RePCL"` |
| `FormMain.xaml` | 窗口标题改为 **RePCL** |
| `Pages/PageSetup/Settings.vb` | 标题栏默认文本模式，显示 **RePCL** |
| `Pages/PageSetup/PageSetupUI.xaml.vb` | 无自定义背景时载入内置背景图 |
| `Images/Background.jpg` | 新增内置背景图资源 |

---

## 📂 项目结构

```
RePCL/
├── RePCL.exe                     # 已编译的可执行文件
├── PCL-main/                     # 源码根目录
│   ├── Plain Craft Launcher 2/   # 启动器主项目（VB.NET / WPF）
│   │   ├── Modules/              # 核心模块（含 ModSecret.vb）
│   │   ├── Pages/                # 各功能页面
│   │   ├── Images/               # 图片资源（含内置背景图）
│   │   └── Plain Craft Launcher 2.vbproj
│   ├── PCLCS/                    # 公共类库（C#）
│   ├── MeloongCore/              # 底层核心依赖
│   └── Plain Craft Launcher 2.sln
└── README.md
```

---

## ❓ 常见问题

<details>
<summary><b>启动时提示找不到 .NET Framework 4.8 怎么办？</b></summary>

请安装 [.NET Framework 4.8 运行时](https://dotnet.microsoft.com/download/dotnet-framework/net48) 后重试。

</details>

<details>
<summary><b>正版登录 / CurseForge 无法使用？</b></summary>

RePCL 已内置凭据。若仍失败，通常是网络问题，请检查代理或系统时间是否准确。

</details>

<details>
<summary><b>如何自定义背景图？</b></summary>

把图片放入启动器同目录下的 `PCL\Pictures\` 文件夹即可，启动器会自动随机选用；若该文件夹为空，则使用内置背景图。

</details>

---

## ⚖️ 免责声明

- 本项目基于 **Plain Craft Launcher 2** 开源版构建，PCL 的著作权归原作者 **龙腾猫跃** 所有。
- 本项目为**个人学习与自用**目的的非官方分支，与原作者无任何关联。
- 请遵循原项目 [LICENCE](./PCL-main/LICENCE) 的相关规定，**不得用于任何商业用途**。
- 使用本项目产生的一切后果由使用者自行承担。

---

<div align="center">

**RePCL** · Made with ❤️ based on Plain Craft Launcher 2

</div>
