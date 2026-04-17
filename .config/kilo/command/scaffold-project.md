---
name: scaffold-project
description: 以新项目初始化为唯一目标，生成贴合技术栈的最小可运行目录、基础配置、开发脚本与验证骨架。
---

# 工作流目标

用于从零创建新项目或新子工程的基础骨架，确保目录、配置、依赖与验证入口具备统一起点。

## 模式要求

- 项目类型判断与技术栈收敛阶段可在只读模式进行
- 一旦进入目录创建、配置写入、示例实现生成与初始化脚本补齐阶段，应切换到可写执行模式
- 初始化验证如依赖本地安装、构建、测试与结果归档，应保持可写执行模式直到 workflow 收口完成

## Workflow

### 步骤 1：确定项目类型
- 明确语言、运行时、应用形态与是否需要单仓/多包结构
- 先判断项目属于后端服务、前端应用、库、CLI、任务型服务或混合仓库
- Python 场景进一步区分 API 服务、Django 类全栈项目、库、CLI、通用脚本工程
- Go 场景进一步区分 Fiber API、CLI、库、任务型服务与混合服务/命令工程
- JavaScript / TypeScript 场景进一步区分 SvelteKit 2 / Svelte 5 类前端、Node API、库、CLI
- 识别最小必需能力：构建、启动、测试、lint、type-check、环境配置、发布入口

### 步骤 2：生成目录骨架
- 创建与技术栈匹配的源码、测试、配置、脚本与文档目录
- 避免一次生成过多业务模块，只保留最小可演进结构
- Python 项目优先使用 `src/` 布局、`tests/`、`pyproject.toml` 与最小入口模块
- Go 项目优先生成 `cmd/`、`internal/`、`pkg/`、`configs/`、`migrations/`、`tests/` 与 `go.mod`
- TypeScript 项目优先生成 `src/`、`tests/`、`package.json`、`tsconfig.json` 与清晰的构建输出目录
- 服务型项目至少提供配置模块、健康检查入口与业务模块占位
- 前端项目至少提供页面或应用入口、基础组件目录、接口层或 `lib/` 目录与测试初始化文件
- SvelteKit 2 项目优先生成 `src/routes`、`src/lib`、基础 UI 组件目录与必要的 `+page` / `+layout` 入口
- Go Fiber 服务优先提供 `cmd/server`、`internal/app`、`internal/http`、`internal/config`、`internal/logging`、`internal/store` 等最小骨架
- Go CLI 项目优先提供 `cmd/root.go` 与按子命令拆分的 cobra 结构

### 步骤 3：补齐工程基线
- 配置依赖管理、格式检查、类型检查、测试工具与基础忽略规则
- 提供环境变量样例、启动脚本和最小健康检查入口
- Python 默认优先考虑 `pyproject.toml`、`ruff`、`pytest`，按项目情况补充 `pytest-asyncio`、类型检查工具
- Go 默认优先考虑 `go 1.25.0`、`gofmt`、`go test`、`go build`，按项目情况补充生成命令与数据库代码生成入口
- Go Fiber 场景可按需纳入 `github.com/gofiber/fiber/v3`、`github.com/spf13/cobra`、`github.com/spf13/viper`
- 若用户明确要求高性能 JSON 与日志替换，可纳入 `mailru/easyjson`、Zap + Lumberjack，并在脚手架中预留初始化位置
- PostgreSQL 场景可按需纳入 `sqlc`、`ent`、`pgx`、`vito` 与 `go-sqlmock`，但只生成最小必要基线
- TypeScript 默认优先考虑严格 `tsconfig`、lint、Vitest 或 Jest，并提供 `type-check` 脚本
- 依赖选择遵循标准库优先、成熟生态优先，不为脚手架引入冷门工具
- 基础脚本名称尽量统一为 `dev`、`build`、`test`、`lint`、`type-check`
- Svelte 前端场景可按需纳入 Tailwind CSS v4、`lucide-svelte`、`layerchart`、`Shadcn-svelte`，但只在项目需求明确时生成

### 步骤 4：写入示例实现
- 添加最小可运行示例，如健康检查、示例路由、基础命令或占位模块
- 示例必须体现推荐结构，但不替代真实业务设计
- Python API 可提供最小路由与设置读取；Django 类项目可提供 app 占位与基础配置分层
- Go Fiber API 可提供最小健康检查、错误处理中间件、配置读取、Zap 日志初始化与 PostgreSQL store 占位
- Go CLI 场景应优先体现 Cobra 根命令、子命令注册与 Viper 配置绑定
- Go 数据访问示例应预留 `sqlc` 查询、`ent` 实体或 schema、`pgx` 连接池与 `go-sqlmock` 测试样例位置
- Node / TypeScript API 可提供 `createApp`、路由入口、错误处理中间件占位与配置解析
- 前端项目可提供最小页面、组件与数据请求封装示例，但避免堆砌 UI
- SvelteKit 2 场景下示例应优先体现 `load`、表单 action、`src/lib` 复用边界与基础组件组合方式
- 库项目只提供单一导出与对应测试，CLI 项目只提供一个最小命令

### 步骤 5：执行初始化验证
- 验证安装、构建、启动或测试命令至少有一条能通过
- 记录缺失前提，如本地工具链、包管理器或系统依赖
- 优先执行最能反映脚手架健康度的命令组合，如 `lint`、`type-check`、`test`、`build`
- 若工具链缺失，明确记录未验证项与所需前提，不伪造通过结果

### 步骤 6：输出脚手架边界
- 输出生成目录树、关键配置说明、后续第一步开发建议与未包含内容
- 明确该 workflow 只负责“起盘”，不承担完整功能实现

## 通用脚手架约束

- 只生成高频、工程相关、边界清晰的基础文件，避免预置过多业务模块
- 目录设计优先贴合项目现有风格或目标技术栈主流惯例，不混搭多套模式
- 默认保留最小改动面，允许后续按架构方案继续扩展
- 不为 FastAPI、Django、Fiber、Node、SvelteKit 单独拆 workflow，只在项目类型判断中给出场景化骨架

## 产出清单

- 目录结构与关键文件列表
- 依赖与工具选择说明
- 启动、测试、lint、type-check、build 入口
- 环境变量样例与配置边界
- 已验证命令、未验证前提与后续第一步建议
