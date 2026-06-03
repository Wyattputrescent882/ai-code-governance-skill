# CLAUDE.md

Claude Code 在本项目中必须遵守 `AGENTS.md`。

@AGENTS.md

## Claude Code 使用规则

1. 优先按 `AGENTS.md` 的项目规则工作。
2. 每次任务开始时先搜索现有实现，再决定是否新增文件。
3. 如用户要求直接实现，在完成必要盘点后实施最小变更；不要为了等待计划确认而停住。
4. 如任务涉及新增依赖、删除/迁移、大范围重构、不可逆操作，先输出计划并等待确认。
5. 不要一次性重写大模块。
6. 不要生成多套可选实现。
7. 不要把业务逻辑塞进页面组件。
8. 不要随意创建新的 helper、utils、hooks。
9. 不要修改 lockfile，除非用户确认新增依赖。
10. 不要通过降低 lint / typecheck / test 规则来让检查通过。

## 项目中途接入

如果本文件是在已有项目中新增的，先审计真实项目，再更新 `docs/architecture.md`、`docs/project-index.md`、`docs/dependency-policy.md`、`docs/coding-standards.md`。模板示例只能作为占位，不能当成已确认事实。

## 每次完成后输出

```md
## 变更摘要

## 文件变更

## 复用情况

## 去重情况

## 依赖变更

## 校验结果

## 风险和后续建议
```
