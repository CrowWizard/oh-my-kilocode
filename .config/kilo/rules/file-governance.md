# File Governance

## 目标

定义 `kilo/.kilo` 当前的核心治理约束，保证目录结构、能力边界与安全约束保持一致。

---

## 目录治理

- `agent/` 只承载角色定义，不承载运行命令或具体 workflow 步骤
- `command/` 承载 workflow 入口与阶段编排
- `rules/` 只保留稳定、跨多处复用的约束，不堆砌杂项文档
- `docs/` 承载使用说明、维护说明、执行流程与决策记录
- 不单独创建 `skills/` 目录，相关能力直接炼化进 agent 或 command

---

## 安全与敏感文件治理

- 不在文档中鼓励读取或输出敏感文件内容
- 不应把密钥、凭据、Token、密码等敏感信息写入规则、agent、command 或示例
- 涉及环境变量、密钥与部署配置时，只能写边界与要求，不写真实值

---

## 能力边界治理

- 优先使用 command 组织完整 workflow，避免用户手工拼接多个 agent
- agent 负责角色能力，command 负责流程闭环，mode 负责运行态控制
- mode 不写入 `agent/*.md`
- command 如需表达阶段切换，应写成文档化“模式要求”，不写成命令式 `switch mode`
- 长尾能力默认隔离，不污染核心工程链路

---

## 文件输出治理

- 复杂任务的 Discovery 结果应优先写入摘要文件，而不是只保留在对话中
- writing-plans 在跨阶段、多人协作或高风险任务中应落成计划文件
- `audit-general`、`review-full`、`security-hardening`、`observability-review`、`migration-upgrade` 的结果优先落成可追踪文件
- `status-overview` 在长任务中应维护状态文件
- 小任务、一次性咨询或低风险改动允许仅输出对话结果，不强制创建文件
- 推荐但不强制的最小文件载体包括：`PLAN.md`、`STATUS.md` 与 `docs/*-<topic>.md`

## 演进治理

- 新增 agent 或 command 时，应同步更新 README、usage 文档与相关决策记录
- 外部模板只能选择性吸收，不得整仓照搬覆盖当前结构
- 对现有约束有冲突时，优先保持当前仓库已确认的收敛原则