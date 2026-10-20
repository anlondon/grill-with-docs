[English](./README.md) | 中文

<p>
  <a href="https://www.aihero.dev/s/skills-newsletter">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skills-repo-dark_2x.png">
      <source media="(prefers-color-scheme: light)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skill-repo-light_2x.png">
      <img alt="Skills" src="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skill-repo-light_2x.png" width="369">
    </picture>
  </a>
</p>

# 给真正做工程的人用的 Skills

[![skills.sh](https://skills.sh/b/mattpocock/skills)](https://skills.sh/mattpocock/skills)

这是我每天用来做真实工程的 agent skills，不是用来“凭感觉写代码”的。

做真正的应用很难。GSD、BMAD、Spec-Kit 这类方法想帮忙，做法是把流程接管过去。接管之后，你失去控制，流程自己出了错也难查。

这些 skill 做得小，方便改，也能拼在一起用。它们不挑模型，来自几十年的工程经验。拿去改，变成你自己的。好好用。

如果想跟上这些 skill 的改动，以及我新写的 skill，可以加入大约 6 万人的 newsletter：

[订阅 Newsletter](https://www.aihero.dev/s/skills-newsletter)

## 安装（大约 30 秒）

插件会自己更新。[skills.sh](https://skills.sh/mattpocock/skills) 是把可编辑的文件复制进你的项目，之后要自己更新。每个 agent 只选一种装法，两种都装的话，每个 skill 会出现两份。

### 1. 拿到这些 skill

<details>
<summary><strong>Claude Code</strong></summary>

```bash
claude plugin install mattpocock-skills@claude-plugins-official
```

默认会自己更新。

</details>

<details>
<summary><strong>Codex</strong></summary>

```bash
codex plugin marketplace add mattpocock/skills
codex plugin add mattpocock-skills@mattpocock
```

启动时会自己更新。

</details>

<details>
<summary><strong>GitHub Copilot</strong>（CLI 和 VS Code）</summary>

```bash
copilot plugin marketplace add mattpocock/skills
copilot plugin install mattpocock-skills@mattpocock
```

然后做一次，写进 `~/.copilot/settings.json`：

```json
{
  "extraKnownMarketplaces": {
    "mattpocock": { "source": { "source": "github", "repo": "mattpocock/skills" }, "autoUpdate": true }
  }
}
```

在 VS Code 里运行 **Chat: Install Plugin From Source**，填 `https://github.com/mattpocock/skills`。它每天更新。

</details>

<details>
<summary><strong>Gemini CLI</strong>（手动更新）</summary>

```bash
gemini skills install https://github.com/mattpocock/skills.git --path skills/engineering
gemini skills install https://github.com/mattpocock/skills.git --path skills/productivity
```

要更新就再跑这两条。

</details>

<details>
<summary><strong>其他 agent，或想要可编辑的文件</strong>（手动更新）</summary>

```bash
npx skills@latest add mattpocock/skills -a <agent>  # cursor, opencode, devin, windsurf, amp, pi; 不写 -a 就会让你自己选
```

安装程序问你要哪些 skill 时，把 `setup-matt-pocock-skills` 包括进去。更新时跑 `npx skills@latest update`，新 skill 要再跑一次 `add` 才会出现。

</details>

### 2. 跑一次 `/setup-matt-pocock-skills`

在 agent 里，每个仓库跑一次。它会问你：

- 工单放在哪（GitHub、GitLab、本地文件，或你自己描述的地方）
- 分拣工单时用哪些标签（`/triage` 会用到）
- 我们写出的文档放在哪

### 3. 可以开始了。

## 这些 skill 为什么存在

我写它们，是为了修我在 Claude Code、Codex 和其他编程 agent 上反复看到的失败。

### 1. Agent 没做成我想要的

> “没有人完全知道自己要什么。”
>
> David Thomas、Andrew Hunt，[《程序员修炼之道》](https://www.amazon.co.uk/Pragmatic-Programmer-Anniversary-Journey-Mastery/dp/B0833F1T3V)

**问题。** 软件开发里最常见的失败，是两边想的不是同一件事。你以为对方知道你要什么。等你看到做出来的东西，才发现它根本没理解你。

用上 AI 之后还是这样。你和 agent 之间有一道沟通缺口。补上的办法是一次 **grilling**：让 agent 就你要做的东西，逐项问清楚。

**做法**是用：

- [`/grill-me`](./skills/productivity/grill-me/SKILL.md)：不在代码仓库里用
- [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md)：和 [`/grill-me`](./skills/productivity/grill-me/SKILL.md) 一样追问，另外会把说法和决定写进仓库（见下文）

这两个是我用得最多的 skill。每次要改东西之前，用它们先和 agent 对齐，并把这次改动想清楚。

### 2. Agent 太啰嗦

> 有了统一语言，开发者之间的谈话和代码里的表达，都从同一个领域模型来。
>
> Eric Evans，[《领域驱动设计》](https://www.amazon.co.uk/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215)

**问题：** 项目刚开始时，写软件的人和提需求的人往往不说同一种话。

我和 agent 之间也是这样。agent 被丢进一个项目，一边做一边猜黑话，于是能用 1 个词说清的事，它用 20 个词。

**做法**是一份共享语言。这是一份文档，帮 agent 读懂项目里的行话。

<details>
<summary>
例子
</summary>

这是我的 `course-video-manager` 仓库里的一份 [术语表](https://github.com/mattpocock/course-video-manager/blob/076a5a7a182db0fe1e62971dd7a68bcadf010f1c/CONTEXT.md)（那次提交里还叫 `CONTEXT.md`，后来这套 skill 把约定改成了 `GLOSSARY.md`）。哪一句更好读？

- **之前：** “课程某一节里的一课被做成‘真实的’（也就是在文件系统里给了它一个位置）时出了问题”
- **之后：** “materialization cascade 出了问题”

这种缩短，每次开会话都还在起作用。

</details>

这写在 [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md) 里。它还是一次追问，同时帮你和 AI 建成一套共用说法，并把难以事后解释的决定记成 ADR。

这有多有用，很难一次讲完。它可能是这个仓库里最值得试的一件事。

> [!TIP]
> 共享语言除了少说话，还有这些好处：
>
> - **变量、函数、文件用同一套名字**
> - 因此 agent **更容易在代码里找到路**
> - agent **思考时少花一些 token**，因为它手里已经有更短的说法

### 3. 代码不能跑

> “永远走小而故意的步骤。反馈有多快，你就只能走多快。不要接一件大到抱不住的任务。”
>
> David Thomas、Andrew Hunt，[《程序员修炼之道》](https://www.amazon.co.uk/Pragmatic-Programmer-Anniversary-Journey-Mastery/dp/B0833F1T3V)

**问题：** 就算你和 agent 已经对齐要做什么，它做出来的东西还是不行，怎么办？

去看反馈环。它写出来的代码到底能不能跑，如果没有反馈，它就是闭着眼睛飞。

**做法：** 你需要通常那一组反馈：静态类型、浏览器、自动化测试。

自动化测试里，红-绿-重构这一圈很关键。agent 先写一个失败的测试，再让测试通过。这样它每次都得到同样性质的反馈，写出来的代码会好很多。

我写了 **[`/tdd`](./skills/engineering/tdd/SKILL.md)**，可以放进任何项目。它推动红-绿-重构，并告诉 agent 什么样的测试好、什么样的不好。

排查问题时，我写了 **[`/diagnosing-bugs`](./skills/engineering/diagnosing-bugs/SKILL.md)**。它把一套排查做法收成有门禁的循环，一阶段一阶段往下走。

### 4. 做成了一团泥

> “每天都在系统设计上投入。”
>
> Kent Beck，[《解析极限编程》](https://www.amazon.co.uk/Extreme-Programming-Explained-Embrace-Change/dp/0321278658)

> “最好的模块是深的。很多功能，从一个简单的接口进去就能用到。”
>
> John Ousterhout，[《软件设计哲学》](https://www.amazon.co.uk/Philosophy-Software-Design-2nd/dp/173210221X)

**问题：** 用 agent 搭出来的应用，大多又复杂又难改。agent 把写代码加快了，也把软件变乱的速度加快了。代码库变复杂的速度，是以前没有的。

**做法**是一种更较真的 AI 开发方式：在意代码的设计。

这写进了这些 skill 的每一层：

- [`/to-spec`](./skills/engineering/to-spec/SKILL.md) 在写成规格之前，会问你这次动哪些模块

更关键的是 [`/improve-codebase-architecture`](./skills/engineering/improve-codebase-architecture/SKILL.md)。它巡视代码库，找出可以变“深”的地方，把候选交给你。我建议每隔几天对代码库跑一次。它是巡视，不是救援：老代码库上它找得到真候选，但不会替你把那团泥解开。

### 小结

软件工程的基本功比以前更重要。这些 skill 是我把这些基本功收成可重复做法的一次努力，帮你做出职业生涯里最好的那些应用。

## 参考

它们按一个轴分开：谁来调用。**你来点名**的 skill 只有你打出名字才出现（例如 `/grill-me`），负责把流程串起来。**模型也会自己拿起**的 skill，你可以点名，任务对上时 agent 自己也会用；它们放的是可重复的做法。你点名的 skill 可以去用模型自己会拿的 skill，但不会再去调用另一个要你点名的 skill。

每个 skill 单独的说明、以及什么时候用，写在 [docs/skills.zh-CN.md](./docs/skills.zh-CN.md)（[English](./docs/skills.md)）。

### 工程

我每天写代码会用的 skill。

**你来点名**

- **[ask-matt](./skills/engineering/ask-matt/SKILL.md)**：问现在该用哪个 skill 或哪条流程。它是这个仓库里那些“你来点名”的 skill 的问路人。
- **[grill-with-docs](./skills/engineering/grill-with-docs/SKILL.md)**：追问一次方案，同时建项目的领域说法，并把术语和 ADR 写进仓库。
- **[triage](./skills/engineering/triage/SKILL.md)**：让 issue 按分拣角色的状态机往下走。
- **[improve-codebase-architecture](./skills/engineering/improve-codebase-architecture/SKILL.md)**：扫描代码库里可以变深的地方，做成一份可视化 HTML 报告，再挑一个追问下去。
- **[setup-matt-pocock-skills](./skills/engineering/setup-matt-pocock-skills/SKILL.md)**：为一个仓库配好工程 skill（工单放哪、分拣标签、领域文档放哪）。用其他工程 skill 之前，每个仓库跑一次。
- **[to-spec](./skills/engineering/to-spec/SKILL.md)**：把当前谈话收成一份规格，发到工单系统。不再追问，只整理你们已经谈过的内容。
- **[to-tickets](./skills/engineering/to-tickets/SKILL.md)**：把一份计划、规格或谈话拆成一组小票。每张票写明它被谁挡住。可以写成本地文件，也可以在真正的工单系统上做成阻塞链接。
- **[implement](./skills/engineering/implement/SKILL.md)**：按一份规格或一组票把东西做出来。事先说好的接缝上走 `/tdd`，提交前用 `/code-review` 收尾。
- **[implement-spec](./skills/engineering/implement-spec/SKILL.md)**：整份规格放在一条集成分支上做。把票当成任务图，能同时做的那些交给多个实现子 agent，最后用 `/code-review` 收尾。
- **[wayfinder](./skills/engineering/wayfinder/SKILL.md)**：一次谈话装不下的一大块工作。在工单系统上画一张共享的决策地图，一次解决一张，直到去向清楚。
- **[retro](./skills/engineering/retro/SKILL.md)**：一次会话之后，建议怎么改进 coding agent 的环境（找路、自动检查、编码规范、指引文件、工具）。最严重的排在前面。

**模型也会自己拿起**

- **[prototype](./skills/engineering/prototype/SKILL.md)**：做一个用完即扔的原型来回答设计问题。状态或逻辑问题做成一个可分享的 HTML 文件；界面问题做成同一条路由上可切换的几种差别很大的样子。
- **[diagnosing-bugs](./skills/engineering/diagnosing-bugs/SKILL.md)**：难查的 bug 和性能回退。先做出一个能稳定变红的反馈环，再缩小、提假设、加探针、修复、补回归测试。
- **[research](./skills/engineering/research/SKILL.md)**：对着可靠的一手来源查一个问题，把发现写成带来源引用的 Markdown，放进仓库。当作后台 agent 跑。
- **[tdd](./skills/engineering/tdd/SKILL.md)**：测试驱动开发，红-绿-重构。一次做一个纵向切片，用来做功能或修 bug。
- **[domain-modeling](./skills/engineering/domain-modeling/SKILL.md)**：主动建立并收紧项目的领域模型。拿术语去对术语表，用边界场景试，并当场更新 `GLOSSARY.md` 和 ADR。
- **[codebase-design](./skills/engineering/codebase-design/SKILL.md)**：设计深模块时共用的做法和词汇。很多行为藏在一个小接口后面，放在干净的接缝上，并且能透过这个接口来测。
- **[code-review](./skills/engineering/code-review/SKILL.md)**：从某个固定点以来的 diff，分两路看。**规范**：守不守这个仓库的编码规范，外加一套 Fowler 的坏味道基线。**规格**：有没有忠实实现原来的 issue 或规格。两路用并行的子 agent，互不污染。
- **[pr](./skills/engineering/pr/SKILL.md)**：一份 pull request 说明该长什么样。摘要是能把改动看清的最小图示；附上改前改后、证明它能用的证据；并判断合并有多危险（单向门还是双向门，以及波及范围）。
- **[wizard](./skills/engineering/wizard/SKILL.md)**：生成一个交互式 bash 向导，带人走只有人能做的步骤：开通基础设施、配置凭据或 CI 密钥、在不熟悉的第三方后台里点一遍，或做一次迁移、切换。

### 生产力

通用的工作流工具，不限于写代码。

**你来点名**

- **[grill-me](./skills/productivity/grill-me/SKILL.md)**：就一份计划或设计追问下去，直到设计树上的每一支都有了结论。
- **[handoff](./skills/productivity/handoff/SKILL.md)**：把当前谈话压成一份交接文档，让另一个 agent 接着做。
- **[teach](./skills/productivity/teach/SKILL.md)**：分多次教用户一个新技能或概念。当前目录当作有状态的教室。
- **[to-questionnaire](./skills/productivity/to-questionnaire/SKILL.md)**：一个你一个人答不了的决定，做成 Markdown 问卷，交给那个能答的人。可以异步填，也可以开会一起填。它追问的是这次发送（给谁、你要拿回什么），不是题目本身。
- **[wait-what](./skills/productivity/wait-what/SKILL.md)**：一句话没听懂时立刻用。agent 用你缺少的上下文把那句话重新讲一遍，用大白话，并用你 `GLOSSARY.md` 里的词。

**模型也会自己拿起**

- **[grilling](./skills/productivity/grilling/SKILL.md)**：就一份计划、一个决定或一个想法追问用户，直到设计树上的每一支都有结论。这是 `grill-me`、`grill-with-docs`、`triage`、`wayfinder`、`improve-codebase-architecture` 背后共用的追问做法。
- **[writing-for-agents](./skills/productivity/writing-for-agents/SKILL.md)**：写给 agent 看的文档：skill、AGENTS.md / CLAUDE.md，以及 agent 会顺着链接打开的任何文档。
