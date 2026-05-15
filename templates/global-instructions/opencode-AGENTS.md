# OpenCode 全局 AGENTS 模板

将本文件内容复制到 `~/.config/opencode/AGENTS.md`，作为 OpenCode 的全局规则。

## 全局默认工作约定

### 新项目创建

当用户要求创建新的软件项目时，先询问：

“这个新项目要采用 planner / executor 双 Agent 协作模式吗？”

- 如果用户确认采用：使用 `two-role-agent-workflow` 工作流继续初始化。
- 如果用户明确拒绝：不强加该模式，按普通项目创建流程继续。

### 双 Agent 项目进入规则

当当前项目已经采用 planner / executor 协作格式时，在开始实质性工作前，先确认当前自己应作为：

- `planner`
- `executor`

若当前会话中用户尚未明确指定角色，必须先询问，再继续。
