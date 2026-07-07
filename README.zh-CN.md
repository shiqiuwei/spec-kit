# Spec Kit 中文说明

<div align="center">
  <img src="./media/logo_large.webp" alt="Spec Kit Logo" width="200" height="200"/>
  <h1>🌱 Spec Kit</h1>
  <h3><em>更快构建高质量软件</em></h3>
</div>

## 项目简介

Spec Kit 是一个用于 **Spec-Driven Development（规格驱动开发）** 的开源工具包。

它的目标不是让 AI 直接从一句模糊提示里“即兴写代码”，而是帮助你先明确：

- 要构建什么
- 为什么要构建
- 有哪些约束和原则
- 应该如何规划实现

然后再让 AI 编码代理基于这些上下文，有步骤地完成实现。

简单来说，Spec Kit 想把 AI 辅助开发从不可预测的“vibe coding”，变成 **更结构化、可追踪、可复用** 的工程化流程。

---

## 它解决的问题

传统开发和 AI 辅助开发中常见的问题包括：

- 规格说明往往不完整，或者在写完代码后就失去作用
- 直接让 AI 从 prompt 开始写代码，结果容易不可控
- 团队缺少统一的约束、模板和执行流程
- 功能需求、技术计划、任务拆解之间容易脱节

Spec Kit 通过一套标准流程，把开发过程拆成多个阶段，让需求、计划、任务和实现之间保持一致。

---

## 核心工作流

README 中介绍的标准流程大致如下：

### 1. 安装 Specify CLI

推荐使用 `uv` 安装：

```bash
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git@vX.Y.Z
```

你也可以参考项目文档选择其他安装方式。

### 2. 初始化项目

```bash
specify init my-project --integration copilot
cd my-project
```

这一步会把 Spec Kit 所需的模板、命令和项目结构写入你的项目目录中。

### 3. 建立项目原则

使用：

```text
/speckit.constitution
```

这一阶段用于定义项目级原则，例如：

- 代码质量要求
- 测试标准
- 性能要求
- 用户体验一致性
- 团队治理规则

### 4. 编写功能规格

使用：

```text
/speckit.specify
```

在这一步，重点描述：

- 你要做什么
- 目标用户是谁
- 为什么这个功能有价值

而不是一开始就陷入技术细节。

### 5. 生成技术实现计划

使用：

```text
/speckit.plan
```

这一步再明确：

- 技术栈
- 架构方案
- 数据模型
- 外部依赖
- 实现边界

### 6. 拆解任务

使用：

```text
/speckit.tasks
```

把实现计划拆成可执行的任务清单，便于逐步推进和跟踪。

### 7. 执行实现

使用：

```text
/speckit.implement
```

AI 编码代理会基于前面形成的规格、计划和任务列表来实施功能，而不是无约束地直接生成代码。

---

## 主要命令

### 核心命令

- `/speckit.constitution`：创建或更新项目治理原则
- `/speckit.specify`：定义功能需求、用户故事和目标
- `/speckit.plan`：生成技术实现计划
- `/speckit.tasks`：把计划拆成任务列表
- `/speckit.taskstoissues`：把任务转换成 GitHub Issues
- `/speckit.implement`：根据任务执行实现
- `/speckit.converge`：对照规格/计划/任务检查缺口并补充工作项

### 可选增强命令

- `/speckit.clarify`：对不清晰的需求进行澄清
- `/speckit.analyze`：检查规格、计划和任务之间的一致性
- `/speckit.checklist`：生成自定义质量检查清单

---

## 扩展能力

Spec Kit 不只是一个固定模板，还提供了三类扩展机制。

### 1. Extensions

用于 **新增能力**，例如：

- Jira 集成
- 审查工作流
- 测试追踪能力
- 项目健康检查

### 2. Presets

用于 **定制现有工作流的行为**，例如：

- 调整规格模板
- 适配 Agile / Kanban / Waterfall
- 增加合规或审计要求

### 3. Bundles

用于把多个扩展和预设打包成一整套角色化配置，例如：

- 产品经理
- 业务分析师
- 安全研究人员
- 开发者

这样团队成员可以按角色快速安装一整套工作流能力。

---

## 核心理念

Spec Kit 的核心理念包括：

- **先定义意图，再定义实现**
- **先写规格，再做计划，再拆任务，再落地代码**
- **通过多阶段迭代提升结果质量**
- **让 AI 在明确约束和上下文中工作**
- **提高开发过程的可预测性与可维护性**

它强调的不是“一次 prompt 生成全部代码”，而是构建一个更适合复杂项目、团队协作和长期维护的 AI 开发流程。

---

## 适用场景

README 中提到它适用于多种场景，例如：

- **0 到 1 新项目开发**
- **创意探索**：并行比较不同方案
- **已有项目迭代增强**
- **旧系统现代化改造**
- **带组织规范或企业约束的开发**

---

## 运行前提

使用前通常需要：

- Linux / macOS / Windows
- 支持的 AI coding agent
- `uv` 或 `pipx`
- Python 3.11+
- Git

---

## 一句话理解

**Spec Kit 不是单纯的代码生成工具，而是一套帮助你把 AI 辅助开发流程规范化、阶段化、可追踪化的方法和工具链。**

---

## 进一步阅读

如果你想了解更多，可以继续查看仓库中的这些内容：

- `README.md`：英文原始说明
- `spec-driven.md`：完整方法论介绍
- `docs/`：安装、快速开始、升级和参考文档
- `extensions/`：扩展系统说明
- `presets/`：预设系统说明
- `examples/`：示例内容

