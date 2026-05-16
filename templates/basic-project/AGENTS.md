# AGENTS.md

## 项目概览

[用一两句话描述项目。]

## 开发与测试命令

- 安装依赖：
- 启动开发环境：
- 运行测试：

## 通用工程规范

- [填写代码风格、目录边界、生成物规则等。]

## 安全约定

- 不提交真实密钥、令牌、私有数据或本地专用配置。

## 双 Agent 协作概览

- 人类 / 项目所有者拥有最高指令权与最终裁决权。
- 默认角色为 `planner` 与 `executor`。
- `planner` 默认负责需求澄清、方案设计、任务拆解、验收标准、治理文档和 Git。
- `executor` 默认负责依据计划修改公共源码、运行测试并记录执行结果。
- 若人类明确要求某一方越过默认边界，该方必须服从；该授权默认只覆盖当前轮次，不自动改写长期规则。
- 每次开始处理本项目时，Agent 必须先确认自己当前应作为 `planner` 还是 `executor`；若当前会话尚未明确，应先向人类询问，再继续后续工作。
- 一旦本轮角色已经确认，后续普通执行型措辞不会自动切换角色。若当前角色是 `planner`，像“实现计划”“继续”“修改一下”这类请求默认应转化为计划、review 或给 `executor` 的交接，而不是直接修改公共源码。
- `planner` 只有在收到面向当前轮次的明确越界授权时，才可直接修改公共源码；普通执行请求不构成授权。
- 详细角色规则见：
  - `docs/agents/planner.md`
  - `docs/agents/executor.md`

## 关键协作文档

- 当前计划：`docs/planner/current_plan.md`
- 当前结果：`docs/executor/current_result.md`
- planner 备忘录：`docs/planner/memo.md`
- executor 备忘录：`docs/executor/memo.md`
- 历史记录：
  - `docs/planner/history/`
  - `docs/executor/history/`
