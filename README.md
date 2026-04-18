# Kilo

## 目录说明

`kilo/` 目录用于承载 Kilo 当前收敛后的最小可用能力集，核心配置位于 `.config/kilo/`：

- `.config/kilo/agent/`：可直接调用的角色文档
- `.config/kilo/command/`：按 workflow 编排的任务入口
- `.config/kilo/rules/`：跨 command 与 agent 复用的稳定治理约束
- `.config/kilo/AGENTS.md`：当前目录的约束与迁移背景

## 如何使用

如果你是第一次使用 Kilo，建议按下面顺序理解：

1. 先看 `.config/kilo/usage-by-scenario.md`
   - 这是一份按场景组织的使用文档
   - 说明遇到什么任务时，应优先选择哪个 command 入口或 agent
2. 再看 `.config/kilo/command/`
   - 适合直接落入某个工作流的任务入口，如开发、调试、审查、安全、脚手架、迁移等
3. 最后按需查看 `.config/kilo/agent/`
   - 当你只需要单一角色能力，或需要理解某个角色边界时使用

## 文档入口

### 按场景使用文档

- [`.config/kilo/usage-by-scenario.md`](./.config/kilo/usage-by-scenario.md)

推荐优先阅读这份文档，再决定使用哪个 command 或 agent。

### 其他文档
- `.config/kilo/rules/workflow-phases.md`：统一 Discovery / Planning / Execution 的阶段语言
- `.config/kilo/rules/file-governance.md`：目录边界、mode 表达与文件输出治理
- `.config/kilo/rules/tooling-context-governance.md`：MCP 使用边界与多 subagent 上下文治理
- `.config/kilo/rules/release-governance.md`：release 收口的最小治理约束
- `@kilo/ARCHITECTURE_LOG.md`：关键结构决策与演进记录

## 当前设计原则

- 优先使用 command 组织完整 workflow，避免用户手工拼接多个 agent
- agent 负责角色能力，command 负责流程闭环
- 长尾能力默认隔离，不污染核心工程链路
- 不单独创建 `skills/`，相关能力应炼化进现有角色或 workflow
- mode 属于运行态控制，不写入 agent 文档本体

## 术语约定

- `mode`：运行态工作模式，决定当前怎么工作
- `phase`：阶段语言，统一使用 `Discovery / Planning / Execution`
- `workflow`：一类可复用任务流程
- `command`：workflow 的实际入口
- `agent`：角色能力，不替代 command 入口
- `brainstorming`：新项目语境下的 `Discovery`，不是独立 command
- `项目分析`：已有项目语境下的 `Discovery`
- `writing-plans`：`Planning` 阶段的计划输出，不是独立 command，当前主要由 `brief-project` 承担

## 默认增强能力

- `serena`：代码语义检索、符号定位、引用分析与精确编辑
- `memory`：项目长期约定、稳定偏好与长任务状态沉淀
- `context7`：官方文档、版本差异与迁移说明查证

它们属于流程增强层，不是新的 command 入口；具体使用边界以 `tooling-context-governance.md` 为准。

## 快速入口建议

- 项目起手与任务收敛：`brief-project`
- 长任务状态汇总：`status-overview`
- 起项目：`scaffold-project`
- 后端功能：`feature-backend`
- 全栈功能：`feature-fullstack`
- 调试排障：`debug-smart`
- 通用审计与分流：`audit-general`
- 完整审查：`review-full`
- 安全加固：`security-hardening`
- TDD：`tdd-cycle`
- 可观测性专项：`observability-review`
- 升级迁移：`migration-upgrade`
- API Mock：`api-mock`
- 图像灵感检索：`meigen-find`
