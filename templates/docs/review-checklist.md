# Review Checklist

用于人工 review 或 Agent 自检。

## 架构检查

- [ ] 是否遵守目录分层？
- [ ] 页面层是否只负责展示和交互？
- [ ] API 调用是否集中在 services？
- [ ] 状态是否集中在 stores / hooks？
- [ ] Utils 是否保持纯函数？

## 去重检查

- [ ] 是否重复实现已有组件？
- [ ] 是否重复实现已有 Hook？
- [ ] 是否重复实现已有 Service？
- [ ] 是否重复实现已有 Store？
- [ ] 是否重复实现已有 Utils？
- [ ] 是否重复定义类型？

## 依赖检查

- [ ] 是否新增依赖？
- [ ] 是否经过确认？
- [ ] 是否引入第二套方案？
- [ ] 是否修改 lockfile？

## 代码质量检查

- [ ] 是否存在 unused import？
- [ ] 是否存在 dead code？
- [ ] 是否存在 mock / 临时代码？
- [ ] 是否存在空 catch？
- [ ] 是否滥用 any？
- [ ] 是否硬编码样式？
- [ ] 文件是否过长？
- [ ] 函数是否过长？

## 验证检查

- [ ] lint 是否通过？
- [ ] typecheck 是否通过？
- [ ] test 是否通过？
- [ ] 重复代码检测是否通过？
- [ ] 未使用代码检测是否通过？

## 文档检查

- [ ] 是否更新 project-index.md？
- [ ] 是否更新 architecture.md？
- [ ] 是否更新 dependency-policy.md？
- [ ] 是否记录重要决策？
