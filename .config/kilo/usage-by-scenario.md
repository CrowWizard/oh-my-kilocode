## Kilo 使用文档：按场景选择 agent 与 workflow

### 目标

本文档作为 `kilo/` 根目录下的统一使用入口，整合原 `docs/usage-by-scenario.md` 与 `docs/common-execution-flow.md` 中的使用说明与过程建议。

适用对象：

- 想快速判断该选哪个 workflow 的使用者
- 想理解 agent 与 command 分工边界的维护者
- 想避免重复造入口、误用角色或把长尾能力混入核心链路的整理者

---

## 一、先记住三个判断规则

### 1. 先选 workflow，再补充 agent

如果当前任务能直接落入已有 command，优先使用 command：

- `brief-project`
- `status-overview`
- `scaffold-project`
- `feature-backend`
- `feature-fullstack`
- `debug-smart`
- `audit-general`
- `review-full`
- `security-hardening`
- `tdd-cycle`
- `observability-review`
- `migration-upgrade`
- `api-mock`
- `meigen-find`

只有当任务还不适合直接落入某个 workflow，或者你只需要单点角色能力时，才直接点 agent。

### 2. agent 负责角色能力，command 负责流程闭环

- `agent`：解决“谁来做”
- `command`：解决“怎么串起来做”

补充约定：

- `command` 是 workflow 的实际入口
- `agent` 是角色能力，不替代 command 入口

例如：

- 你要交付一个后端功能，优先用 `feature-backend`
- 你只想让某个角色给出架构方案，才直接用 `architect`

### 3. 长尾能力默认隔离，不污染核心工程链路

当前核心工程链路围绕：

- 架构
- 后端
- 前端
- 测试
- 安全
- 调试
- 代码审查
- 文档
- DevOps / 可观测性
- 数据工程

图像灵感、外部设计参考、特定长尾域能力，默认只保留为独立 command，不进入通用 agent 池。

### 4. `brainstorming`、`项目分析` 与 `writing-plans` 都不是独立 command

- `Discovery` 是总阶段名
- 已有项目语境下，`Discovery` 通常表现为“项目分析”
- 新项目语境下，`Discovery` 通常表现为 `brainstorming`
- `writing-plans` 是 `Planning` 阶段的计划输出，不是独立 command
- 当前 `brainstorming` 与 `writing-plans` 主要由 `brief-project` 承担

---

## 二、通用执行顺序

### 已有项目

默认顺序：

```text
项目分析 → writing-plans → 进入实现 / 调试 / review workflow → 验证与收口
```

最低应确认：

- 技术栈
- 目录结构
- 分层方式
- 既有模式
- 依赖与工具链
- 本次任务影响范围

目标：

- 避免脱离现有模式做理想化重写
- 避免误伤稳定模块
- 避免重复造已有抽象

### 新项目

默认顺序：

```text
brainstorming → writing-plans → scaffold-project / 实施 → 验证与收口
```

最低应确认：

- 要解决什么问题
- 用户是谁
- 成功标准是什么
- 范围与非范围
- 技术栈候选
- 最小交付物是什么

目标：

- 在没有既有结构可分析时，先把目标与边界收敛
- 避免一开始就陷入目录和文件细节

### 共通原则

- 优先判断是否已有匹配的 command
- 只有 workflow 不适用，或只需要单点角色能力时，才直接点 agent
- 只要任务开始形成多阶段闭环，仍应优先回到 command
- 当前任务阶段统一使用 `Discovery / Planning / Execution`

---

## 三、当前能力地图

### 核心 agent

- `architect`：需求澄清、系统分层、接口边界、数据模型、风险评估
- `backend-engineer`：后端接口、业务逻辑、数据访问、校验、可观测性实现
- `frontend-engineer`：页面、组件、交互、状态管理、可访问性实现
- `test-engineer`：测试设计、自动化验证、回归保护
- `security-auditor`：安全审查、威胁建模、漏洞修复建议
- `debugger`：问题定位、根因假设、最小修复、回归预防
- `code-reviewer`：代码质量、可维护性、风险识别、改进建议
- `docs-architect`：架构说明、使用指南、实现背景、维护文档
- `devops-engineer`：构建、部署、环境治理、交付可观测性
- `data-engineer`：数据建模、迁移、ETL、流批处理、数据质量治理

### 核心 workflow / command

- `brief-project`：项目起手、任务收敛与后续入口分流
- `status-overview`：长任务状态汇总与阶段定位
- `scaffold-project`：创建项目或子工程骨架
- `feature-backend`：交付单个后端功能
- `feature-fullstack`：交付跨前后端功能
- `debug-smart`：问题排查与最小修复
- `audit-general`：轻量发现式审计与后续分流
- `review-full`：多维度完整审查
- `security-hardening`：安全加固闭环
- `tdd-cycle`：按 RED / GREEN / REFACTOR 推进实现
- `observability-review`：专项审查指标、日志、trace、告警与 SLO
- `migration-upgrade`：框架、依赖、运行时或伴随数据迁移的升级工程
- `api-mock`：构建 Mock API 与场景模拟
- `meigen-find`：查找图像灵感与提示词线索

---

## 四、按场景选入口

### 场景 1：任务还没收敛，不确定后面该走哪条 workflow

**优先入口：** `brief-project`

适用情况：

- 还不确定任务属于开发、调试、审查、安全、迁移还是起盘
- 需要先做项目分析或 `brainstorming`
- 需要先产出最小 `writing-plans` 再分流

输出重点：

- 项目类型判断
- Discovery 结果摘要
- writing-plans 摘要
- 推荐后续入口
- 风险与待补充信息

示例：

- `/brief-project 我想改造现有支付模块，但还不确定应该先做审计、直接开发、还是先排查现有问题，请先帮我收敛任务并给出下一步入口`

### 场景 2：需要查看长任务当前状态

**优先入口：** `status-overview`

适用情况：

- 多阶段任务推进到中途
- 需要整理当前阶段、已完成项、阻塞点与下一步
- 想避免上下文漂移

输出重点：

- 当前任务目标
- 当前阶段判断
- 已完成项
- 阻塞点与风险
- 下一步建议

示例：

- `/status-overview 帮我汇总当前订单系统改造任务的进度，说明现在处于哪个阶段、已经完成什么、还有哪些阻塞和下一步建议`

### 场景 3：从零起盘一个新项目或新子工程

**优先入口：** `scaffold-project`

适用情况：

- 新建 Python / Go / JavaScript / TypeScript 项目
- 新建 API 服务、前端应用、库、CLI、任务型服务
- 需要统一目录、配置、脚本、测试与基础验证入口

补充 agent：

- 需要明确系统边界时，补 `architect`
- 需要运行、容器化、部署约束时，补 `devops-engineer`

示例：

- `/scaffold-project 新建一个 TypeScript Node API 服务，希望一次性生成 src/、tests/、package.json、tsconfig.json、lint / test / type-check 脚本与最小健康检查入口`

### 场景 4：实现一个单独的后端功能

**优先入口：** `feature-backend`

默认协作角色：

- `architect`
- `backend-engineer`
- `security-auditor`
- `test-engineer`
- 必要时 `docs-architect`

示例：

- `/feature-backend 在现有 FastAPI 服务中新增创建订单接口，包含请求校验、库存校验、数据库写入、错误返回与最小回归测试`

### 场景 5：交付跨前后端完整功能

**优先入口：** `feature-fullstack`

默认协作角色：

- `architect`
- `backend-engineer`
- `frontend-engineer`
- `security-auditor`
- `code-reviewer`
- `test-engineer`
- `docs-architect`

示例：

- `/feature-fullstack 新增用户资料页，补后端资料查询与保存接口，并实现前端页面、表单校验、加载态、错误态与提交成功反馈`

### 场景 6：线上报错、测试失败、异常行为排查

**优先入口：** `debug-smart`

默认协作角色：

- `debugger`
- 必要时 `code-reviewer`
- 回归保护阶段补 `test-engineer`

推荐使用方式：

1. 先收集日志、堆栈、复现路径与环境差异
2. 排出根因假设
3. 验证后再做最小修复
4. 补最小回归保护

示例：

- `/debug-smart 线上订单支付成功后偶发没有生成发票，日志里只有部分 request id，请先帮我归档问题、列根因假设并给出最小修复路径`

### 场景 7：先做一次通用审计，再决定走哪条专项 workflow

**优先入口：** `audit-general`

默认协作角色：

- `code-reviewer`
- 必要时补 `architect`、`security-auditor`、`devops-engineer`

边界：

- `audit-general` 偏发现、分类与分流
- 它不默认承担完整深入审查或持续修复

示例：

- `/audit-general 帮我先审一遍这个支付模块，判断主要问题更偏代码质量、安全风险、可观测性缺口还是升级兼容性，并给出下一步建议入口`

### 场景 8：准备提交前做完整代码审查

**优先入口：** `review-full`

默认协作角色：

- `code-reviewer`
- `architect`
- `security-auditor`
- `test-engineer`
- `docs-architect`

边界：

- `review-full` 偏深入审查、问题分级与放行判断
- 如果只是先做轻量发现式分类，优先用 `audit-general`

示例：

- `/review-full 帮我对这组待提交改动做完整审查，覆盖代码质量、架构一致性、安全风险、测试充分性和文档缺口`

### 场景 9：识别和修复安全风险

**优先入口：** `security-hardening`

默认协作角色：

- `security-auditor`
- 必要时 `architect`
- 修复阶段可配合 `backend-engineer` / `frontend-engineer`
- 回归验证配合 `test-engineer`

边界：

- `security-hardening` 是安全加固 workflow，不等于只做安全 review
- 它包含风险识别、优先级排序、修复与回归验证

示例：

- `/security-hardening 检查这个登录与权限模块的输入校验、鉴权边界、密钥使用和配置风险，并按优先级给出修复顺序`

### 场景 10：想按 TDD 节奏推进实现

**优先入口：** `tdd-cycle`

默认协作角色：

- `test-engineer`
- `code-reviewer`
- 实现阶段按需要配合 `backend-engineer` / `frontend-engineer`

示例：

- `/tdd-cycle 为优惠券折扣计算逻辑新增测试，先覆盖满减、互斥优惠、无效券和边界金额，再用最小实现让测试通过并整理重构`

### 场景 11：专项检查可观测性是否到位

**优先入口：** `observability-review`

默认协作角色：

- `devops-engineer`

补充角色：

- 涉及代码埋点、日志上下文、接口 trace 透传时，可补 `backend-engineer` 或 `frontend-engineer`

示例：

- `/observability-review 帮我检查这个 API 服务上线前的日志、指标、trace、告警和 SLO 是否足够支撑问题发现与定位`

### 场景 12：升级框架、依赖、运行时，或伴随迁移

**优先入口：** `migration-upgrade`

默认协作角色：

- `architect`
- `backend-engineer`
- `frontend-engineer`
- `devops-engineer`
- 涉及数据迁移时补 `data-engineer`

示例：

- `/migration-upgrade 把现有项目从旧版框架升级到新主版本，先梳理 breaking changes、配置差异、迁移步骤、验证命令和回退方案`

### 场景 13：前后端并行开发，需要先造 Mock API

**优先入口：** `api-mock`

默认协作角色：

- `backend-engineer`

补充角色：

- 需要前端联调约束时，可补 `frontend-engineer`
- 需要测试场景分层时，可补 `test-engineer`

示例：

- `/api-mock 为用户中心接口生成 mock，覆盖成功返回、空结果、401、429 和上游异常五种场景，供前端联调先使用`

### 场景 14：只想做图像灵感检索

**优先入口：** `meigen-find`

边界：

- 只负责“找灵感”
- 不负责前端设计实现
- 不负责完整图片生成工作流

示例：

- `/meigen-find 帮我找“深色数据看板 + 蓝紫渐变 + 未来感控制台”方向的参考图和提示词线索`

---

## 五、什么时候直接点 agent

以下情况可以跳过完整 workflow，直接点 agent：

- 只需要架构方案：`architect`
- 只需要后端实现建议：`backend-engineer`
- 只需要前端实现建议：`frontend-engineer`
- 只需要测试设计：`test-engineer`
- 只需要安全审查：`security-auditor`
- 只需要根因分析：`debugger`
- 只需要代码质量审查：`code-reviewer`
- 只需要文档整理：`docs-architect`
- 只需要交付/部署建议：`devops-engineer`
- 只需要数据链路建议：`data-engineer`

补充说明：

- `security-auditor` 与 `debugger` 当前属于双形态角色
- `code-reviewer`、`docs-architect` 更推荐作为 workflow 内部辅助角色使用

---

## 六、按任务目标快速选型

| 目标 | 优先入口 | 补充角色 |
| --- | --- | --- |
| 任务起手与分流 | `brief-project` | `architect` / `code-reviewer` |
| 查看长任务状态 | `status-overview` | 按当前阶段补充 |
| 起一个新项目 | `scaffold-project` | `architect` / `devops-engineer` |
| 做后端功能 | `feature-backend` | `architect` / `security-auditor` / `test-engineer` |
| 做前后端联动功能 | `feature-fullstack` | `architect` / `security-auditor` / `test-engineer` |
| 排查问题 | `debug-smart` | `debugger` / `test-engineer` |
| 先做轻量审计 | `audit-general` | `code-reviewer` / `security-auditor` |
| 做完整 review | `review-full` | `code-reviewer` / `architect` / `security-auditor` |
| 做安全加固 | `security-hardening` | `security-auditor` / `test-engineer` |
| 按 TDD 开发 | `tdd-cycle` | `test-engineer` / `code-reviewer` |
| 查可观测性缺口 | `observability-review` | `devops-engineer` |
| 做升级迁移 | `migration-upgrade` | `architect` / `devops-engineer` / `data-engineer` |
| 造接口 mock | `api-mock` | `backend-engineer` / `frontend-engineer` |
| 找图像灵感 | `meigen-find` | 无需进入核心工程角色 |

---

## 七、模式与流程使用建议

### 1. 优先让 workflow 驱动，而不是让 agent 乱跳

如果已有 command 能覆盖，就不要手工拼多个 agent。

### 2. 只读分析与可写执行的边界看 workflow

可按以下原则理解：

- 需求澄清、方案分析、问题归档阶段可只读
- 一旦进入实现、修复、脚手架生成、测试补齐、配置写入与验证归档阶段，应进入可写执行

补充说明：

- `mode` 是运行态工作模式
- 文档里对 `mode` 的表达统一写为“模式要求”

### 3. 不要把 `switch mode` 写进 agent 文档

- agent 是角色定义
- command 是流程编排
- mode 是运行态控制

三者应分层处理，不要混写。

### 4. 默认增强能力按阶段按需使用

- `serena`：当任务涉及代码语义检索、符号定位、引用分析、跨文件理解或精确修改时优先使用
- `memory`：当任务涉及项目长期约定、个人偏好、长任务状态或稳定边界沉淀时优先使用
- `context7`：当任务涉及框架 API、官方用法、版本差异或迁移说明时优先使用

常见对应关系：

- `brief-project`：优先结合 `memory`，必要时补 `serena`
- `feature-backend` / `feature-fullstack`：优先结合 `serena`，涉及框架细节时补 `context7`
- `debug-smart` / `review-full` / `audit-general`：优先结合 `serena`
- `migration-upgrade`：优先结合 `context7` 与 `serena`
- `status-overview`：优先结合 `memory`

这些能力属于流程增强层，不是新的 command。

更细的使用边界、多 subagent 上下文治理与 `memory` 写入规则以 `tooling-context-governance.md` 为准。

---

## 八、推荐的最小使用顺序

### 如果你是第一次使用 Kilo

按下面顺序判断：

1. 这是起盘、开发、调试、审查、安全、迁移，还是专项能力？
2. 能否直接落入已有 command？
3. 如果不能，再点某个 agent 做单点任务
4. 如需实际改文件，再进入可写执行模式

### 简化版口诀

- 起手：`brief-project`
- 状态：`status-overview`
- 起盘：`scaffold-project`
- 后端：`feature-backend`
- 全栈：`feature-fullstack`
- 调试：`debug-smart`
- 审计：`audit-general`
- 审查：`review-full`
- 安全：`security-hardening`
- 测试驱动：`tdd-cycle`
- 可观测性：`observability-review`
- 升级迁移：`migration-upgrade`
- Mock：`api-mock`
- 灵感：`meigen-find`

---

## 九、文档维护建议

后续如果新增或删除，应同步更新本文档中的：

- 能力地图
- 场景分流
- 快速选型表

保证使用文档与实际入口一致，避免文档先行漂移。
