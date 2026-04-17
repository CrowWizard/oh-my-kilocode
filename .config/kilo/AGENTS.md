# Kilo Workspace Guide

## 目标

本目录承载 `kilo/` 当前收敛后的核心工作台配置，用于统一 agent、command、rules 与配套说明文档的职责边界。

这里描述的是当前稳定结构，不再保留早期 Phase 1 最小迁移口径。

## 目录结构

- `agent/`：可直接调用的角色文档，负责角色能力、工作边界与输出要求
- `command/`：workflow 入口文档，负责阶段编排、角色协作、模式要求与收口方式
- `rules/`：稳定、跨多处复用的治理约束，不承载一次性说明
- `AGENTS.md`：`.kilo/` 总述、边界原则与维护入口

## 当前能力组成

### Agents

- `architect`
- `backend-engineer`
- `frontend-engineer`
- `devops-engineer`
- `test-engineer`
- `security-auditor`
- `debugger`
- `code-reviewer`
- `docs-architect`
- `data-engineer`

### Commands

- `brief-project`
- `status-overview`
- `audit-general`
- `scaffold-project`
- `feature-backend`
- `feature-fullstack`
- `debug-smart`
- `review-full`
- `security-hardening`
- `tdd-cycle`
- `observability-review`
- `migration-upgrade`
- `api-mock`
- `meigen-find`

### Rules

- `workflow-phases.md`
- `file-governance.md`
- `release-governance.md`

## 边界原则

1. 优先使用 command 组织完整 workflow，避免让用户手工拼接多个 agent
2. agent 负责角色能力，不承载运行时 mode，也不编排完整 workflow
3. command 负责阶段串联、角色协作、模式要求与结果收口
4. rules 只保留稳定治理约束，不重复堆叠到每个 agent 或 command
5. docs 与 README 负责使用说明、维护说明与演进记录，不替代规则本体
6. 不单独创建 `skills/`，相关能力继续炼化进 agent 或 command
7. 长尾能力默认隔离，不污染核心工程链路

## 关于模式要求

- mode 属于运行态控制，不写成命令式 `switch mode`
- mode 不写入 `agent/*.md`
- command 如需表达阶段切换，应使用 `## 模式要求` 小节
- `模式要求` 应优先说明三件事：哪些阶段默认只读、何时进入可写执行模式、验证与归档阶段是否继续保持可写

## 与三阶段流程的关系

- 当前默认流程语言采用 `Discovery / Planning / Execution`
- 阶段定义以 `rules/workflow-phases.md` 为准
- command 负责把阶段串成可复用 workflow
- agent 在自身职责范围内遵循同样的阶段纪律，但不替代 command

## 维护要求

1. 新增或删除 agent / command / rules 时，应同步更新 `README.md` 与相关 docs
2. 新增 command 时，先判断它是否真的是稳定、多阶段、可复用的 workflow
3. 新增 agent 时，先判断它是否真的是长期存在、边界清晰、值得直接调用的角色
4. 如需新增规则文件，必须确认它是稳定、跨多处复用、适合作为治理源的约束
5. 修改结构后，应避免 README、docs 与 `.kilo/` 实际状态发生信息漂移

## 相关入口

- `@kilo/README.md`：总导航与快速入口
- `@kilo/docs/usage-by-scenario.md`：按场景选 command / agent
- `@kilo/docs/common-execution-flow.md`：通用执行流程
- `@kilo/docs/kilo-maintainer-guide.md`：维护者说明
