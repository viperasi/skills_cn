技能按照分类文件夹组织在 `skills/` 下：

- `engineering/` — 日常编码工作
- `productivity/` — 日常非编码工作流工具
- `misc/` — 保留但很少使用
- `personal/` — 与个人设置相关，不对外推广
- `in-progress/` — 尚未发布的草稿
- `deprecated/` — 已弃用

`engineering/`、`productivity/` 或 `misc/` 中的每个技能必须在顶层 `README.md` 中有引用，并在 `.claude-plugin/plugin.json` 中有条目。`personal/`、`in-progress/` 和 `deprecated/` 中的技能不得出现在这两者中。

顶层 `README.md` 中的每个技能条目必须将技能名称链接到其 `SKILL.md`。

每个分类文件夹都有一个 `README.md`，列出该分类中的每个技能及其一行描述，技能名称链接到其 `SKILL.md`。
