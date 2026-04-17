# Kilo

## 目录说明

`kilo/` 目录用于承载 Kilo 当前收敛后的最小可用能力集，核心内容位于 `@kilo/.kilo`：

- `@kilo/.kilo/agent/`：可直接调用的角色文档
- `@kilo/.kilo/command/`：按 workflow 编排的任务入口
- `@kilo/.kilo/rules/`：跨 command 与 agent 复用的稳定治理约束
- `@kilo/.kilo/AGENTS.md`：当前目录的约束与迁移背景
- `@kilo/docs/`：补充说明文档、使用文档与阶段性决策记录

## 如何使用

如果你是第一次使用 Kilo，建议按下面顺序理解：

1. 先看 `@kilo/docs/usage-by-scenario.md`
   - 这是一份按场景组织的使用文档
   - 说明遇到什么任务时，应优先选择哪个 workflow 或 agent
2. 再看 `@kilo/.kilo/command/`
   - 适合直接落入某个工作流的任务入口，如开发、调试、审查、安全、脚手架、迁移等
3. 最后按需查看 `@kilo/.kilo/agent/`
   - 当你只需要单一角色能力，或需要理解某个角色边界时使用

## 文档入口

### 按场景使用文档

- [`@kilo/docs/usage-by-scenario.md`](./docs/usage-by-scenario.md)

推荐优先阅读这份文档，再决定使用哪个 command 或 agent。

### 其他文档

- `@kilo/docs/common-execution-flow.md`：已有项目与新项目的通用执行流程
- `@kilo/docs/kilo-maintainer-guide.md`：维护者如何继续演进 `.kilo/` 的说明
- `@kilo/docs/agent-vs-subagent-plan.md`：主 agent、逻辑 subagent 与双形态角色的分层计划
- `@kilo/docs/universal-template-integration-plan.md`：与外部 universal template 的整合计划
- `@kilo/docs/phase-3-longtail-admission.md`：长尾能力准入与试点结论
- `@kilo/.kilo/rules/workflow-phases.md`：统一 Discovery / Planning / Execution 的阶段语言
- `@kilo/.kilo/rules/file-governance.md`：目录边界、mode 表达与文件输出治理
- `@kilo/.kilo/rules/release-governance.md`：release 收口的最小治理约束
- `@kilo/ARCHITECTURE_LOG.md`：关键结构决策与演进记录

## 当前设计原则

- 优先使用 command 组织完整 workflow，避免用户手工拼接多个 agent
- agent 负责角色能力，command 负责流程闭环
- 长尾能力默认隔离，不污染核心工程链路
- 不单独创建 `skills/`，相关能力应炼化进现有角色或 workflow
- mode 属于运行态控制，不写入 agent 文档本体

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
