# 实施计划：[功能名称]

**分支**: `[###-功能名称]` | **日期**: [日期] | **规格**: [链接]
**输入**: 来自 `/specs/[###-功能名称]/spec.md` 的功能规格

**注意**: 此模板由 `/speckit.plan` 命令填充。执行工作流程请参见 `.specify/templates/commands/plan.md`。

**ONES 集成**: 此模板包含强制性的 ONES 能力验证，确保所有 ONES 应用功能都基于官方平台能力。

## 摘要

[从功能规格中提取：主要需求 + 研究中的技术方法]

## 技术背景

**语言/版本**: TypeScript 5.x, Node.js 18+  
**主要依赖**: NestJS, TypeORM, ONES OpenAPI SDK, JWT  
**存储**: SQLite + ONES
**测试**: Jest, Supertest  
**目标平台**: ONES App (Linux 服务器)  

## 项目概览

<!--
  需要操作：将此部分的内容替换为项目的实现类型、范围、约束、规模。
  此处展示的结构仅供参考，用于指导迭代过程。
-->
**项目类型**: [自动化/系统集成/批处理/其他 - 确定项目类型]  
**性能目标**: [性能目标，例如：1000 req/s、10k lines/sec、60 fps 或需要澄清]  
**约束**: [领域特定，例如：<200ms p95、<100MB 内存或需要澄清]  
**规模/范围**: [领域特定，例如：10k 用户、1M LOC、50 个屏幕或需要澄清]


## 章程检查

*关卡：必须在阶段 0 研究之前通过。阶段 1 设计后重新检查。*

### ONES 能力验证（ONES 应用强制要求）

*在进行任何设计或开发工作之前，完成 ONES 能力验证。*

**能力映射要求**:
- [ ] 已查阅 `/Users/malvin/Coding/appbuilder/ones-specs` 目录
- [ ] 已确定具体的事件类型（如 `ones:project:issue:updated`）
- [ ] 已确定具体的API端点（如 `PUT /openapi/v2/project/issues/{issueID}`）
- [ ] 已确定具体的字段ID（如 `field032` 对应故事点）
- [ ] 已确定具体的 oauth 权限范围（如 `read:project:issue`, `write:project:issue`）

**文档要求**:
- [ ] 已生成 `ones-capabilities.md` 文档
- [ ] 已更新 `research.md` 包含具体ONES能力信息
- [ ] 已更新 `contracts/openapi.yaml` 符合ONES规范

**验证要求**:
- [ ] 已运行能力校验脚本验证合规性
- [ ] 所有功能需求都映射到具体ONES能力
- [ ] 所有技术决策都基于官方文档
- [ ] 所有字段引用都使用正确ID
- [ ] 所有API调用都使用正确端点

### 仓库与技术栈约束（不可协商）
- [ ] 代码改动仅发生在 `my-new-project/` 目录
- [ ] 未引入新的技术栈/框架/运行时（沿用 NestJS、React+Vite、TypeORM、TypeScript、SQLite）
- [ ] 新增依赖已论证必要性、兼容性与安全性，并通过治理评审（如适用）
- [ ] 采用增量变更并保持向后兼容；破坏性变更附带迁移与影响评估（如适用）

**ONES 应用设计检查**: 
- [好的设计]用户操作是否完全在 ONES 界面内？
- [好的设计]在ONES原生界面操作触发的功能主要通过监听ONES事件并响应实现（而非自定义 API）？
- [好的设计]修改ONES中的数据通过调用 ONES OpenAPI 进行？
- [好的设计]是否优先使用 ONES App 扩展点？
- [坏的设计]如果需要创建用户需要调用的自定义 API，必须解释为什么绝对必要?

**详细 ONES 应用设计检查清单**（参考：`templates-zh/ones-app-design-checklist.zh.md`）：

### 核心设计原则
- [ ] 用户操作完全在 ONES 内
- [ ] 优先使用ONES App 功能扩展添加新的页面提供给用户使用
- [ ] 在ONES原生界面操作触发的功能主要通过监听ONES事件并响应实现（而非自定义 API）
- [ ] 修改ONES中的数据通过调用 ONES OpenAPI 进行
- [ ] 不创建重复 ONES 数据的存储

### 数据流设计
- [ ] 主要数据流1：用户操作 → ONES 事件 → App 处理 → ONES OpenAPI 调用
- [ ] 主要数据流2：用户操作 → App 页面 → ONES OpenAPI 调用
- [ ] 配置型数据流：用户操作 → App 页面 → App 自定义 API 调用 → App 存储
- [ ] 连接其他系统：用户操作 → App 页面 → App 自定义 API 调用 → 其他系统 API 调用
- [ ] 连接其他系统：其他系统 → App 自定义 API 调用 → ONES OpenAPI 调用

### 设计决策验证
- [ ] 功能是否可以通过监听 ONES 事件实现？
- [ ] 数据更新是否可以通过调用 ONES OpenAPI 完成？
- [ ] 创建自定义用户界面是否必要？
- [ ] 存储是否仅用于必要的审计或配置数据（不重复 ONES 数据）？

[基于章程文件确定的关卡]

## 项目结构

### 文档（此功能）

```
specs/[###-功能]/
├── plan.md              # 此文件（/speckit.plan 命令输出）
├── research.md          # 阶段 0 输出（/speckit.plan 命令）
├── ones-capabilities.md # ONES 能力映射（ONES 应用强制要求）
├── data-model.md        # 阶段 1 输出（/speckit.plan 命令）
├── quickstart.md        # 阶段 1 输出（/speckit.plan 命令）
├── contracts/           # 阶段 1 输出（/speckit.plan 命令）
│   └── openapi.yaml     # API 合约（必须符合 ONES 规范）
├── checklists/          # 质量检查清单
│   └── requirements.md  # 规格质量检查清单
└── tasks.md             # 阶段 2 输出（/speckit.tasks 命令 - 不由 /speckit.plan 创建）
```

### 源代码（仓库根目录-不可协商）

```
src/
├── dto/
├── entities/
├── services/
├── app.controller.ts
├── app.module.ts
└── main.ts

web/
├── src/
│   ├── components/
│   ├── pages/
│   └── services/

```

**结构决策**: 选择单一项目结构，因为这是ONES应用。

## 复杂性跟踪

*仅在章程检查有必须证明的违规时填写*

| 违规 | 为什么需要 | 拒绝更简单替代方案的原因 |
|------|------------|------------------------|
| [例如：第4个项目] | [当前需求] | [为什么3个项目不够] |
| [例如：Repository 模式] | [具体问题] | [为什么直接数据库访问不够] |

## ONES 能力验证错误

*仅在 ONES 能力验证失败时填写*

### 能力映射失败
- **错误**: [具体能力映射失败]
- **影响**: [这如何影响功能]
- **解决方案**: [如何解决或绕过]

### 文档失败  
- **错误**: [具体文档失败]
- **影响**: [这如何影响开发]
- **解决方案**: [如何解决]

### 验证失败
- **错误**: [具体验证失败]
- **影响**: [这如何影响合规性]
- **解决方案**: [如何解决]
