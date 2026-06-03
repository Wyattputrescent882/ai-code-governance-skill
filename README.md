# AI Code Governance Skill

Make Codex, Claude Code, Cursor, and other AI coding agents behave more like maintainers: search before writing, reuse existing architecture, avoid duplicate implementations, control dependencies, and verify every change.

AI coding agents are powerful, but without project-level rules they often create a second `request.ts`, another modal component, another validator, another state store, or a large one-off implementation that nobody wants to maintain. This skill gives them a practical maintainer workflow.

## What It Does

- Forces search-before-write behavior.
- Makes agents reuse existing components, hooks, services, stores, utils, types, and design tokens.
- Blocks unapproved dependency changes.
- Works for both new projects and existing projects adopted midstream.
- Provides `AGENTS.md`, `CLAUDE.md`, `CODEX.md`, and project governance templates.
- Requires verification and a clear change report after implementation.

## Before / After

```text
Before
User: Add a payment popup.
AI: Creates PaymentModal.tsx, paymentRequest.ts, usePaymentState.ts,
    another loading component, and edits package.json for a new UI library.

After
User: Add a payment popup.
AI: Reads AGENTS.md and project-index.md, finds AppModal, usePayment,
    payment.service.ts, and LoadingState, then extends the existing flow
    with a small scoped change and runs the configured checks.
```

## Install For Codex

Install as a personal skill:

macOS / Linux:

```bash
mkdir -p ~/.codex/skills/ai-code-governance
cp -R SKILL.md agents templates prompts snippets LICENSE ~/.codex/skills/ai-code-governance/
```

Windows PowerShell:

```powershell
$source = "C:\path\to\ai-code-governance-skill"
$dest = "$env:USERPROFILE\.codex\skills\ai-code-governance"
New-Item -ItemType Directory -Force $dest
Copy-Item "$source\SKILL.md", "$source\agents", "$source\templates", "$source\prompts", "$source\snippets", "$source\LICENSE" -Destination $dest -Recurse -Force
```

Restart Codex after installation so the new skill is discovered.

## Install For Claude Code

Install as a personal Claude Code skill:

macOS / Linux:

```bash
mkdir -p ~/.claude/skills/ai-code-governance
cp -R SKILL.md templates prompts snippets LICENSE ~/.claude/skills/ai-code-governance/
```

Windows PowerShell:

```powershell
$source = "C:\path\to\ai-code-governance-skill"
$dest = "$env:USERPROFILE\.claude\skills\ai-code-governance"
New-Item -ItemType Directory -Force $dest
Copy-Item "$source\SKILL.md", "$source\templates", "$source\prompts", "$source\snippets", "$source\LICENSE" -Destination $dest -Recurse -Force
```

Install as a project-level Claude Code skill:

macOS / Linux:

```bash
mkdir -p .claude/skills/ai-code-governance
cp -R SKILL.md templates prompts snippets .claude/skills/ai-code-governance/
```

Windows PowerShell:

```powershell
$source = "C:\path\to\ai-code-governance-skill"
$dest = ".claude\skills\ai-code-governance"
New-Item -ItemType Directory -Force $dest
Copy-Item "$source\SKILL.md", "$source\templates", "$source\prompts", "$source\snippets" -Destination $dest -Recurse -Force
```

Project-level installation is best for team repos. Personal installation is best when you want the same governance workflow available everywhere.

## Use In An Existing Project

Do not copy templates and pretend they describe the project. Ask the agent to audit the real codebase first.

```text
Use ai-code-governance to adopt AI coding governance in this existing repo.

First inspect the real project structure, package scripts, request layer,
components, hooks, services, stores, utils, types, styles, and tests.

Then create or update:
- AGENTS.md
- CLAUDE.md
- CODEX.md
- docs/architecture.md
- docs/project-index.md
- docs/dependency-policy.md
- docs/coding-standards.md
- docs/agent-workflows.md

Do not keep template examples as facts. Mark unknowns as TBD or needs confirmation.
Do not modify package.json or lockfiles without approval.
```

Expected result:

```text
Adoption report
- Created AGENTS.md, CLAUDE.md, CODEX.md
- Added docs/project-index.md with real reusable modules
- Found existing request wrapper: src/services/request.ts
- Found existing modal component: src/components/base/AppModal.tsx
- Found existing validation utilities: src/utils/validators.ts
- Unknown: duplicate-code checker is not configured yet
- No dependency changes
```

## Use During Normal Feature Work

```text
Use ai-code-governance for this task.

Task: Add export CSV support to the orders page.

Requirements:
1. Read project rules first.
2. Search for existing export, file download, table, order service, and formatter logic.
3. Reuse existing modules when possible.
4. Do not add dependencies unless approved.
5. If I did not ask for plan-only mode, implement the smallest safe change and run checks.
```

Expected behavior:

```text
The agent searches for existing CSV/export utilities, reuses the order service
and table patterns, avoids adding a new CSV library if the project already has
formatting helpers, runs configured checks, and reports exactly what changed.
```

## Repository Contents

```text
ai-code-governance-skill/
  SKILL.md                         Skill instructions
  README.md                        Public documentation
  agents/
    openai.yaml                    Codex UI metadata
  templates/
    AGENTS.md                      Shared agent rules
    CLAUDE.md                      Claude Code project entry point
    CODEX.md                       Codex project entry point
    docs/
      architecture.md              Architecture contract template
      project-index.md             Reusable module index template
      dependency-policy.md         Dependency governance template
      coding-standards.md          Coding standards template
      agent-workflows.md           Agent workflow template
      review-checklist.md          Review checklist template
      task-template.md             Task prompt template
  prompts/
    preflight.md                   Search-before-write prompt
    implementation.md              Feature implementation prompt
    refactor.md                    Deduplication/refactor prompt
    review.md                      Review prompt
  snippets/
    package-json-scripts.json      Optional quality-check scripts
    jscpd.json                     Duplicate-code checker example
```

## Recommended Checks

Use the checks your project already has. Common examples:

```bash
npm run lint
npm run typecheck
npm run test
npm run dupcheck
npm run unused
npm run check
```

Useful tools:

- ESLint for static checks.
- TypeScript or `vue-tsc` for type checks.
- Vitest or Jest for tests.
- `jscpd` for duplicate-code detection.
- `knip` for unused files and exports.
- `depcheck` for unused dependencies.

## 中文说明

这是一个用于约束 Codex、Claude Code、Cursor、Copilot Workspace 等 Coding Agent 的治理型 skill。它的目标不是让 AI 多写代码，而是让 AI 在项目规则内少写、复用、去重、验证，避免生成重复逻辑和不可维护代码。

它适用于两种情况：

- 新项目启动时建立 AI 编码规范。
- 已有项目进行到一半时，再补充 AI 编码治理、项目索引、依赖规则和 Agent 工作流。

### 解决什么问题

当 Coding Agent 没有项目级约束时，经常会出现：

- 同一个功能生成多套实现。
- 重复创建 request、date、storage、validator 等工具。
- 弹窗、按钮、Loading、Empty 等组件越写越多。
- 页面里塞满业务逻辑。
- 随意新增依赖。
- 一次性生成过大功能，后续无法维护。
- 代码量暴涨，但项目稳定性下降。

本 skill 增加四层护栏：

1. 生成前约束：先检索、先理解项目、先规划。
2. 生成中约束：复用既有组件、hooks、services、stores、utils、types。
3. 生成后校验：lint、typecheck、test、重复代码检测、未使用代码检测。
4. 知识反哺：把架构决策、依赖约束、review 反馈沉淀回项目规则。

### 项目中途接入流程

不要把模板直接复制成事实。已有项目中途接入时，让 Agent 先审计真实项目，再生成或更新规则文件。

推荐流程：

1. 读取 `README`、package/build/test 配置、源码目录和已有规范文件。
2. 盘点真实的 request 层、组件库、hooks、services、stores、utils、types、设计 token、测试命令。
3. 创建或更新 `AGENTS.md`、`CLAUDE.md`、`CODEX.md`。
4. 创建或更新 `docs/architecture.md`、`docs/project-index.md`、`docs/dependency-policy.md`、`docs/coding-standards.md`、`docs/agent-workflows.md`。
5. 把模板里的示例路径替换为真实路径；未知项标记为 `TBD` 或 `needs confirmation`。
6. 不经确认，不修改 `package.json` 或 lockfile。
7. 输出接入报告：新增/修改文件、已发现可复用模块、未知项、建议补充的检查命令。

### 最小提示词

```text
使用 ai-code-governance 规范处理本任务。

任务：{填写任务}

要求：
1. 先阅读项目规则文件。
2. 先搜索现有实现。
3. 优先复用已有组件、Hook、Service、Store、Utils、Types。
4. 禁止新增重复实现。
5. 禁止新增依赖，除非先获得确认。
6. 禁止修改无关文件。
7. 如我没有要求只输出计划，请在完成必要盘点后直接实施最小变更并运行检查。
```

## Contributing

Issues and pull requests are welcome. Good contributions include:

- Better examples for real Codex or Claude Code projects.
- More project adoption templates.
- Governance patterns for Python, frontend, mobile, and monorepos.
- Improved checks for duplicate logic and dependency drift.

If this skill prevents even one duplicate implementation in your AI-assisted project, a star helps other developers find it.

## License

MIT
