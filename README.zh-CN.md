<p>
  <a href="https://www.aihero.dev/s/skills-newsletter">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skills-repo-dark_2x.png">
      <source media="(prefers-color-scheme: light)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skill-repo-light_2x.png">
      <img alt="Skills" src="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skill-repo-light_2x.png" width="369">
    </picture>
  </a>
</p>

# 真正工程师用的 Skills

[![skills.sh](https://skills.sh/b/mattpocock/skills)](https://skills.sh/mattpocock/skills)

[English](./README.md)

我每天用来做真正工程的 agent skills——不是 vibe coding。

开发真正的应用很难。GSD、BMAD、Spec-Kit 这类方法试图通过接管流程来帮你。但这么做的同时，它们也夺走了你的控制权，让流程里的 bug 很难排查。

这些 skills 设计得小、好改、可组合。它们适配任何模型，基于数十年的工程经验。随便改，变成你自己的。享受这个过程。

想跟上这些 skills 的更新和新 skill，可以加入我的 newsletter（已有约 6 万开发者）：

[订阅 Newsletter](https://www.aihero.dev/s/skills-newsletter)

## 快速开始（30 秒搞定）

1. 运行 skills.sh 安装器：

```bash
npx skills@latest add mattpocock/skills
```

2. 选择你想要的 skills，以及要装到哪些 coding agent 上。**务必选中 `/setup-matt-pocock-skills`**。

3. 在 agent 里运行 `/setup-matt-pocock-skills`。它会：
   - 问你想用哪种 issue tracker（GitHub、Linear，或本地文件）
   - 问你 triage 工单时用哪些标签（`/triage` 会用到）
   - 问你希望把生成的文档存到哪里

4. 搞定——可以开工了。

## 为什么要有这些 Skills

我做这些 skills，是为了修复我在 Claude Code、Codex 和其他 coding agent 上常见的失败模式。

### #1：Agent 没按我想的做

> 「没有人真正知道自己到底想要什么。」
>
> David Thomas & Andrew Hunt，《[程序员修炼之道](https://www.amazon.co.uk/Pragmatic-Programmer-Anniversary-Journey-Mastery/dp/B0833F1T3V)》

**问题**。软件开发里最常见的失败模式是对齐失败。你以为开发知道你想要什么。然后你看到成品——才发现它完全没理解你。

AI 时代也一样。你和 agent 之间存在沟通鸿沟。解法是一次**审讯式对齐（grilling session）**——让 agent 就你要做的事向你问详细问题。

**解法**是用：

- [`/grill-me`](./skills/productivity/grill-me/SKILL.md) — 非代码场景
- [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md) — 与 [`/grill-me`](./skills/productivity/grill-me/SKILL.md) 相同，但多了一些能力（见下文）

这是我最受欢迎的 skills。它们帮你在动手前与 agent 对齐，并深入思考即将做的变更。**每次**要做变更时都用它们。

### #2：Agent 太啰嗦了

> 有了统一语言，开发者之间的对话与代码表达都源自同一个领域模型。
>
> Eric Evans，《[领域驱动设计](https://www.amazon.co.uk/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215)》

**问题**：项目初期，开发者和他们为之构建软件的人（领域专家）通常说着不同的语言。

我和 agent 之间也有同样的张力。Agent 通常被扔进一个项目，边做边猜行话。于是它们用 20 个词表达本来 1 个词就够的意思。

**解法**是共享语言。一份帮 agent 解码项目行话的文档。

<details>
<summary>
示例
</summary>

这是我的 `course-video-manager` 仓库里的 [`CONTEXT.md`](https://github.com/mattpocock/course-video-manager/blob/076a5a7a182db0fe1e62971dd7a68bcadf010f1c/CONTEXT.md) 示例。哪个更好读？

- **之前**：「当课程某个章节里的一节课被『实体化』（即在文件系统里分到一个位置）时会出问题」
- **之后**：「实体化级联出了问题」

这种简洁会在一次次会话里持续回报。

</details>

这内建在 [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md) 里。它是一次审讯式对齐，同时帮你与 AI 建立共享语言，并把难解释的决策记进 ADR。

很难说清这有多强。它可能是这个仓库里最酷的技术。试试看就知道了。

> [!TIP]
> 共享语言除了减少啰嗦，还有很多好处：
>
> - **变量、函数和文件命名一致**，都用共享语言
> - 因此，agent **更容易导航代码库**
> - agent 也**花更少 token 思考**，因为它有更简洁的语言可用

### #3：代码根本跑不通

> 「永远迈小而审慎的步子。反馈速率就是你的速度上限。永远不要接太大的任务。」
>
> David Thomas & Andrew Hunt，《[程序员修炼之道](https://www.amazon.co.uk/Pragmatic-Programmer-Anniversary-Journey-Mastery/dp/B0833F1T3V)》

**问题**：假设你和 agent 已经对齐了要做什么。那当 agent *仍然*产出垃圾时怎么办？

该看反馈环了。没有关于它所产代码实际如何运行的反馈，agent 就是在盲飞。

**解法**：你需要常见的那套反馈环：静态类型、浏览器访问，以及自动化测试。

对自动化测试来说，红-绿-重构循环至关重要。agent 先写一个失败的测试，再修到通过。这给 agent 稳定的反馈水平，从而产出好得多的代码。

我做了一个 **[`/tdd`](./skills/engineering/tdd/SKILL.md) skill**，可以塞进任何项目。它鼓励红-绿-重构，并给 agent 充分指导：什么是好测试、什么是坏测试。

调试方面，我也做了 **[`/diagnosing-bugs`](./skills/engineering/diagnosing-bugs/SKILL.md)** skill，把最佳调试实践包成一个简单循环。

### #4：我们造出了一团泥球

> 「*每天*投资于系统设计。」
>
> Kent Beck，《[解析极限编程](https://www.amazon.co.uk/Extreme-Programming-Explained-Embrace-Change/dp/0321278658)》

> 「最好的模块是深的。它们让大量功能能通过一个简单接口访问。」
>
> John Ousterhout，《[软件设计的哲学](https://www.amazon.co.uk/Philosophy-Software-Design-2nd/dp/173210221X)》

**问题**：大多数用 agent 建的应用又复杂又难改。因为 agent 能极大加速编码，它们也加速了软件熵。代码库以前所未有的速度变复杂。

**解法**是一种激进的新 AI 开发方式：在乎代码设计。

这内建在这些 skills 的每一层：

- [`/to-spec`](./skills/engineering/to-spec/SKILL.md) 在创建 spec 前会问你要动哪些模块

更关键的是，[`/improve-codebase-architecture`](./skills/engineering/improve-codebase-architecture/SKILL.md) 帮你拯救已经变成泥球的代码库。我建议每隔几天对代码库跑一次。

### 总结

软件工程基本功比以往任何时候都更重要。这些 skills 是我把这些基本功浓缩成可重复实践的尽力之作，帮你交付职业生涯里最好的应用。享受吧。

## 参考

这些 skills 按谁可以调用来分。**用户调用（User-invoked）** skills 只有你手动输入时才会触发（例如 `/grill-me`）；职责是编排流程。**模型调用（Model-invoked）** skills 既可以由你调用，也可以在任务匹配时由 agent 自动选用；它们承载可复用的纪律。用户调用 skill 可以调用模型调用 skill，但绝不会再调用另一个用户调用 skill。

### Engineering

我每天做代码工作时用的 skills。

**用户调用**

- **[ask-matt](./skills/engineering/ask-matt/SKILL.md)** — 询问哪个 skill 或流程适合你当前情况。本仓库用户调用 skills 的路由器。
- **[grill-with-docs](./skills/engineering/grill-with-docs/SKILL.md)** — 审讯式对齐，同时构建项目的领域模型，打磨术语，并就地更新 `CONTEXT.md` 和 ADR。
- **[triage](./skills/engineering/triage/SKILL.md)** — 按 triage 角色状态机推进 issues。
- **[improve-codebase-architecture](./skills/engineering/improve-codebase-architecture/SKILL.md)** — 扫描代码库寻找加深模块的机会，以可视化 HTML 报告呈现，再对你选中的那一项做审讯式对齐。
- **[setup-matt-pocock-skills](./skills/engineering/setup-matt-pocock-skills/SKILL.md)** — 为本仓库的 engineering skills 做配置（issue tracker、triage 标签、领域文档布局）。在使用其他 engineering skills 前，每个仓库跑一次。
- **[to-spec](./skills/engineering/to-spec/SKILL.md)** — 把当前对话变成 spec 并发布到 issue tracker。不做访谈——只综合你们已经讨论过的内容。
- **[to-tickets](./skills/engineering/to-tickets/SKILL.md)** — 把任何计划、spec 或对话拆成一组 tracer-bullet 工单，每个声明自己的阻塞边——写成本地文件里的文本，或真实 tracker 上的原生阻塞链接。
- **[wayfinder](./skills/engineering/wayfinder/SKILL.md)** — 规划超出单次 agent 会话容量的大块工作，在 issue tracker 上做成共享的调查工单地图——一次解决一个，直到通往终点的路清晰。

**模型调用**

- **[prototype](./skills/engineering/prototype/SKILL.md)** — 做一个可丢弃的原型来回答设计问题——状态/逻辑问题用可运行的终端应用；UI 问题则在同一路由下提供多种截然不同的、可切换变体。
- **[diagnosing-bugs](./skills/engineering/diagnosing-bugs/SKILL.md)** — 针对疑难 bug 和性能回退的纪律化诊断循环：复现 → 最小化 → 假设 → 埋点 → 修复 → 回归测试。
- **[research](./skills/engineering/research/SKILL.md)** — 针对高可信一手来源调查一个问题，把发现写成带引用的 Markdown 文件放进仓库，作为后台 agent 运行。
- **[tdd](./skills/engineering/tdd/SKILL.md)** — 带红-绿-重构循环的测试驱动开发。一次做一个垂直切片来构建功能或修 bug。
- **[domain-modeling](./skills/engineering/domain-modeling/SKILL.md)** — 主动构建并打磨项目的领域模型——用术语表挑战术语、用边界场景压力测试，并就地更新 `CONTEXT.md` 和 ADR。
- **[codebase-design](./skills/engineering/codebase-design/SKILL.md)** — 设计深模块的共享纪律与词汇：大量行为藏在小接口后面，放在干净的接缝上，并通过该接口可测。
- **[code-review](./skills/engineering/code-review/SKILL.md)** — 对自固定点以来的 diff 做双轴审查：**Standards**（是否遵循仓库编码标准，外加 Fowler smell 基线？）和 **Spec**（是否忠实地实现了来源 issue/PRD？），以并行子 agent 运行，互不污染。

### Productivity

通用工作流工具，不限于代码。

**用户调用**

- **[grill-me](./skills/productivity/grill-me/SKILL.md)** — 针对计划或设计被无情追问，直到决策树的每个分支都解决。
- **[handoff](./skills/productivity/handoff/SKILL.md)** — 把当前对话压成交接文档，好让另一个 agent 继续工作。
- **[teach](./skills/productivity/teach/SKILL.md)** — 跨多次会话教用户一项新技能或概念，用当前目录作为有状态的教学工作区。
- **[writing-great-skills](./skills/productivity/writing-great-skills/SKILL.md)** — 写好、改好 skills 的参考：让 skill 可预期的词汇与原则。

**模型调用**

- **[grilling](./skills/productivity/grilling/SKILL.md)** — 针对计划或设计无情追问用户，直到决策树的每个分支都解决。`grill-me` 和 `grill-with-docs` 背后的可复用循环。
