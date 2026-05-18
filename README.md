<p>
  <a href="https://www.aihero.dev/s/skills-newsletter">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skills-repo-dark_2x.png">
      <source media="(prefers-color-scheme: light)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skill-repo-light_2x.png">
      <img alt="Skills" src="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skill-repo-light_2x.png" width="369">
    </picture>
  </a>
</p>

# 真正工程师的技能集

[![skills.sh](https://skills.sh/b/mattpocock/skills)](https://skills.sh/mattpocock/skills)

我每天都在使用的智能体技能，用于真正的工程开发——而不是随心所欲地敲代码。

开发真正的应用程序是困难的。像 GSD、BMAD 和 Spec-Kit 这样的方法试图通过掌控流程来提供帮助。但这样做会剥夺你的控制权，并且使得过程中出现的 bug 难以解决。

这些技能被设计得小巧、易于适应且可组合。它们可以与任何模型配合使用。它们基于数十年的工程经验。随意修改它们，让它们成为你自己的工具，尽情享用。

如果你想跟踪这些技能的更新，以及我创建的任何新技能，你可以和大约 60,000 名其他开发者一起订阅我的 Newsletter：

[订阅 Newsletter](https://www.aihero.dev/s/skills-newsletter)

## 快速开始（30 秒设置）

1. 运行 skills.sh 安装器：

```bash
npx skills@latest add mattpocock/skills
```

2. 选择你想要的技能，以及你想在哪些编码智能体上安装它们。**确保选中 `/setup-matt-pocock-skills`**。

3. 在你的智能体中运行 `/setup-matt-pocock-skills`。它将：
   - 询问你想使用哪个问题跟踪器（GitHub、Linear 或本地文件）
   - 询问你在分类 Issue 时应用哪些标签（`/triage` 使用标签）
   - 询问你想在哪里保存我们创建的任何文档

4. 开始使用。

## 这些技能存在的原因

我构建这些技能是为了解决我在 Claude Code、Codex 和其他编码智能体中看到的常见失败模式。

### #1：智能体没有按照我的意愿行事

> "没有人确切知道自己想要什么"
>
> David Thomas & Andrew Hunt，《程序员修炼之道》

**问题**：软件开发中最常见的失败模式是理解偏差。你以为开发者知道你想要什么，然后你看到他们构建的东西——你才意识到它根本没理解你。

这在 AI 时代也是一样的。你与智能体之间存在沟通鸿沟。解决方法是进行一次**盘问会话**——让智能体就你要构建的内容向你提出详细问题。

**解决方案**是使用：

- [`/grill-me`](./skills/productivity/grill-me/SKILL.md) — 用于非编码场景
- [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md) — 与 [`/grill-me`](./skills/productivity/grill-me/SKILL.md) 相同，但增加了更多好功能（见下文）

这些是我最受欢迎的技能。它们帮助你在开始之前与智能体对齐，并深入思考你要做的变更。_每次_你想要做变更时都使用它们。

### #2：智能体过于啰嗦

> 有了通用语言，开发者之间的对话以及代码的表达都源自同一个领域模型。
>
> Eric Evans，《领域驱动设计》

**问题**：在项目开始时，开发者和他们要为其构建软件的人（领域专家）通常说着不同的语言。

我在与智能体协作时感受到了同样的紧张感。智能体通常被丢进一个项目里，被要求边做边理解行话，所以他们会用 20 个词来表达用 1 个词就能说清楚的事。

**解决方案**是建立一种共享语言。这是一个帮助智能体解读项目中行话的文档。

<details>
<summary>
示例
</summary>

以下是我的 `course-video-manager` 仓库中的一个 [`CONTEXT.md`](https://github.com/mattpocock/course-video-manager/blob/076a5a7a182db0fe1e62971dd7a68bcadf010f1c/CONTEXT.md) 示例。哪一个更容易阅读？

- **之前**："课程中某一节的一课被设为'真实'（即在文件系统中被赋予一个位置）时出现问题"
- **之后**："物化级联有问题"

这种简洁在一次又一次的会话中都能带来好处。

</details>

这个功能内置于 [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md) 中。它是一个盘问会话，但能帮助你在与 AI 之间建立共享语言，并将难以解释的决策记录在 ADR 中。

很难解释这有多强大。它可能是这个仓库中最酷的技巧。试试看。

> [!TIP]
> 共享语言除了减少啰嗦之外还有许多其他好处：
>
> - **变量、函数和文件命名一致**，使用共享语言
> - 因此，**代码库对智能体来说更容易导航**
> - 智能体也会**在思考上花费更少的 token**，因为它可以使用更简洁的语言

### #3：代码无法运行

> "始终保持小而审慎的步伐。反馈频率是你的速度限制。永远不要承担太大的任务。"
>
> David Thomas & Andrew Hunt，《程序员修炼之道》

**问题**：假设你和智能体就构建什么达成了共识。当智能体仍然产生糟糕的代码时，会发生什么？

是时候审视你的反馈循环了。如果对它生成的代码实际运行情况没有反馈，智能体就是在盲目飞行。

**解决方案**：你需要常规的那套反馈循环：静态类型、浏览器访问和自动化测试。

对于自动化测试，红-绿-重构循环至关重要。这是指智能体先写一个失败的测试，然后修复测试。这有助于为智能体提供持续的反馈，从而产生好得多的代码。

我构建了一个 **[`/tdd`](./skills/engineering/tdd/SKILL.md) 技能**，可以嵌入到任何项目中。它鼓励红-绿-重构，并为智能体提供了关于什么是好测试和坏测试的大量指导。

对于调试，我也构建了一个 **[`/diagnose`](./skills/engineering/diagnose/SKILL.md)** 技能，将最佳调试实践封装在一个简单的循环中。

### #4：我们构建了一团乱麻

> "每天都要投资于系统的设计。"
>
> Kent Beck，《解析极限编程》

> "最好的模块是深的。它们允许通过简单的接口访问大量功能。"
>
> John Ousterhout，《软件设计的哲学》

**问题**：大多数使用智能体构建的应用复杂且难以修改。因为智能体可以极大地加速编码，它们也加速了软件的熵增。代码库以前所未有的速度变得复杂。

**解决方案**是一种全新的 AI 驱动开发方法：关心代码的设计。

这内建于这些技能的每一层：

- [`/to-prd`](./skills/engineering/to-prd/SKILL.md) 在创建 PRD 之前询问你将涉及哪些模块
- [`/zoom-out`](./skills/engineering/zoom-out/SKILL.md) 告诉智能体在整个系统的背景下解释代码

最关键的是，[`/improve-codebase-architecture`](./skills/engineering/improve-codebase-architecture/SKILL.md) 帮助你将一团乱麻的代码库解救出来。我建议每几天在你的代码库上运行一次。

### 总结

软件工程的基本功比以往任何时候都更重要。这些技能是我将这些基本功浓缩为可重复实践的最佳努力，帮助你交付职业生涯中最好的应用。尽情享用。

## 参考目录

### 工程类

我每天用于编码工作的技能。

- **[diagnose](./skills/engineering/diagnose/SKILL.md)** — 针对疑难 bug 和性能回归的规范化诊断循环：复现 → 最小化 → 假设 → 插桩 → 修复 → 回归测试。
- **[grill-with-docs](./skills/engineering/grill-with-docs/SKILL.md)** — 盘问会话，将你的计划与现有领域模型进行对质、精炼术语，并即时更新 `CONTEXT.md` 和 ADR。
- **[triage](./skills/engineering/triage/SKILL.md)** — 通过分类角色状态机对 Issue 进行分类处理。
- **[improve-codebase-architecture](./skills/engineering/improve-codebase-architecture/SKILL.md)** — 在代码库中寻找深化机会，以 `CONTEXT.md` 中的领域语言和 `docs/adr/` 中的决策为指导。
- **[setup-matt-pocock-skills](./skills/engineering/setup-matt-pocock-skills/SKILL.md)** — 搭建按仓库的配置（问题跟踪器、分类标签词汇、领域文档布局），供其他工程技能使用。在首次使用 `to-issues`、`to-prd`、`triage`、`diagnose`、`tdd`、`improve-codebase-architecture` 或 `zoom-out` 之前按仓库运行一次。
- **[tdd](./skills/engineering/tdd/SKILL.md)** — 带有红-绿-重构循环的测试驱动开发。一次一个垂直切片地构建功能或修复 bug。
- **[to-issues](./skills/engineering/to-issues/SKILL.md)** — 将任何计划、规格或 PRD 拆分为可使用垂直切片独立认领的 GitHub Issue。
- **[to-prd](./skills/engineering/to-prd/SKILL.md)** — 将当前对话上下文转换为 PRD 并作为 GitHub Issue 提交。不需要面谈——只是综合你已经讨论过的内容。
- **[zoom-out](./skills/engineering/zoom-out/SKILL.md)** — 告诉智能体放远视野，为不熟悉的代码段提供更广泛的上下文或更高层次的视角。
- **[prototype](./skills/engineering/prototype/SKILL.md)** — 构建一个一次性原型来充实设计——要么是一个可运行的终端应用用于状态/业务逻辑问题，要么是通过一个路由可切换的多个截然不同的 UI 变体。

### 生产力类

通用工作流工具，不限于编码。

- **[caveman](./skills/productivity/caveman/SKILL.md)** — 超压缩沟通模式。通过去掉填充词将 token 使用量降低约 75%，同时保持完整的技术准确性。
- **[grill-me](./skills/productivity/grill-me/SKILL.md)** — 就计划或设计接受无情的面试，直到决策树的每个分支都得到解决。
- **[handoff](./skills/productivity/handoff/SKILL.md)** — 将当前对话压缩成交接文档，以便另一个智能体可以继续工作。
- **[write-a-skill](./skills/productivity/write-a-skill/SKILL.md)** — 创建具有正确结构、渐进披露和配套资源的新技能。

### 杂项

保留但很少使用的工具。

- **[git-guardrails-claude-code](./skills/misc/git-guardrails-claude-code/SKILL.md)** — 设置 Claude Code 钩子以在执行前阻止危险的 git 命令（push、reset --hard、clean 等）。
- **[migrate-to-shoehorn](./skills/misc/migrate-to-shoehorn/SKILL.md)** — 将测试文件从 `as` 类型断言迁移到 @total-typescript/shoehorn。
- **[scaffold-exercises](./skills/misc/scaffold-exercises/SKILL.md)** — 创建练习目录结构，包括章节、问题、解决方案和说明。
- **[setup-pre-commit](./skills/misc/setup-pre-commit/SKILL.md)** — 使用 lint-staged、Prettier、类型检查和测试设置 Husky pre-commit 钩子。
