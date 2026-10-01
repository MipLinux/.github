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

**项目处于早期阶段，尚未对外发布。**

## 中文支持是五层，缺一层就是半成品

只装 `fcitx5` 不配 Wayland 环境变量，输入法不会出现；只换 Live 的镜像源，装完后第一次 `pacman -Syu` 就会退回官方源。MipLinux 要解决的就是这些层与层之间的接缝。

| 层面 | 装完 Arch 之后通常还要 | MipLinux 怎么做 | 当前状态 |
|---|---|---|---|
| 网络 | 换国内源，否则下载慢到不可用 | 默认国内源（清华 / 阿里 / 中科大等） | ✅ 装后系统继承国内源已实测；`reflector` 覆盖防线随 M4 落地（Issue #23） |
| 字体 | 装中文字体，手调 `fontconfig` 的 CJK fallback | 字体层默认配好，中英混排不乱字重 | 🚧 `noto-fonts-cjk` 在 Live 清单里，fallback 规则已实测生效；装后清单还没有字体包（P10） |
| 输入法 | 装输入法，处理 Wayland 环境变量与自启动 | `fcitx5` + RIME 默认可用 | 🚧 `fcitx5` 系的包在 Live 清单里，没有配置、没有自启动，装后清单也没有（P10） |
| 本地化 | 预生成 `zh_CN.UTF-8`、设时区、配键盘 | 本地化层默认到位 | ✅ `LANG=zh_CN.UTF-8` 已实测；键盘目前只有 `us` 生效（Issue #64） |
| 文档 | 遇到问题找不到中文资料 | 随系统提供中文上手文档 | ⬜ 未开始 |

## 进度

截至 **2026-10-01**。**「✅」= 在本机实测过**，不等于用户拿到的成品已经具备该能力。

<!-- BEGIN:progress-table -->
| 阶段 | 状态 |
|---|---|
| 构建环境与基线 | ✅ 未修改的 `releng` 构建出 ISO，QEMU（UEFI）引导到 `[root@archiso ~]#` |
| 自有 profile | ✅ `profile/` 进仓库并改名 MipLinux，产物 `miplinux-<日期>-x86_64.iso`（1.5 GiB，构建 2 分 08 秒） |
| 装系统链路 | ✅ 安装器 M0、M1 实测：空盘装出能启动的系统（检查点 4），装后 `pacman -Syu` 成功（检查点 6）；检查点 5 到配置层 |
| 国内源与中文本地化 | 🚧 国内源、`zh_CN.UTF-8`、CJK fallback、终端字体已并主线；装后系统的源继承、用户 / sudo、输入法环境变量已实测生效。CJK 字体与 `fcitx5` 的**包在 Live 清单里**，但**装后清单还没有**（[P10](https://github.com/MipLinux/MipLinux/blob/main/docs/knowledge/06-待定事项.md)）；`reflector` 防线随 M4（Issue #23） |
| NVIDIA 驱动 | 🚧 Live 清单已加 `nvidia-open` / `nvidia-utils`；真机第一次验证 ✅（09-22，RTX 5060 Max-Q，独显模式）：驱动加载、`nvidia-smi`、内屏点亮、`nmcli` 联网；装完重启后能用未做，由 M3 带 |
| 安装程序 | ✅ M0 / M1 完成，M2 验收通过：全部流程页已接入真实后端，QEMU 里全程图形化装完一次，检查点 4 通过；后端单测 239 全绿、接线烟测 44 项；技术栈见 D14 |
| 桌面环境 / 品牌化 | ⬜ 未开始。P5 已定不做 DE，niri / Hyprland 待真机各跑一轮 |
<!-- END:progress-table -->

## 还没定的事

| 编号 | 待定 |
|---|---|
| P5 | 桌面环境：**WM 路线已定**（不做 DE），niri / Hyprland 二选一 |
| P10 | 包清单的组织方式：**方向已明** —— 两份清单（Live 精简 / 装后更大）+ 安装器询问应用，怎么落地待定案 |
| P11 | 第三方仓库政策：`archlinuxcn` 现在以 `SigLevel = Optional TrustAll` 启用，对外发布前怎么收紧 |
| P12 | 时区名单与显示名的审定规则：tzdata 的地名本身带政治表述，「列出来的」与「我们写的」是两件事 |

## 参与

项目由**三位长期维护者**维护，三台机器的宿主发行版各不相同；分工写在项目仓库的 [Issues](https://github.com/MipLinux/MipLinux/issues?q=label%3Atask) 里 —— 一条工作 = 一个 issue。
对中文 Linux 桌面有想法，或愿意帮忙测 NVIDIA 硬件兼容性，欢迎提 Issue；动手前请先读 [CONTRIBUTING.md](https://github.com/MipLinux/.github/blob/main/CONTRIBUTING.md)。

安全漏洞走 [SECURITY.md](https://github.com/MipLinux/.github/blob/main/SECURITY.md) 的私下流程，不要在公开 Issue 里披露。

<details>
<summary><b>English</b></summary>

<br>

**MipLinux** is an Arch Linux-based rolling release for Chinese-speaking users. Two goals: the Chinese environment (mirrors, fonts, input method, locale, documentation) ships as the default instead of post-install chores, and NVIDIA drivers work out of the box via `nvidia-open` on the official `linux` kernel.

**Status:** early stage, no release yet. The project's own profile builds a bootable ISO. The first Chinese-environment layers — domestic mirrors, `zh_CN.UTF-8`, CJK font fallback rules, console settings — are merged, post-install mirror inheritance is verified (`pacman -Syu` succeeds), and `nvidia-open` in the live package list was verified once on real hardware. The installer's M0/M1 core is tested end to end (a blank disk becomes a bootable system in QEMU), and its Qt6 interface (M2) is wired to the real backend and accepted, driven headlessly through the whole flow in QEMU. Not implemented yet: the post-install half of the NVIDIA verification, the CJK-font and input-method packages in the installed system, desktop selection, and branding.

Built with `mkarchiso` inside a `systemd-nspawn` container running clean Arch; verified by booting in QEMU/KVM. Architecture: x86_64. Maintained by three long-term maintainers on three different host distributions.

</details>
