# MipLinux/.github

这个仓库**不含任何功能代码**。它是 MipLinux 组织的公共门面与共享约定；**项目本体在
[MipLinux/MipLinux](https://github.com/MipLinux/MipLinux)** —— 构建配置、安装器源码与全部技术文档都在那边。

组织主页显示的内容来自 [`profile/README.md`](profile/README.md)。

---

## 这里放什么

| 路径 | 作用 |
|---|---|
| [`profile/README.md`](profile/README.md) | 组织主页本体 —— 在 <https://github.com/MipLinux> 展示 |
| [`profile/assets/`](profile/assets/) | 组织主页用的图片（logo 等） |
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | 协作约定：环境、工作流、文档规范、报告问题的去处 |
| [`SECURITY.md`](SECURITY.md) | 安全问题的私下报告通道与当前安全模型 |
| [`ISSUE_TEMPLATE/`](ISSUE_TEMPLATE/) | 组织级 Issue 模板（位置有硬要求，见下） |

## 这里不放什么

项目的**构建配置、安装器源码与全部技术文档**都在项目仓库里，不在这里：怎么构建、怎么验证、哪些决策已经定了、哪些还没定，都以 [MipLinux/MipLinux](https://github.com/MipLinux/MipLinux) 为准。

组织主页描述的是**已经定下来的技术决策与实现路径，不是已交付的功能** —— 项目尚未对外发布。主页上的「✅」只表示维护者在本机实测过；逐项状态以项目仓库 README 的[进度表](https://github.com/MipLinux/MipLinux#当前进度)为真源。

---

## 组织级文件是怎么生效的

GitHub 按以下顺序查找社区健康文件（[官方文档](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file)）：

1. 仓库自己的 `.github/` 目录
2. 仓库根目录
3. **本仓库**（名字必须是 `.github`，且必须是公开仓库）

也就是说，这里的文件是**兜底默认值**：没有自带 `CONTRIBUTING.md` / `SECURITY.md` 的仓库会自动使用这里的版本，自带一份则覆盖它。反过来说，改这里的文件会影响整个组织下的所有仓库。

### Issue 模板：位置有硬要求，本项目走副本路线

- **位置** —— 组织级默认的 Issue 模板要放在本仓库的 `.github/ISSUE_TEMPLATE/` 下。本仓库目前放在根目录的 `ISSUE_TEMPLATE/`，项目仓库实测继承不到（New issue 选择页空白）。
- **文件名必须是 ASCII** —— GitHub 不识别中文文件名，例如 `bug-报告.md` 不会被加载。模板正文可以用中文，文件名不行。

所以**项目仓库各自保留一份副本**（副本头三行写明来历），并由项目仓库的 `scripts/check-doc-sync.sh` 逐字比对两边，漂了就报错。
**改模板先改这里，再同步副本**；只改副本会被守卫拦下。

---

## 组织主页的进度表是生成物

组织主页的进度表与项目仓库 README 的进度表**逐行同形**（同阶段名、同状态）。唯一允许的差异是链接形态 ——
主页是另一个仓库，仓库内相对链接点了会 404，必须写成指向项目仓库的绝对链接。

- **真源是项目仓库的 `README.md`**：要改进度，先改它。
- 项目仓库的 `scripts/sync-profile-progress.sh` 把真源同步到这里：只动两张表之间的那一块，写完自跑守卫，不通过就回滚。
- 项目仓库的 `scripts/check-doc-sync.sh` 断言两边一致，并挡住已被推翻、不许再写回来的旧口径。

**不要手改这里进度表的那一块** —— 改了守卫会报出来。

---

## 修改流程

- 这个仓库是组织门面，改动会直接对外可见；描述尚未实现的功能时，明确标注它还没实现。
- 改「现状」「路线图」这类会过期的内容前，先对照项目仓库的 `docs/` 与 README 的进度表；两处冲突时以项目仓库为准。
- 两份仓库并列检出时，改完在项目仓库里跑这两条，都过再提交：
  `./scripts/check-readme-links.sh`（链接、锚点、进度表标记）、
  `./scripts/check-doc-sync.sh`（进度口径与模板副本；本仓库不在并列位置时加 `--org <本仓库路径>`）。

细节见 [CONTRIBUTING.md](CONTRIBUTING.md)。
