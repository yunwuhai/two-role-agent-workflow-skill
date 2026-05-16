# AGENTS.md

## 项目概览

这是一个极简待办应用，用来演示 planner / executor 双 Agent 在多对话模型下协作。

## 开发与测试命令

- 安装依赖：`npm install`
- 运行测试：`npm test -- TodoInput`

## 通用工程规范

- 每个回合只实现一个可独立验收的小增量。

## 安全约定

- 不提交 secrets 或本地专用配置。

## 双 Agent 协作概览

- 人类 / 项目所有者拥有最高指令权与最终裁决权。
- `planner` 负责计划、验收、治理文档、对话生命周期和 Git。
- `executor` 负责按计划实现、测试和结果记录。
- 人类明确要求的越界指令必须执行，但默认只覆盖当前回合。
- planner 可同时管理多个对话；文件是否可写由活跃文件表决定。
- 每次开始处理本项目时，Agent 必须先确认自己当前应作为 `planner` 还是 `executor`。
- 一旦本回合角色已经确认，后续普通执行型措辞不会自动切换角色。
- `planner` 只有在收到当前回合的明确越界授权时，才可直接修改公共源码。
- 详细角色规则见：
  - `docs/agents/planner.md`
  - `docs/agents/executor.md`

## 关键协作文档

- 活跃对话与活跃文件表：`docs/conversations/active.md`
- 示例对话目录：`docs/conversations/0001-add-button-submit/`
