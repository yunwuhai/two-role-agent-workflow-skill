# AGENTS.md

## 项目概览

这是一个极简待办应用，用来演示新版 planner / executor 双 Agent 协作模板。

## 开发与测试命令

- 安装依赖：`npm install`
- 运行测试：`npm test -- TodoInput`

## 通用工程规范

- 每回合只实现一个可独立验收的小增量。

## 安全约定

- 不提交 secrets 或本地专用配置。

## 双 Agent 协作概览

- 人类 / 项目所有者拥有最高指令权与最终裁决权。
- `planner` 负责计划、验收、治理文档、对话生命周期和 Git。
- `executor` 负责依据正式计划修改项目源码、运行测试并记录执行结果。
- 角色一旦在当前回合确认，普通执行型措辞不会自动切换角色。
- 人类明确要求的当前回合越界指令必须执行，但默认不会改写长期规则。
- 详细角色规则见：
  - `docs/agents/planner.md`
  - `docs/agents/executor.md`

## 关键协作文档

- 活跃对话与活跃文件表：`docs/conversations/active.md`
- 每个对话目录：`docs/conversations/<id>-<slug>/`
  - 当前计划：`plan.md`
  - 当前结果：`result.md`
  - 对话备忘录：`memo.md`
  - 回合历史：`history/`

## 示例阅读提示

- `0001-add-button-submit` 已完成，因此不再出现在活跃对话表中。
- `0002-enter-submit` 仍在执行，所以它继续持有本回合需要修改的两个文件。
