# Kilo 全局约定

## 目标

主 `AGENTS.md` 负责全局目标、术语与顶层约束；稳定治理规则下沉到 `rules/`；
`command/` 负责 workflow 入口；`agent/` 负责角色能力定义。

这样可以避免主 `AGENTS.md` 演变成大而全手册，并保持目录职责清晰。

## 核心原则

1. 优先使用 command 组织完整 workflow，避免手工拼接多个 agent
2. agent 负责角色能力，command 负责流程闭环，rules 负责稳定治理约束
3. 证据驱动，不凭空假设；复杂任务先规划，再进入执行
4. 安全优先，不写入敏感信息，不引入已知高风险依赖
5. 保持小步交付，涉及代码或配置改动时优先完成本地验证
6. 长尾能力默认隔离，不污染核心工程链路
7. 不单独创建 `skills/`，相关能力继续炼化进 agent 或 command

## 语言要求

- 说明、规则、文档与注释默认使用中文
- 技术术语保留英文原文
- 文件名、command 名、agent 名与代码标识符保持英文

## 术语约定

- `mode`：运行态工作模式，决定当前怎么工作
- `phase`：阶段语言，统一使用 `Discovery / Planning / Execution`
- `workflow`：一类可复用任务流程
- `command`：workflow 的实际入口
- `agent`：角色能力，不替代 command 入口
- `brainstorming`：新项目语境下的 `Discovery`，不是独立 command
- `项目分析`：已有项目语境下的 `Discovery`
- `writing-plans`：`Planning` 阶段的计划输出，不是独立 command，当前主要由 `brief-project` 承担
- `audit`：偏发现、分类与分流
- `review`：偏深入审查、问题分级与结论输出

## 默认增强能力

以下能力属于流程增强层，不是新的 command：

- `serena`：代码语义检索、符号定位、引用分析与精确修改
- `memory`：长期约定、稳定偏好与长任务状态沉淀
- `context7`：官方文档、版本差异与迁移说明查证

关键摘要：

- `serena` 优先用于代码理解、符号定位、引用分析、跨文件影响判断与精确修改
- `memory` 只沉淀稳定、高价值、跨轮次复用的信息，不记录一次性执行细节
- `context7` 优先用于框架 API、官方推荐写法、版本差异与迁移说明查证

具体使用边界与 `memory` 写入规则以 `rules/tooling-context-governance.md` 为准。

## 阶段摘要

- 统一阶段语言为 `Discovery / Planning / Execution`
- 已有项目中，`Discovery` 通常表现为“项目分析”
- 新项目中，`Discovery` 通常表现为 `brainstorming`
- `Planning` 的常见输出为 `writing-plans`
- command 负责把阶段串成 workflow，agent 在各自职责范围内遵循同样阶段纪律

具体阶段定义以 `rules/workflow-phases.md` 为准。

## 目录与输出摘要

- `agent/` 只承载角色定义，不承载运行命令或具体 workflow 步骤
- `command/` 承载 workflow 入口与阶段编排
- `rules/` 只保留稳定、跨多处复用的约束
- 复杂任务的 Discovery、Planning、审计、review、迁移与长任务状态应优先落成可追踪文件
- 小任务、一次性咨询或低风险改动允许只在对话中输出，不强制创建文件

具体目录边界与文件输出治理以 `rules/file-governance.md` 为准。

## Release 摘要

- release 收口前应尽量具备计划、状态、验证结果、已知风险与回滚边界
- release 输出至少应包含发布范围、主要变更摘要、验证结果摘要、已知风险与回滚说明
- 若需求只是整理当前状态，应优先使用 `status-overview`，不要滥用 release 概念

具体 release 治理以 `rules/release-governance.md` 为准。

## 模式要求原则

- `mode` 属于运行态控制，不写成命令式 `switch mode`
- `mode` 不写入 `agent/*.md`
- command 如需表达阶段切换，应使用 `## 模式要求` 小节
