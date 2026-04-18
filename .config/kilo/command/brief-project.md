---
name: brief-project
description: 以项目起手与任务收敛为入口，区分新项目与已有项目，统一组织 Discovery、decision-framing、writing-plans 与后续 workflow 选择。
---

# 工作流目标

用于在真正进入开发、调试、审查或脚手架生成之前，先把项目类型、任务边界、关键约束与下一步入口收敛清楚。

## 模式要求

- 项目判断、范围澄清与计划输出阶段可在只读模式进行
- 仅当后续明确进入脚手架生成、实现、修复、测试补齐或配置写入阶段，才切换到可写执行模式
- 本 workflow 自身以收敛与分流为主，不要求在当前阶段直接修改代码

## 工具偏好

- 涉及项目长期约定、个人偏好或已有稳定边界时，优先读取 `memory`
- 涉及代码结构理解、符号定位或跨文件影响范围判断时，必要时补充使用 `serena`

## Workflow

### 步骤 1：判断项目类型
- 先区分当前任务属于“已有项目”还是“新项目”
- 明确当前目标是起盘、开发、调试、审查、安全、迁移、mock 还是专项 review

### 步骤 2：执行 Discovery
- 已有项目：分析技术栈、目录结构、分层方式、既有模式、依赖与影响范围
- 新项目：通过 brainstorming 明确目标、用户、成功标准、范围与非范围
- 记录未知项、约束项与潜在风险

### 步骤 3：必要时执行 decision-framing
- 当 Discovery 结果较多、方案分歧明显、风险较高或边界仍不够清晰时，先做一轮结构化收敛
- 汇总关键约束、主要风险、备选方案与推荐方向
- 明确哪些判断已经足以进入 `writing-plans`，哪些问题仍需补充

### 步骤 4：输出 writing-plans
- 给出最小可执行计划
- 明确实施步骤、验证方式、风险点与回滚边界
- 标注哪些信息已确认，哪些仍待补充

### 步骤 5：分流到后续入口
- 新项目起盘：进入 `scaffold-project`
- 单个后端功能：进入 `feature-backend`
- 全栈功能：进入 `feature-fullstack`
- 调试排障：进入 `debug-smart`
- 完整审查：进入 `review-full`
- 安全加固：进入 `security-hardening`
- TDD：进入 `tdd-cycle`
- 可观测性专项：进入 `observability-review`
- 升级迁移：进入 `migration-upgrade`
- Mock 场景：进入 `api-mock`

### 步骤 6：输出起手结论
- 输出项目类型判断结果
- 如有触发，输出 `decision-framing` 收敛摘要
- 输出 writing-plans 摘要
- 明确推荐的下一个 workflow 或 agent
- 如当前信息不足，列出必须先补齐的问题清单

## 与 `/task` 思想的关系

- 本 workflow 承担统一任务 intake、Discovery、必要时的 `decision-framing`、writing-plans 与后续 workflow 分流职责
- 当前不再单独引入通用 `/task` command，避免与 `feature-backend`、`feature-fullstack` 及其他专项 workflow 重叠
- 若任务尚不明确属于哪类入口，优先先走 `brief-project`

## 产出清单

- 项目类型判断
- Discovery 结果摘要
- 如有触发，补充 `decision-framing` 收敛摘要
- writing-plans 摘要
- 推荐后续入口
- 关键风险与待补充信息
