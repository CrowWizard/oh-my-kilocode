# Release Governance

## 目标

定义 `kilo/.kilo` 当前最小可用的 release 治理约束，为后续是否引入 release 类 command 提供稳定前提。

当前阶段先建立发布收口规则，不立即假设存在完整版本系统。

---

## 适用范围

适用于以下场景：

- 一次较完整的功能交付准备对外发布
- 一次较大的修复批次准备收口
- 一次迁移、升级或安全修复准备形成发布说明
- 需要生成 changelog、release note 或发布批次摘要时

---

## release 的前置条件

在考虑 release 类 workflow 前，应尽量具备以下输入：

- 计划文件，例如 `PLAN.md` 或等价计划文档
- 状态文件，例如 `STATUS.md` 或等价状态文档
- 相关审计、review、安全、可观测性或迁移结果文件
- 已执行验证命令与结果摘要
- 已知风险、未完成项与回滚边界说明

若以上信息长期缺失，不应直接进入 release 收口。

---

## release 前检查项

进入 release 收口前，至少应确认：

- 当前发布范围已经明确
- 核心验证已经完成，或未完成项已明确记录
- 高风险 blocker 没有被忽略
- 涉及迁移、配置或安全影响时，已给出单独说明
- 已有最小回滚路径或回退说明
- 已明确本次发布是正式版本、内部批次，还是阶段性发布摘要

---

## release 输出要求

release 类 workflow 至少应产出以下之一：

- `CHANGELOG.md`
- `RELEASE_NOTES.md`
- `docs/releases/<topic-or-version>.md`

输出内容至少包含：

- 发布范围
- 主要变更摘要
- 验证结果摘要
- 已知风险
- 配置、迁移或兼容性注意事项
- 回滚说明或回退边界

---

## 边界约束

- release workflow 只负责发布收口、变更摘要与说明整理
- 不替代开发、review、安全修复、迁移实施本身
- 在版本命名、SemVer、发布批次规则未稳定前，不强制要求版本号治理
- 若需求只是整理当前任务状态，应优先使用 `status-overview`，而不是滥用 release 概念

---

## 当前结论

- 当前已具备“开始设计 release workflow”的基础
- 但在 release 输入、检查项与输出载体稳定之前，不急于新增正式 `/release` command
- 后续如需落地，更适合先从 `release-prep` 或 `release-summary` 这类轻量 command 开始