# Matt Pocock 技能集

一组由 Claude Code 加载的智能体技能（斜杠命令和行为）。技能按分类组织，由 `/setup-matt-pocock-skills` 生成的按仓库配置来使用。

## 领域语言

**问题跟踪器**：
托管仓库 Issues 的工具——GitHub Issues、Linear、本地 `.scratch/` markdown 约定或类似工具。像 `to-issues`、`to-prd`、`triage` 和 `qa` 这样的技能会读写它。
_避免使用_：backlog manager、backlog backend、issue host

**Issue**：
**问题跟踪器**中一个被跟踪的工作单元——由 `to-issues` 生成的 bug、任务、PRD 或切片。
_避免使用_：ticket（仅在引用称其为 ticket 的外部系统时使用）

**分类角色**：
在分类过程中应用于 **Issue** 的标准状态机标签（如 `needs-triage`、`ready-for-afk`）。每个角色通过 `docs/agents/triage-labels.md` 映射到**问题跟踪器**中的实际标签字符串。

## 关系

- 一个**问题跟踪器**包含多个**Issue**
- 一个**Issue** 在同一时间携带一个**分类角色**

## 已标记的歧义

- "backlog" 之前既被用于指代托管 Issues 的*工具*，也被用于指代其中的*工作内容*——已解决：工具是**问题跟踪器**；"backlog" 不再作为领域术语使用。
- "backlog backend" / "backlog manager" —— 已解决：合并为**问题跟踪器**。
