# AGENTS.md

## 项目概览

这是一个极简待办应用，用来演示 planner / executor 双 Agent 协作模板。

## 开发与测试命令

- 安装依赖：`npm install`
- 运行测试：`npm test -- TodoInput`

## 通用工程规范

- 每轮只实现一个可独立验收的小增量。

## 安全约定

- 不提交 secrets 或本地专用配置。

## 双 Agent 协作概览

- 人类 / 项目所有者拥有最高指令权与最终裁决权。
- `planner` 负责计划、验收、治理文档和 Git。
- `executor` 负责按计划实现、测试和结果记录。
- 人类明确要求的越界指令必须执行，但默认只覆盖当前轮次。
- 每次开始处理本项目时，Agent 必须先确认自己当前应作为 `planner` 还是 `executor`；若当前会话尚未明确，应先向人类询问，再继续后续工作。
- 一旦本轮角色已经确认，后续普通执行型措辞不会自动切换角色。若当前角色是 `planner`，普通实现请求默认应转化为交接，而不是直接修改公共源码。
- `planner` 只有在收到当前轮次的明确越界授权时，才可直接修改公共源码。
- 详细角色规则见：
  - `docs/agents/planner.md`
  - `docs/agents/executor.md`

## 关键协作文档

- 当前计划：`docs/planner/current_plan.md`
- 当前结果：`docs/executor/current_result.md`
