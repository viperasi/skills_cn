---
name: setup-matt-pocock-skills
description: 在金 AGENTS.md/CLAUDE.md 中和 `docs/agents/` 中设置 `## Agent skills` 块，使工程技能知道此仓库的问题跟踪器（GitHub 或本地 markdown）、分类标签词汇和领域文档布局。在首次使用 `to-issues`、`to-prd`、`triage`、`diagnose`、`tdd`、`improve-codebase-architecture` 或 `zoom-out` 之前运行——或当这些技能似乎缺少关于问题跟踪器、分类标签或领域文档的上下文时运行。
disable-model-invocation: true
---

# 设置 Matt Pocock 的技能

搭建工程技能所假设的按仓库配置：

- **问题跟踪器** — Issue 存放的位置（默认 GitHub；也原生支持本地 markdown）
- **分类标签** — 用于五个规范分类角色的字符串
- **领域文档** — `CONTEXT.md` 和 ADR 存放的位置，以及读取它们的消费规则

这是一个提示驱动的技能，而非确定性脚本。探索、展示你发现的内容、与用户确认，然后写入。

## 流程

### 1. 探索

查看当前仓库以了解其起始状态。读取任何存在的东西；不要假设：

- `git remote -v` 和 `.git/config` — 这是 GitHub 仓库吗？哪个？
- 仓库根目录的 `AGENTS.md` 和 `CLAUDE.md` — 是否存在？其中是否已有 `## Agent skills` 部分？
- 仓库根目录的 `CONTEXT.md` 和 `CONTEXT-MAP.md`
- `docs/adr/` 和任何 `src/*/docs/adr/` 目录
- `docs/agents/` — 此技能之前的输出是否已存在？
- `.scratch/` — 本地 markdown 问题跟踪器约定已在使用的信号

### 2. 展示发现并询问

总结现有内容和缺失内容。然后**一次一个**地引导用户完成三个决策——展示一个部分，获取用户的答案，然后移至下一个。不要一次性抛出所有三个。

假设用户不知道这些术语意味着什么。每个部分以一个简短说明开头（它是什么，为什么这些技能需要它，如果他们选择不同的会有什么变化）。然后展示选择和默认值。

**A 部分 — 问题跟踪器。**

> 说明："问题跟踪器"是此仓库中 Issue 存放的地方。像 `to-issues`、`triage`、`to-prd` 和 `qa` 这样的技能会读写它——它们需要知道是调用 `gh issue create`，还是在 `.scratch/` 下写一个 markdown 文件，或者遵循你描述的其他工作流。选择你为此仓库实际跟踪工作的地方。

默认立场：这些技能是为 GitHub 设计的。如果一个 `git remote` 指向 GitHub，建议那个。如果一个 `git remote` 指向 GitLab（`gitlab.com` 或自托管主机），建议 GitLab。否则（或如果用户偏好），提供：

- **GitHub** — Issue 存在仓库的 GitHub Issues 中（使用 `gh` CLI）
- **GitLab** — Issue 存在仓库的 GitLab Issues 中（使用 [`glab`](https://gitlab.com/gitlab-org/cli) CLI）
- **本地 markdown** — Issue 作为此仓库中 `.scratch/<feature>/` 下的文件存在（适合单独项目或没有远程的仓库）
- **其他**（Jira、Linear 等）— 请用户用一段话描述工作流；技能将其记录为自由文本

**B 部分 — 分类标签词汇。**

> 说明：当 `triage` 技能处理一个传入的 Issue 时，它将其通过状态机移动——需要评估、等待报告者、可供 AFK 智能体认领、可供人工处理或不会修复。为此，它需要应用与你*实际配置的*字符串匹配的标签（或你的问题跟踪器中的等价物）。如果你的仓库已经使用不同的标签名称（例如用 `bug:triage` 代替 `needs-triage`），在此映射它们，这样技能就能应用正确的标签而不会创建重复项。

五个规范角色：

- `needs-triage` — 维护者需要评估
- `needs-info` — 等待报告者
- `ready-for-agent` — 完全指定，可供 AFK 使用（智能体可以在没有人类上下文的情况下认领）
- `ready-for-human` — 需要人类实现
- `wontfix` — 不会被处理

默认：每个角色的字符串等于其名称。询问用户是否想要覆盖任何角色。如果他们的问题跟踪器没有现有标签，默认值就可以。

**C 部分 — 领域文档。**

> 说明：某些技能（`improve-codebase-architecture`、`diagnose`、`tdd`）读取 `CONTEXT.md` 文件以学习项目的领域语言，以及 `docs/adr/` 用于过去的架构决策。它们需要知道仓库具有一个全局上下文还是多个（例如一个具有独立前端/后端上下文的 monorepo），这样它们就能在正确的地方查看。

确认布局：

- **单上下文** — 一个 `CONTEXT.md` + `docs/adr/` 在仓库根目录。大多数仓库如此。
- **多上下文** — 根目录有 `CONTEXT-MAP.md`，指向每个上下文的 `CONTEXT.md` 文件（通常是 monorepo）。

### 3. 确认和编辑

向用户展示草稿：

- 要添加到正在编辑的 `CLAUDE.md` / `AGENTS.md` 中的 `## Agent skills` 块（见步骤 4 的选择规则）
- `docs/agents/issue-tracker.md`、`docs/agents/triage-labels.md`、`docs/agents/domain.md` 的内容

让他们在写入之前编辑。

### 4. 写入

**选择要编辑的文件：**

- 如果 `CLAUDE.md` 存在，编辑它。
- 否则如果 `AGENTS.md` 存在，编辑它。
- 如果两者都不存在，询问用户要创建哪一个——不要替他们选。

当 `CLAUDE.md` 已存在时，永远不要创建 `AGENTS.md`（反之亦然）——总是编辑已存在的那个。

如果所选文件中已存在 `## Agent skills` 块，原地更新其内容而不是追加重复项。不要覆盖用户对周围部分的编辑。

块内容：

```markdown
## Agent skills

### 问题跟踪器

[Issue 跟踪位置的一句话摘要]。详见 `docs/agents/issue-tracker.md`。

### 分类标签

[标签词汇的一句话摘要]。详见 `docs/agents/triage-labels.md`。

### 领域文档

[布局的一句话摘要——"单上下文"或"多上下文"]。详见 `docs/agents/domain.md`。
```

然后以此技能文件夹中的种子模板为起点写入三个文档文件：

- [issue-tracker-github.md](./issue-tracker-github.md) — GitHub 问题跟踪器
- [issue-tracker-gitlab.md](./issue-tracker-gitlab.md) — GitLab 问题跟踪器
- [issue-tracker-local.md](./issue-tracker-local.md) — 本地 markdown 问题跟踪器
- [triage-labels.md](./triage-labels.md) — 标签映射
- [domain.md](./domain.md) — 领域文档消费规则 + 布局

对于"其他"问题跟踪器，使用用户的描述从头写入 `docs/agents/issue-tracker.md`。

### 5. 完成

告诉用户设置已完成，哪些工程技能现在将从这些文件中读取。提及他们稍后可以直接编辑 `docs/agents/*.md`——只有在他们想要切换问题跟踪器或从头开始时，才需要重新运行此技能。
