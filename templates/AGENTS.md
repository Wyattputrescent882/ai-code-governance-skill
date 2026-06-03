# AGENTS.md

本文件是项目级 AI 编码规则。所有 Coding Agent 在修改本项目代码前必须阅读并遵守，包括 Codex、Claude Code、Cursor、Copilot Workspace 等。

本文件适用于新项目，也适用于项目进行到一半后补充 AI 编码治理。

## 绝对原则

1. 修改前必须先搜索现有实现。
2. 优先复用现有目录、命名、组件风格、hooks、services、stores、utils、types。
3. 不允许重复实现已有函数、组件、Hook、Service、Store、Utils、Types。
4. 不允许为同一问题提供多套并行实现。
5. 不允许新增未经确认的依赖。
6. 每次任务只修改与需求直接相关的文件。
7. 新增公共函数或公共组件前，必须确认现有实现无法复用。
8. 禁止保留 mock、临时代码、备用方案、兼容方案、实验性实现，除非用户明确要求。
9. 禁止通过降低 lint、typecheck、test 规则来让检查通过。
10. 代码必须运行项目已有检查命令；未运行或命令不存在时必须如实说明。

## 项目中途接入规则

如果本文件是在项目过程中新增的，Agent 的下一步不是直接套模板，而是先完成接入审计：

1. 读取 `README`、package/build/test 配置、源码目录和已有规范文件。
2. 盘点真实的请求层、组件库、hooks、services、stores、utils、types、样式系统和测试命令。
3. 更新 `docs/project-index.md`，只写已确认存在的路径。
4. 更新 `docs/architecture.md`，记录当前项目真实分层。
5. 更新 `docs/dependency-policy.md`，记录已批准依赖和禁止重复方案。
6. 未确认的信息标记为 `TBD` 或 `needs confirmation`，不得猜测。

## 编码前必须阅读

如果存在，优先阅读：

- `docs/architecture.md`
- `docs/project-index.md`
- `docs/dependency-policy.md`
- `docs/coding-standards.md`
- `docs/agent-workflows.md`
- `CLAUDE.md`
- `CODEX.md`

## 默认执行流程

1. 理解需求。
2. 搜索现有实现。
3. 明确复用方案和最小修改范围。
4. 如果用户要求“先给计划”或任务涉及新增依赖、删除/迁移、大范围架构调整，先停在计划等待确认。
5. 其他情况下，完成必要盘点后直接实施最小变更。
6. 运行项目检查命令。
7. 清理重复和废弃逻辑。
8. 输出变更报告。

## 目录职责

按项目实际结构维护本节：

- `src/pages/`：页面层，只负责展示、路由和用户交互。
- `src/components/`：UI 组件。
- `src/hooks/`：组合逻辑 / composables。
- `src/services/`：API 调用、后端通信。
- `src/stores/`：全局状态。
- `src/utils/`：纯函数工具。
- `src/types/`：类型定义。
- `src/styles/`：样式变量、主题、公共样式。

如果项目目录与本节不同，以 `docs/architecture.md` 中记录的真实结构为准。

## 禁止事项

- 页面层禁止直接调用 `fetch`、`axios`、`uni.request`，除非项目架构明确允许。
- 页面层禁止写复杂业务逻辑。
- 组件禁止直接调用 API，除非它是项目认可的数据组件。
- Service 禁止依赖 UI。
- Utils 禁止依赖 Store 或 UI。
- 禁止硬编码颜色、字号、间距，除非项目没有样式系统且任务范围允许。
- 禁止修改无关文件。
- 禁止保留 unused import、dead code、mock 代码。

## 编码前计划应包含

- 需求理解。
- 已检索的现有实现。
- 复用方案。
- 修改文件列表。
- 新增文件列表。
- 是否新增依赖。
- 验证命令。
- 风险点。

## 编码后总结必须包含

- 修改了哪些文件。
- 新增了哪些文件。
- 删除了哪些重复逻辑。
- 复用了哪些已有实现。
- 是否新增依赖。
- 执行了哪些检查命令。
- 检查是否通过；未运行时说明原因。
- 后续建议。
