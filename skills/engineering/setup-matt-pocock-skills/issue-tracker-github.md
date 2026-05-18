# 问题跟踪器：GitHub

此仓库的 Issue 和 PRD 作为 GitHub Issue 存在。对所有操作使用 `gh` CLI。

## 约定

- **创建一个 Issue**：`gh issue create --title "..." --body "..."`。对多行正文使用 heredoc。
- **读取一个 Issue**：`gh issue view <number> --comments`，通过 `jq` 过滤评论并获取标签。
- **列出 Issue**：`gh issue list --state open --json number,title,body,labels,comments --jq '[.[] | {number, title, body, labels: [.labels[].name], comments: [.comments[].body]}]'`，使用适当的 `--label` 和 `--state` 过滤器。
- **评论一个 Issue**：`gh issue comment <number> --body "..."`
- **应用/移除标签**：`gh issue edit <number> --add-label "..."` / `--remove-label "..."`
- **关闭**：`gh issue close <number> --comment "..."`

从 `git remote -v` 推断仓库——在克隆仓库内运行时 `gh` 会自动执行此操作。

## 当技能说"发布到问题跟踪器"

创建一个 GitHub Issue。

## 当技能说"获取相关工单"

运行 `gh issue view <number> --comments`。
