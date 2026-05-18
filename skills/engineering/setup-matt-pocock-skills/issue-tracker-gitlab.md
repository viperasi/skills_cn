# 问题跟踪器：GitLab

此仓库的 Issue 和 PRD 作为 GitLab Issue 存在。对所有操作使用 [`glab`](https://gitlab.com/gitlab-org/cli) CLI。

## 约定

- **创建一个 Issue**：`glab issue create --title "..." --description "..."`。对多行描述使用 heredoc。传递 `--description -` 打开编辑器。
- **读取一个 Issue**：`glab issue view <number> --comments`。使用 `-F json` 获取机器可读输出。
- **列出 Issue**：`glab issue list -F json` 使用适当的 `--label` 过滤器。
- **评论一个 Issue**：`glab issue note <number> --message "..."`。GitLab 称评论为 "notes"。
- **应用/移除标签**：`glab issue update <number> --label "..."` / `--unlabel "..."`。多个标签可以用逗号分隔或重复标志。
- **关闭**：`glab issue close <number>`。`glab issue close` 不接受关闭评论，因此首先用 `glab issue note <number> --message "..."` 发布解释，然后关闭。
- **合并请求**：GitLab 称 PR 为"merge requests"。使用 `glab mr create`、`glab mr view`、`glab mr note` 等——与 `gh pr ...` 形状相同，用 `mr` 代替 `pr`，用 `note`/`--message` 代替 `comment`/`--body`。

从 `git remote -v` 推断仓库——在克隆仓库内运行时 `glab` 会自动执行此操作。

## 当技能说"发布到问题跟踪器"

创建一个 GitLab Issue。

## 当技能说"获取相关工单"

运行 `glab issue view <number> --comments`。
