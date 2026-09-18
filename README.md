# MipLinux/.github

这个仓库**不含任何功能代码**。它是 MipLinux 组织的公共门面与共享约定。

组织主页显示的内容来自 [`profile/README.md`](profile/README.md)。

---

## 这里放什么

| 路径 | 作用 |
|---|---|
| [`profile/README.md`](profile/README.md) | 组织主页本体 —— 在 <https://github.com/MipLinux> 展示 |
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | 协作约定：环境、工作流、文档规范 |
| [`SECURITY.md`](SECURITY.md) | 安全问题的私下报告通道与当前安全模型 |
| [`ISSUE_TEMPLATE/`](ISSUE_TEMPLATE/) | 组织级 Issue 模板 |

## 这里不放什么

项目的**主体代码、构建配置与全部技术文档**在单独的项目仓库中，不在这里。

这个组织目前是一个半可见的私人组织，项目尚未对外发布。组织主页描述的是已经定下来的技术决策与实现路径 —— **不是已交付的功能**。

---

## 组织级文件是怎么生效的

GitHub 会按以下顺序查找社区健康文件：

1. 仓库自己的 `.github/` 目录
2. 仓库根目录
3. **本仓库**（`.github` 仓库）

也就是说，这里的文件是**兜底默认值**：任何没有自带 `CONTRIBUTING.md`、`SECURITY.md` 或 Issue 模板的仓库，都会自动使用这里的版本。仓库自己放一份则可以覆盖它。

因此修改本仓库的文件会影响整个组织下的所有仓库 —— 改之前请注意这一点。

> **命名限制：** Issue 模板的文件名必须是 ASCII。GitHub 不识别中文文件名，
> 例如 `bug-报告.md` 不会被加载。模板正文可以用中文，文件名不行。

---

## 修改流程

这个仓库是组织门面，改动会直接对外可见。

- 组织主页的描述、决策与路线图，必须与项目仓库中的实际状态一致
- 改「现状」「路线图」这类会过期的内容时，请一并核对项目仓库的 `docs/`
- 描述尚未实现的功能时，明确标注它还没实现

细节见 [CONTRIBUTING.md](CONTRIBUTING.md)。
