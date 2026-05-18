# 问题跟踪器：本地 Markdown

此仓库的 Issue 和 PRD 作为 `.scratch/` 中的 markdown 文件存在。

## 约定

- 每个功能一个目录：`.scratch/<feature-slug>/`
- PRD 是 `.scratch/<feature-slug>/PRD.md`
- 实现 Issue 是 `.scratch/<feature-slug>/issues/<NN>-<slug>.md`，从 `01` 开始编号
- 分类状态记录在每个 Issue 文件顶部附近的 `Status:` 行中（参见 `triage-labels.md` 了解角色字符串）
- 评论和对话历史追加到文件底部 `## Comments` 标题下

## 当技能说"发布到问题跟踪器"

在 `.scratch/<feature-slug>/` 下创建一个新文件（根据需要创建目录）。

## 当技能说"获取相关工单"

读取引用路径上的文件。用户通常会直接传递路径或 Issue 编号。
