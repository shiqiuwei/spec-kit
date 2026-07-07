# Spec Kit 中文说明

<div align="center">
    <img src="./media/logo_large.webp" alt="Spec Kit Logo" width="200" height="200"/>
    <h1>🌱 Spec Kit</h1>
    <h3><em>更快构建高质量软件。</em></h3>
</div>

<p align="center">
    <strong>一个开源工具包，帮助你把注意力放在产品场景和可预测的结果上，而不是从零开始为每一个部分进行 vibe coding。</strong>
</p>

<p align="center">
    <a href="https://github.com/github/spec-kit/releases/latest"><img src="https://img.shields.io/github/v/release/github/spec-kit" alt="Latest Release"/></a>
    <a href="https://github.com/github/spec-kit/stargazers"><img src="https://img.shields.io/github/stars/github/spec-kit?style=social" alt="GitHub stars"/></a>
    <a href="https://github.com/github/spec-kit/blob/main/LICENSE"><img src="https://img.shields.io/github/license/github/spec-kit" alt="License"/></a>
    <a href="https://github.github.io/spec-kit/"><img src="https://img.shields.io/badge/docs-GitHub_Pages-blue" alt="Documentation"/></a>
</p>

<p align="center">
    English | <a href="./README.zh-CN.md">中文</a>
</p>

---

## 目录

- [🤔 什么是 Spec-Driven Development？](#-什么是-spec-driven-development)
- [⚡ 快速开始](#-快速开始)
- [📽️ 视频概览](#️-视频概览)
- [🌍 社区](#-社区)
- [🤖 支持的 AI 编码代理集成](#-支持的-ai-编码代理集成)
- [🔧 Specify CLI 参考](#-specify-cli-参考)
- [🧩 让 Spec Kit 适配你的需求：Extensions 与 Presets](#-让-spec-kit-适配你的需求extensions-与-presets)
- [📦 Bundles：基于角色的配置方案](#-bundles基于角色的配置方案)
- [📚 核心理念](#-核心理念)
- [🌟 开发阶段](#-开发阶段)
- [🎯 实验目标](#-实验目标)
- [🔧 运行前提](#-运行前提)
- [📖 了解更多](#-了解更多)
- [📋 详细流程](#-详细流程)
- [💬 支持](#-支持)
- [🙏 致谢](#-致谢)
- [📄 许可证](#-许可证)

## 🤔 什么是 Spec-Driven Development？

Spec-Driven Development（规格驱动开发）**颠覆了**传统的软件开发方式。几十年来，代码一直是主角——规格说明只是我们搭建起来、又在“真正工作”开始后丢弃的脚手架。

但在 AI 时代，这种模式已经不再适用。

当 AI 编码代理能够直接根据自然语言实现软件时，规格不再是可丢弃的规划文档，而是决定最终产物的 **事实来源（source of truth）**。Spec-Driven Development 的关键思想是：

与其让 AI 代理从一次性提示直接生成代码，不如引导它遵循一个有纪律的流程：

1. 定义项目的治理原则
2. 明确要构建什么以及为什么要构建
3. 创建包含架构与技术决策的实现计划
4. 将计划拆解为任务
5. 让编码代理在完整上下文中执行实现

这使 AI 生成的软件更加可预测、可审查，并且更符合你的目标。

## ⚡ 快速开始

### 1. 安装 Specify CLI

需要先安装 **[uv](https://docs.astral.sh/uv/)**（[安装 uv](./docs/install/uv.md)）。请将 `vX.Y.Z` 替换为 [Releases](https://github.com/github/spec-kit/releases) 中的最新标签：

```bash
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git@vX.Y.Z
```

如需替代安装方式、验证、升级和故障排查，请参阅 [安装指南](./docs/installation.md)。

### 2. 初始化项目

```bash
specify init my-project --integration copilot
cd my-project
```

如需检查更新或升级已安装的 CLI，请使用自管理命令。详细场景和自定义选项请参阅 [升级指南](./docs/upgrade.md)。

```bash
# 检查是否有更新版本可用（只读，不会修改任何内容）
specify self check

# 预览升级时会执行什么，但不真正升级
specify self upgrade --dry-run

# 直接升级到最新稳定版本（会自动识别 uv tool 或 pipx 安装方式）
specify self upgrade

# 或固定到某个特定发布标签（将 vX.Y.Z[suffix] 替换为目标标签）
specify self upgrade --tag vX.Y.Z[suffix]
```

直接执行 `specify self upgrade` 会立即生效，这种行为与 `pip install -U` 和 `npm update` 等无提示命令一致。对于 `uv tool` 安装，它会运行 `uv tool install specify-cli ...`。

### 3. 建立项目原则

在项目目录中启动你的编码代理。大多数代理会把 spec-kit 暴露为 `/speckit.*` 斜杠命令；Codex CLI 的 skills 模式则使用 `$speckit-*`；GitHub Copilot CLI 使用 `/agents/...` 风格的命令。

使用 **`/speckit.constitution`** 命令来创建项目的治理原则和开发指南，这些内容会指导后续所有开发工作。

```bash
/speckit.constitution Create principles focused on code quality, testing standards, user experience consistency, and performance requirements
```

### 4. 创建规格说明

使用 **`/speckit.specify`** 命令描述你想构建的内容。重点关注 **是什么** 和 **为什么**，而不是技术栈。

```bash
/speckit.specify Build an application that can help me organize my photos in separate photo albums. Albums are grouped by date and can be re-organized by dragging and dropping on the main page. Albums should support custom titles and tags.
```

### 5. 创建技术实现计划

使用 **`/speckit.plan`** 命令提供你的技术栈和架构选择。

```bash
/speckit.plan The application uses Vite with minimal number of libraries. Use vanilla HTML, CSS, and JavaScript as much as possible. Images are not uploaded anywhere and metadata is stored in a local database.
```

### 6. 拆解为任务

使用 **`/speckit.tasks`** 从实现计划中生成可执行的任务清单。

```bash
/speckit.tasks
```

### 7. 执行实现

使用 **`/speckit.implement`** 按照计划执行所有任务并构建你的功能。

```bash
/speckit.implement
```

如需更详细的逐步说明，请查看我们的 [完整指南](./spec-driven.md)。

## 📽️ 视频概览

想看看 Spec Kit 的实际效果？观看我们的 [视频概览](https://www.youtube.com/watch?v=a9eR1xsfvHg&pp=0gcJCckJAYcqIYzv)！

[![Spec Kit video header](/media/spec-kit-video-header.jpg)](https://www.youtube.com/watch?v=a9eR1xsfvHg&pp=0gcJCckJAYcqIYzv)

## 🌍 社区

欢迎在 [Spec Kit 文档站点](https://github.github.io/spec-kit/) 上浏览社区贡献的资源：

- [Extensions](https://github.github.io/spec-kit/community/extensions.html) —— 命令、钩子和能力扩展
- [Presets](https://github.github.io/spec-kit/community/presets.html) —— 模板和术语覆盖
- [Bundles](https://github.github.io/spec-kit/community/bundles.html) —— 由现有组件组合而成的角色与团队配置
- [Walkthroughs](https://github.github.io/spec-kit/community/walkthroughs.html) —— 端到端 SDD 场景
- [Friends](https://github.github.io/spec-kit/community/friends.html) —— 基于或扩展 Spec Kit 的项目

> [!NOTE]
> 社区贡献内容由各自作者独立创建和维护。安装前请审查源代码，并自行决定是否使用。

想要贡献？请查看 [Extension Publishing Guide](extensions/EXTENSION-PUBLISHING-GUIDE.md)、[Presets Publishing Guide](presets/PUBLISHING.md)，或 [Community Bundles 指南](docs/community-bundles.md)。

## 🤖 支持的 AI 编码代理集成

Spec Kit 可与 30+ 种 AI 编码代理协作——既支持 CLI 工具，也支持基于 IDE 的助手。完整列表、说明和使用细节请查看 [Supported AI Coding Agent Integrations](https://github.github.io/spec-kit/reference/integrations.html)。

运行 `specify integration list` 查看你当前安装版本中可用的全部集成。

## 可用的斜杠命令

在运行 `specify init` 之后，你的 AI 编码代理将获得以下用于结构化开发的斜杠命令。对于支持 skills 模式的集成，传入 `--integration <agent> --skills` 时会生成相应的 skill 目录；其他集成则使用标准命令文件。

### 核心命令

适用于 Spec-Driven Development 工作流的核心命令：

| 命令 | Agent Skill | 说明 |
| --- | --- | --- |
| `/speckit.constitution` | `speckit-constitution` | 创建或更新项目治理原则和开发指南 |
| `/speckit.specify` | `speckit-specify` | 定义你要构建什么（需求和用户故事） |
| `/speckit.plan` | `speckit-plan` | 根据你选择的技术栈创建技术实现计划 |
| `/speckit.tasks` | `speckit-tasks` | 生成可执行的实现任务列表 |
| `/speckit.taskstoissues` | `speckit-taskstoissues` | 将生成的任务列表转换为 GitHub Issues 以便跟踪和执行 |
| `/speckit.implement` | `speckit-implement` | 按照计划执行全部任务并构建功能 |
| `/speckit.converge` | `speckit-converge` | 根据规格/计划/任务评估代码库，并把剩余工作补充为新的任务 |

### 可选命令

用于增强质量和验证的附加命令：

| 命令 | Agent Skill | 说明 |
| --- | --- | --- |
| `/speckit.clarify` | `speckit-clarify` | 澄清描述不够明确的部分（建议在 `/speckit.plan` 前使用；此前名为 `/quizme`） |
| `/speckit.analyze` | `speckit-analyze` | 跨制品一致性与覆盖率分析（在 `/speckit.tasks` 之后、`/speckit.implement` 之前运行） |
| `/speckit.checklist` | `speckit-checklist` | 生成自定义质量检查清单，用于验证需求完整性、清晰度和一致性（相当于“英文版单元测试”） |

## 🔧 Specify CLI 参考

有关完整命令细节、选项和示例，请参阅 [CLI Reference](https://github.github.io/spec-kit/reference/overview.html)。

## 🧩 让 Spec Kit 适配你的需求：Extensions 与 Presets

Spec Kit 可以通过两个互补系统来适配你的需求——**extensions** 和 **presets**——再加上项目级覆盖配置来处理一次性的调整：

| 优先级 | 组件类型 | 位置 |
| ---: | --- | --- |
| 1 | Project-Local Overrides | `.specify/templates/overrides/` |
| 2 | Presets — Customize core & extensions | `.specify/presets/templates/` |
| 3 | Extensions — Add new capabilities | `.specify/extensions/templates/` |
| 4 | Spec Kit Core — Built-in SDD commands & templates | `.specify/templates/` |

- **模板** 在 **运行时** 解析——Spec Kit 会自上而下遍历层级，并使用第一个匹配项。
- 项目级覆盖（`.specify/templates/overrides/`）允许你针对单个项目做一次性调整，而无需创建完整 preset。
- **扩展/预设命令** 在 **安装时** 应用——当你运行 `specify extension add` 或 `specify preset add` 时，命令文件会被写入代理目录（例如 `.claude/...`）。
- 如果多个 presets 或 extensions 提供了同一个命令，则优先级最高的版本生效。删除后，会自动恢复次高优先级版本。
- 如果不存在覆盖或定制，Spec Kit 会使用其核心默认配置。

### Extensions —— 添加新能力

当你需要超出 Spec Kit 核心能力的功能时，请使用 **extensions**。扩展会引入新的命令和模板——例如添加领域特定工作流、与外部系统集成，或执行额外的验证步骤。

```bash
# 搜索可用扩展
specify extension search

# 安装扩展
specify extension add <extension-name>
```

例如，扩展可以添加 Jira 集成、实现后代码评审、V-Model 测试追踪，或项目健康诊断。

完整命令指南请参阅 [Extensions reference](https://github.github.io/spec-kit/reference/extensions.html)。浏览 [community extensions](https://github.github.io/spec-kit/community/extensions.html) 了解社区提供的扩展。

### Presets —— 定制现有工作流

当你希望改变 Spec Kit 的工作方式，但不增加新能力时，请使用 **presets**。Presets 会覆盖核心以及已安装扩展中提供的模板和命令，从而调整工作流程本身。

```bash
# 搜索可用 presets
specify preset search

# 安装 preset
specify preset add <preset-name>
```

例如，presets 可以重构规格模板以要求符合法规可追踪性，或将工作流适配为你使用的方法论（如 Agile、Kanban、Waterfall、jobs-to-be-done，或领域驱动设计等）。

完整命令指南（包括解析顺序和优先级叠加）请参阅 [Presets reference](https://github.github.io/spec-kit/reference/presets.html)。

## 📦 Bundles：基于角色的配置方案

Extensions 和 presets 是单独的构建块。**Bundle** 会把一组精选组件——扩展、预设、步骤和工作流——打包成一个单一、版本化、面向角色的配置方案（例如产品经理、业务分析师、安全研究员或开发者）。

Bundle 通过手写的 `bundle.yml` 清单文件描述。它会为每个组件指定版本，并且可以选择绑定到某个特定集成；不指定 `integration` 的 bundle 是 **与集成无关的（agnostic）**。

```bash
# 在当前目录的目录栈中发现 bundles
specify bundle search [<query>]

# 查看某个 bundle 将添加的确切组件集合（与 install 的结果一致）
specify bundle info <bundle-id>

# 一次性安装 bundle 的完整组件集合
specify bundle install <bundle-id>

# 查看已安装内容，然后以非破坏方式更新或移除
specify bundle list
specify bundle update <bundle-id>     # 或 --all
specify bundle remove <bundle-id>     # 仅移除此 bundle 安装的组件
```

Bundle 会从一个 **按优先级排序的目录栈** 中解析（项目 > 用户 > 内置）。每个来源都带有安装策略：`install-allowed` 来源可安装，而 `discovery-only` 来源仅供发现。

作者在本地验证并打包 bundle。分发方式是托管构建产物并添加一个目录源；社区 bundle 提交使用 [Bundle Submission](https://github.com/github/spec-kit/issues/new?template=bundle_submission.yml) 流程。

```bash
specify bundle validate --path ./my-bundle      # 结构与引用检查
specify bundle build --path ./my-bundle         # 生成版本化 .zip 产物
```

[`examples/bundles/`](examples/bundles/) 下有四个可直接阅读的示例清单（产品经理、业务分析师、安全研究员、开发者）。

关键保证：`info` 展示的内容与 `install` 实际添加的内容完全一致（透明可见）；安装是幂等的，并且仅限于项目根目录；`remove` 不会触及仍被其他已安装 bundle 使用的组件。

### 何时使用哪一种

| 目标 | 使用 |
| --- | --- |
| 添加全新的命令或工作流 | Extension |
| 自定义规格、计划或任务的格式 | Preset |
| 集成外部工具或服务 | Extension |
| 强制执行组织或监管标准 | Preset |
| 发布可复用的领域特定模板 | 任选其一——presets 适合模板覆盖，extensions 适合与新命令一起打包模板 |
| 一条命令配置完整的角色方案 | Bundle |

## 📚 核心理念

Spec-Driven Development 是一个结构化流程，强调：

- **以意图驱动开发**：先用规格定义 *是什么*，再决定 *怎么做*
- **创建丰富的规格**：借助约束和组织原则来提升规格质量
- **多步骤细化**：避免只靠一次提示直接生成代码
- **高度依赖**：依赖先进 AI 模型对规格的理解能力

## 🌟 开发阶段

| 阶段 | 重点 | 关键活动 |
| --- | --- | --- |
| **0 到 1 开发**（“Greenfield”） | 从零生成 | 从高层需求开始，生成规格，规划实现步骤，构建并迭代完善 |
| **创意探索** | 并行实现方案 | 探索多种解决方案，支持不同技术栈与架构，尝试不同 UX 模式 |
| **迭代增强**（“Brownfield”） | 存量系统现代化 | 逐步添加功能，现代化遗留系统，适配现有流程 |

对于已有项目，请将 Spec Kit 工具更新与功能制品演进分开处理：升级时刷新受管理的项目文件，在预期行为变更时更新 `specs/` 制品。

## 🎯 实验目标

我们的研究与实验重点在于：

### 技术无关性

- 使用多种技术栈创建应用
- 验证 Spec-Driven Development 是一种不绑定特定技术、编程语言或框架的流程

### 企业约束

- 展示关键业务应用的开发方式
- 纳入组织级约束（云提供商、技术栈、工程实践）
- 支持企业设计系统和合规要求

### 以用户为中心的开发

- 为不同用户群体和偏好构建应用
- 支持多种开发方式（从 vibe-coding 到 AI-native development）

### 创意与迭代过程

- 验证并行探索实现方案的概念
- 提供健壮的迭代式功能开发工作流
- 扩展流程以处理升级和现代化任务

## 🔧 运行前提

- **Linux/macOS/Windows**
- [支持的](#-支持的-ai-编码代理集成) AI 编码代理
- 用于包管理的 [uv](https://docs.astral.sh/uv/)（推荐）或用于持久安装的 [pipx](https://pipx.pypa.io/)
- [Python 3.11+](https://www.python.org/downloads/)
- [Git](https://git-scm.com/downloads)

如果你在使用某个代理时遇到问题，请提交 issue，以便我们改进集成。

## 📖 了解更多

- **[完整的 Spec-Driven Development 方法论](./spec-driven.md)** —— 对完整流程的深入讲解
- **[详细演练](#-详细流程)** —— 分步骤实施指南

---

## 📋 详细流程

<details>
<summary>点击展开详细的逐步演练</summary>

你可以使用 Specify CLI 来引导项目初始化，它会在你的环境中带入所需制品。运行：

```bash
specify init <project_name>
```

或者在当前目录中初始化：

```bash
specify init .
# 或使用 --here 标志
specify init --here
# 当目录已有文件时跳过确认
specify init . --force
# 或
specify init --here --force
```

![Specify CLI 在终端中引导新项目](./media/specify_cli.gif)

在交互式终端中，你会被提示选择正在使用的编码代理集成。在 CI 或管道式运行等非交互式会话中，`specify init` 默认使用 GitHub Copilot 集成。

```bash
specify init <project_name> --integration copilot
specify init <project_name> --integration gemini
specify init <project_name> --integration codex

# 或在当前目录中：
specify init . --integration copilot
specify init . --integration codex --integration-options="--skills"

# 或使用 --here 标志
specify init --here --integration copilot
specify init --here --integration codex --integration-options="--skills"

# 将内容强制合并到一个非空的当前目录
specify init . --force --integration copilot

# 或
specify init --here --force --integration copilot
```

CLI 会检查你所选代理所需的 CLI 工具是否已安装（对于需要 CLI 的集成），例如 Claude Code、Gemini CLI、Qwen Code、opencode、Codex CLI、Qoder CLI、Tabnine CLI 等。

```bash
specify init <project_name> --integration copilot --ignore-agent-tools
```

### **步骤 1：** 建立项目原则

进入项目文件夹并运行你的编码代理。在我们的示例中使用的是 `claude`。

![Bootstrapping Claude Code environment](./media/bootstrap-claude-code.gif)

如果你能看到 `/speckit.constitution`、`/speckit.specify`、`/speckit.plan`、`/speckit.tasks` 和 `/speckit.implement` 命令，说明配置正确。

第一步应该是使用 `/speckit.constitution` 命令建立项目的治理原则。这有助于在后续所有开发过程中保持一致的决策。

```text
/speckit.constitution Create principles focused on code quality, testing standards, user experience consistency, and performance requirements. Include governance for how these principles should guide tradeoffs.
```

这一步会创建或更新 `.specify/memory/constitution.md` 文件，其中包含项目的基础准则，编码代理会在规格、规划和实现过程中引用这些内容。

### **步骤 2：** 创建项目规格

在建立项目原则之后，你就可以创建功能规格了。使用 `/speckit.specify` 命令，然后提供你要构建的项目的具体需求。

> [!IMPORTANT]
> 尽可能明确地描述你要构建什么以及为什么要构建。**此时不要关注技术栈**。

示例提示词：

```text
Develop Taskify, a team productivity platform. It should allow users to create projects, add team members, assign tasks, comment and move tasks between boards in Kanban style. In this initial phase for this feature, let's call it "Create Taskify," let's have multiple users but the users will be declared ahead of time, predefined. I want five users in two different categories, one product manager and four engineers. Let's create three different sample projects. Let's have the standard Kanban columns for the status of each task, such as "To Do," "In Progress," "In Review," and "Done." There will be no login for this application as this is just the very first testing thing to ensure that our basic features are set up. For each task in the UI for a task card, you should be able to change the current status of the task between the different columns in the Kanban work board. You should be able to leave an unlimited number of comments for a particular card. You should be able to, from that task card, assign one of the valid users. When you first launch Taskify, it's going to give you a list of the five users to pick from. There will be no password required. When you click on a user, you go into the main view, which displays the list of projects. When you click on a project, you open the Kanban board for that project. You're going to see the columns. You'll be able to drag and drop cards back and forth between different columns. You will see any cards that are assigned to you, the currently logged in user, in a different color from all the other ones, so you can quickly see yours. You can edit any comments that you make, but you can't edit comments that other people made. You can delete any comments that you made, but you can't delete comments anybody else made.
```

输入该提示后，你应该会看到 Claude Code 启动规划和规格起草流程。Claude Code 还会触发一些内置脚本来设置仓库。

一旦这一步完成，你应该会得到一个新分支（例如 `001-create-taskify`），以及 `specs/001-create-taskify` 目录中的新规格。

生成的规格应包含用户故事和功能需求集合，具体格式由模板定义。

此时，项目文件夹内容大致应如下所示：

```text
.
├── .specify
│   ├── memory
│   │   └── constitution.md
│   ├── scripts
│   │   └── bash
│   │       ├── check-prerequisites.sh
│   │       ├── common.sh
│   │       ├── create-new-feature.sh
│   │       ├── setup-plan.sh
│   │       └── setup-tasks.sh
│   └── templates
│       ├── plan-template.md
│       ├── spec-template.md
│       └── tasks-template.md
└── specs
    └── 001-create-taskify
        └── spec.md
```

### **步骤 3：** 功能规格澄清（规划前必需）

在创建基础规格后，你可以继续澄清第一轮尝试中未能正确捕获的需求。

你应该在创建技术计划 **之前** 运行结构化澄清流程，以减少后续返工。

推荐顺序：

1. 使用 `/speckit.clarify`（结构化）——顺序式、基于覆盖率的提问流程，并把答案记录在 Clarifications 部分。
2. 如有需要，再补充自由形式的开放式修改。

如果你有意跳过澄清（例如快速验证或探索性原型），请明确说明，以免代理因缺少澄清而阻塞。

示例自由形式补充提示（在 `/speckit.clarify` 之后，如仍需进一步说明）：

```text
For each sample project or project that you create there should be a variable number of tasks between 5 and 15 tasks for each one randomly distributed into different states of completion. Make sure that there's at least one task in each stage of completion.
```

你还应该要求 Claude Code 验证 **Review & Acceptance Checklist**，勾选所有已验证/满足需求的项，对不满足的项保持未勾选。该清单有助于确保规格质量并减少遗漏。

```text
Read the review and acceptance checklist, and check off each item in the checklist if the feature spec meets the criteria. Leave it empty if it does not.
```

重要的是，要把与 Claude Code 的交互当作澄清和追问规格的机会——**不要把它的第一版结果视为最终版**。

### **步骤 4：** 生成计划

现在你可以明确技术栈和其他技术要求了。你可以使用项目模板中内置的 `/speckit.plan` 命令，并搭配如下提示：

```text
We are going to generate this using .NET Aspire, using Postgres as the database. The frontend should use Blazor server with drag-and-drop task boards, real-time updates. There should be a REST API created with a projects API, tasks API, and a notifications API.
```

这一步的输出会包含一系列实现细节文档，目录树大致如下：

```text
.
├── CLAUDE.md
├── .specify
│   ├── memory
│   │   └── constitution.md
│   ├── scripts
│   │   └── bash
│   │       ├── check-prerequisites.sh
│   │       ├── common.sh
│   │       ├── create-new-feature.sh
│   │       ├── setup-plan.sh
│   │       └── setup-tasks.sh
│   └── templates
│       ├── CLAUDE-template.md
│       ├── plan-template.md
│       ├── spec-template.md
│       └── tasks-template.md
└── specs
    └── 001-create-taskify
        ├── contracts
        │   ├── api-spec.json
        │   └── signalr-spec.md
        ├── data-model.md
        ├── plan.md
        ├── quickstart.md
        ├── research.md
        └── spec.md
```

检查 `research.md` 文档，确保技术栈与指令一致。如果有任何组件看起来不合适，你可以让 Claude Code 继续优化，甚至让它进一步研究这些组件。

此外，如果你选择的技术栈变化很快（例如 .NET Aspire、JavaScript 框架），还可以让 Claude Code 进一步研究该技术栈的细节，例如：

```text
I want you to go through the implementation plan and implementation details, looking for areas that could benefit from additional research as .NET Aspire is a rapidly changing library. For those areas that you identify that require further research, I want you to update the research document with additional details about the specific versions that we are going to be using in this Taskify application and spawn parallel research tasks to clarify any details using research from the web.
```

在这个过程中，你可能会发现 Claude Code 过度研究了错误的方向——你可以通过如下提示把它引导回正轨：

```text
I think we need to break this down into a series of steps. First, identify a list of tasks that you would need to do during implementation that you're not sure of or would benefit from further research. Write down a list of those tasks. And then for each one of these tasks, I want you to spin up a separate research task so that the net results is we are researching all of those very specific tasks in parallel. What I saw you doing was it looks like you were researching .NET Aspire in general and I don't think that's gonna do much for us in this case. That's way too untargeted research. The research needs to help you solve a specific targeted question.
```

> [!NOTE]
> Claude Code 可能会过于积极地添加你并未要求的组件。请要求它说明每项变更的理由和来源。

### **步骤 5：** 让 Claude Code 验证计划

在有了计划之后，你应该让 Claude Code 再过一遍，以确保没有遗漏。你可以使用如下提示：

```text
Now I want you to go and audit the implementation plan and implementation detail files. Read through it with an eye on determining whether or not there is a sequence of tasks that you need to be doing that are obvious from reading this. Because I don't know if there's enough here. For example, when I look at the core implementation, it would be useful to reference the appropriate places in the implementation details where it can find the information as it walks through each step in the core implementation or in the refinement.
```

这有助于进一步优化实现计划，并帮助你避免 Claude Code 在规划过程中遗漏潜在盲点。完成初始优化后，还可以继续要求 Claude Code……

如果你安装了 [GitHub CLI](https://docs.github.com/en/github-cli/github-cli)，也可以让 Claude Code 直接从当前分支创建一个指向 `main` 的 pull request。

> [!NOTE]
> 在让代理执行实现之前，还值得提示 Claude Code 交叉检查细节，看看是否存在过度设计的部分（记住——它可能过于积极）。如果发现某些内容过于复杂，要求它解释原因并给出变更来源。

### **步骤 6：** 使用 /speckit.tasks 生成任务拆解

在实现计划验证完成后，你现在可以将计划拆解为具体、可执行、且按正确顺序执行的任务。使用 `/speckit.tasks` 命令自动生成任务列表。

```text
/speckit.tasks
```

这一步会在你的功能规格目录中创建一个 `tasks.md` 文件，其中包含：

- **按用户故事组织的任务拆解**——每个用户故事都会成为一个独立的实现阶段，包含自己的一组任务
- **依赖关系管理**——任务排序会考虑组件之间的依赖关系（例如先模型、再服务、最后端点）
- **并行执行标记**——可并行执行的任务会被标记为 `[P]`，以优化��发流程
- **文件路径说明**——每个任务都包含应实施的准确文件路径
- **测试驱动开发结构**——如果要求测试，则会包含测试任务，并安排在实现之前编写
- **检查点验证**——每个用户故事阶段都会包含检查点，用于验证独立功能

生成的 `tasks.md` 为 `/speckit.implement` 命令提供了清晰的路线图，确保实现过程系统化，在维护代码质量的同时支持逐步交付用户价值。

### **步骤 7：** 实现

准备就绪后，使用 `/speckit.implement` 命令执行你的实现计划：

```text
/speckit.implement
```

`/speckit.implement` 命令会：

- 验证所有前提是否已准备完毕（constitution、spec、plan 和 tasks）
- 解析 `tasks.md` 中的任务拆解
- 按正确顺序执行任务，并遵守依赖关系和并行执行标记
- 遵循任务计划中定义的 TDD 方法
- 提供进度更新并妥善处理错误

> [!IMPORTANT]
> 编码代理会执行本地 CLI 命令（例如 `dotnet`、`npm` 等）——请确保你的机器上已安装所需工具。

实现完成后，请测试应用，并解决 CLI 日志中可能看不到的运行时错误（例如浏览器控制台错误）。你可以把这些错误复制粘贴回代理，让它继续修复。

</details>

---

## 💬 支持

如需支持，请打开一个 [GitHub issue](https://github.com/github/spec-kit/issues/new)。我们欢迎 bug 报告、功能请求，以及关于如何使用 Spec-Driven Development 的问题。

## 🙏 致谢

本项目深受 [John Lam](https://github.com/jflam) 的工作和研究启发，并在其基础上构建。

## 📄 许可证

本项目依据 MIT 开源许可证授权。完整条款请参阅 [LICENSE](./LICENSE) 文件。
