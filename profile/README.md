<div align="center">

<img src="assets/mipl-logo-mark.png" width="88" alt="MipLinux">

**一个面向中文用户的 Arch Linux 发行版**

滚动更新 · 中文开箱即用 · NVIDIA 驱动预装

[![平台](https://img.shields.io/badge/平台-x86__64-4a5568?style=flat-square)](https://github.com/MipLinux/MipLinux)
[![阶段](https://img.shields.io/badge/阶段-早期开发中-d97706?style=flat-square)](https://github.com/MipLinux/MipLinux/blob/main/docs/work/installer-roadmap.md)

</div>

MipLinux 基于 Arch Linux，滚动更新，装到硬盘后照常 `pacman -Syu`。两个目标：

1. **NVIDIA 驱动开箱可用** —— 官方 `linux` 内核配 `nvidia-open`，覆盖 Turing 及更新架构
2. **对中文用户友好** —— 国内源、`zh_CN.UTF-8`、CJK 字体规则、`fcitx5` 输入法都进默认配置

参照系是 [CachyOS](https://cachyos.org/)。它做得很好，但中文输入法、字体、国内镜像源都没有默认配置。

**项目处于早期阶段，尚未对外发布。** 想自己构建一次：项目仓库 README 的[上手](https://github.com/MipLinux/MipLinux#上手)一节（环境自检 → 构建 → QEMU 试装）。

## 中文支持是五层，缺一层就是半成品

只装 `fcitx5` 不配 Wayland 环境变量，输入法不会出现；只换 Live 的镜像源，装完后第一次 `pacman -Syu` 就会退回官方源。MipLinux 要解决的就是这些层与层之间的接缝。

| 层面 | 装完 Arch 之后通常还要 | MipLinux 怎么做 | 做到哪一层 |
|---|---|---|---|
| 网络 | 换国内源，否则下载慢到不可用 | 默认国内源（清华 / 阿里 / 中科大等） | 🚧 装后系统继承国内源已实测；安装器里的选源与测速随 M4 |
| 字体 | 装中文字体，手调 `fontconfig` 的 CJK fallback | 字体层默认配好，中英混排不乱字重 | 🚧 fallback 规则已实测；字体包已进装后清单，装后效果待重测（P10） |
| 输入法 | 装输入法，处理 Wayland 环境变量与自启动 | `fcitx5` + 中文输入方案（`fcitx5-chinese-addons`） | 🚧 环境变量已实测；包已进装后清单，`fcitx5` 的 profile 配置与自启动未做（P10） |
| 本地化 | 预生成 `zh_CN.UTF-8`、设时区、配键盘 | 本地化层默认到位 | ✅ `LANG=zh_CN.UTF-8`、键盘布局与时区已实测 |
| 文档 | 遇到问题找不到中文资料 | 随系统提供中文上手文档 | ⬜ 未开始 |

逐项的实测状态不在上表重复，见下面的进度表。

## 进度

截至 **2026-10-10**。**「✅」= 在本机实测过**，不等于用户拿到的成品已经具备该能力。

<!-- BEGIN:progress-table -->
| 阶段         | 状态          |
|------------|-------------|
| 构建环境与基线    | Bingo       |
| 自有 profile | Bingo       |
| 装系统链路      | Bingo       |
| 国内源与中文本地化  | Testing     |
| NVIDIA 驱动  | Testing     |
| 安装程序       | Testing     |
| 桌面环境 / 品牌化 | Coming Soon |
<!-- END:progress-table -->

## 还没定的事

| 编号 | 待定 |
|---|---|
| P5 | 桌面：**WM 路线已定**（不做完整桌面环境），niri / Hyprland 二选一 |
| P10 | 包清单的组织方式：**方向已明** —— 两份清单（Live 精简 / 装后更大）+ 安装器询问应用，细则待定案 |
| P11 | 第三方仓库政策：`archlinuxcn` 现在以 `SigLevel = Optional TrustAll` 启用，对外发布前怎么收紧 |
| P12 | 时区名单与显示名的审定规则：**规则已裁**，只差登记成决策编号（要维护者点头） |

背景、候选与已否决的方案见项目仓库的 [06-待定事项](https://github.com/MipLinux/MipLinux/blob/main/docs/knowledge/06-待定事项.md)。

## 参与

项目由长期维护者维护，各自机器的宿主发行版不同；分工写在项目仓库的 [Issues](https://github.com/MipLinux/MipLinux/issues?q=label%3Atask) 里 —— 一条工作 = 一个 issue。
对中文 Linux 桌面有想法，或愿意帮忙测 NVIDIA 硬件兼容性，欢迎提 Issue；动手前请先读 [CONTRIBUTING.md](https://github.com/MipLinux/.github/blob/main/CONTRIBUTING.md)。

安全漏洞走 [SECURITY.md](https://github.com/MipLinux/.github/blob/main/SECURITY.md) 的私下流程，不要在公开 Issue 里披露。

<details>
<summary><b>English</b></summary>

<br>

**MipLinux** is an Arch Linux-based rolling release for Chinese-speaking users. Two goals: the Chinese environment (mirrors, fonts, input method, locale, documentation) ships as the default instead of post-install chores, and NVIDIA drivers work out of the box via `nvidia-open` on the official `linux` kernel.

**Status:** early stage, no release yet. A bootable ISO is built from this project's own profile; domestic mirrors, `zh_CN.UTF-8`, CJK font fallback rules and the console font are merged, and the installed system inherits the mirrors (`pacman -Syu` succeeds). The installer's backend installs a bootable system from a blank disk in QEMU (checkpoint 4), and its Electron interface (12 pages) has been walked through in the live ISO — a second full walkthrough was reported but is not yet archived. `nvidia-open` was verified once on real hardware in the live environment. Still open: the installed-system half of the NVIDIA verification, the CJK-font and input-method packages' effect in the installed system, the desktop and branding, and the delay before the installer window appears.

Built with `mkarchiso` inside a `systemd-nspawn` container running clean Arch; verified by booting in QEMU/KVM. Architecture: x86_64. Maintained by long-term maintainers on different host distributions.

</details>
