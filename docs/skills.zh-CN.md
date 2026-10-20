[English](./skills.md) | 中文

# 这些 skill 怎么配合

`grill-with-docs` 是一条构建链的开头。它旁边的 skill 做它故意不做的事：写成规格、拆成工单、动手做、复查、再回头看工具。

下面有两种 skill。

- **你得点名。** 只有你喊出名字它才开始，比如 `/grill-with-docs`。这类负责把一条流程串起来。
- **agent 自己也会拿起来。** 你仍然可以点名。任务对得上时，它自己也会用。这类放的是一件可以反复做的事。

你点名的 skill 可以去调用 agent 自己会拿的 skill。它不会再去调用另一个必须由你点名的 skill。

```txt
grill-with-docs → to-spec → to-tickets → implement → code-review → retro
```

在这个 fork 里，`grill-with-docs` 是一份独立的 skill。术语写进 `CONTEXT.md`。家族里其余的 skill 仍说 `GLOSSARY.md`，那是上游给同一类术语表起的名字。

## 主路上的

**[grill-with-docs](../skills/engineering/grill-with-docs/SKILL.md)。** 一次追问，同时留下术语表。你正要在结账里加「先拿货、后付款」，你和 agent 还没说清卡被拒时这张单子怎么办。它一次问一个问题，先用日常的话，再讲一个短场景，再给一句理由。只有两种理解会让下一步不一样时，才给一个短名字。定下来的词，当场写进 `CONTEXT.md`。

**[to-spec](../skills/engineering/to-spec/SKILL.md)。** 把刚才的谈话收成一份规格，发到工单系统。追问已经结束。你不想再被问一轮。你要把已经定下的决定写成「要做的东西」，包括这次会碰到哪些模块。

**[to-tickets](../skills/engineering/to-tickets/SKILL.md)。** 把那份规格切成小票，并写明哪张票挡住哪张。没有「先建好顾客」，就不能开始「记住这张卡」。每张票都薄到可以单独做完、单独检查。可以是本地文件，也可以是工单系统上真正的阻塞链接。

**[implement](../skills/engineering/implement/SKILL.md)。** 把这些票做出来。事先说好要测试的接缝上，它会走 [tdd](../skills/engineering/tdd/SKILL.md)：先写一个失败的测试，再写让它通过的代码。提交之前跑 [code-review](../skills/engineering/code-review/SKILL.md)。

**[code-review](../skills/engineering/code-review/SKILL.md)。** 看从某个固定点以来的改动，分两遍，避免混在一起。一遍问这次改动守不守这个仓库的规矩。另一遍问它有没有做成规格里说的那件事。改动可以很整齐，同时漏掉规格。

**[retro](../skills/engineering/retro/SKILL.md)。** 会话结束之后，看的是 agent 的工作台，不是这个功能。agent 一直在猜测试命令，或者仓库里没有地方写文档该放哪。它把最严重的缺口排在前面。

## 挨着 grill 的

**[grill-me](../skills/productivity/grill-me/SKILL.md)。** 同一种追问，没有仓库，也不写文件。你在一个空目录里把一个产品想法谈清楚，这时还不想留下术语表。

**[grilling](../skills/productivity/grilling/SKILL.md)。** 好几个 skill 背后共用的追问习惯，通常不是你自己开的一场会话。`grill-me`、`triage`、`wayfinder`、`improve-codebase-architecture` 用它，这样它们按轮提问，而不是各自发明一种问法。在这个 fork 里，`grill-with-docs` 不再转去调用它。追问规则写在它自己的 `SKILL.md` 里。

**[domain-modeling](../skills/engineering/domain-modeling/SKILL.md)。** 一边设计，一边维护术语表和 ADR 的习惯。上游的 `grill-with-docs` 只有一行，写文件的事交给它。这个 fork 自己写 `CONTEXT.md`。需要维护 `GLOSSARY.md` 的会话，仍然用 `domain-modeling`。

**[wayfinder](../skills/engineering/wayfinder/SKILL.md)。** 这件事一次坐下来谈不完。你是在开始一个新产品，不是加一条结账规则。它在工单系统上画一张决策票的地图，一次解决一张。地图上能放进一次会话的那一块，可以再交回 `grill-with-docs`。

**[ask-matt](../skills/engineering/ask-matt/SKILL.md)。** 你不确定该点哪一个。它听你描述情况，然后指向一个要你点名的 skill，自己不开工。

**[setup-matt-pocock-skills](../skills/engineering/setup-matt-pocock-skills/SKILL.md)。** 每个仓库先跑一次，再使用别的。它问工单放在哪、分拣用哪些标签、新文档存到哪。没有这一步，后面的 skill 只能猜。

**[to-questionnaire](../skills/productivity/to-questionnaire/SKILL.md)。** 下一个决定在别人脑子里。你需要法务说：卡被拒之后能不能再试一次。它给那个人写一份 Markdown 问卷。它问你这份问卷给谁、你要拿回什么。它不替你把题目本身追问完。

## 其余的工程 skill

**[triage](../skills/engineering/triage/SKILL.md)。** 让一条 issue 按角色往下走：有人说清它是什么，有人决定它在不在范围内，有人准备开工。来了一份其实是功能请求的 bug 报告。分拣把它送到该去的角色，而不是让 agent 直接写代码。

**[improve-codebase-architecture](../skills/engineering/improve-codebase-architecture/SKILL.md)。** 在代码库里找那些表面很大、里面却没做多少事的模块，交给你一份 HTML 报告。你挑一个，它再追问那一个。它不会替你解开一个老代码库。大应用上，每隔几天把它当一次巡视来跑。

**[implement-spec](../skills/engineering/implement-spec/SKILL.md)。** 整份规格放在一条集成分支上做。互不挡住的票同时做，各有一个实现者。结束时仍然走 `code-review`。一张一张用 `implement` 会比这份规格该有的速度慢时，用这个。

**[prototype](../skills/engineering/prototype/SKILL.md)。** 用一个打算扔掉的东西来回答设计问题。「卡被拒时屏幕该怎样」变成一个能打开的 HTML 文件，或者同一条路由上可以来回切换的几种差别很大的界面。这不是要上线的结账页。

**[diagnosing-bugs](../skills/engineering/diagnosing-bugs/SKILL.md)。** 一个站不稳的 bug。先做一个只要 bug 还在就会失败的检查。再把情况缩小，说出一个假设，加上探针，修好，并留下一个能再抓住同一种失败的测试。画面以前 100 毫秒画完、现在要 2 秒，也走这一圈。

**[research](../skills/engineering/research/SKILL.md)。** 你要的答案来自一手材料，不是模型的记忆。「这张卡被拒时，支付网络实际返回什么？」它去读那些材料，在仓库里写一份带来源的 Markdown。它适合放在后台跑。

**[tdd](../skills/engineering/tdd/SKILL.md)。** 做一个纵向切片：先写失败的测试，再让它通过，然后收拾代码。`implement` 在你们已经说好要测试的接缝上调用它。你也可以把它对准一个 bug：测试在这个 bug 上变红，修复再把它变绿。

**[codebase-design](../skills/engineering/codebase-design/SKILL.md)。** 给一种模块共用的说法：很多行为藏在一个小接口后面，放在干净的接缝上，并且能透过这个接口来测。别的设计 skill 用这套词，免得各自再发明一个词来叫「深模块」。

**[pr](../skills/engineering/pr/SKILL.md)。** 一份 pull request 说明该长什么样。先放一张能把改动看清的最小图，再给出改前改后、证明它能用的证据，然后说这次合并有多危险：容易撤回，还是一扇单向门，以及波及多远。

**[wizard](../skills/engineering/wizard/SKILL.md)。** 只有人能做的步骤：去云上开一个账号、把 CI 密钥贴进去、在一个没见过的后台里点一遍。它生成一个交互式 bash 脚本，逐步带你走，每一步停下来等你。

## 不限于写代码的

**[handoff](../skills/productivity/handoff/SKILL.md)。** 这次谈话已经满了，明天得换一个 agent 接着做。它把谈话压成一份交接文档，下一个 agent 不用从空白页开始。

**[teach](../skills/productivity/teach/SKILL.md)。** 你想分好几次学一个概念。当前目录就是教室：笔记和练习留在磁盘上，下次还在。

**[wait-what](../skills/productivity/wait-what/SKILL.md)。** 刚才那句没听懂。你立刻点它。agent 用你缺的上下文把那句话再说一遍，用日常的话，并用项目术语表里的词。

**[writing-for-agents](../skills/productivity/writing-for-agents/SKILL.md)。** 你在写一份以后给 agent 读的文档：一个 skill、一份 `AGENTS.md`、一份 `CLAUDE.md`，或 agent 会因为某处指向它而打开的页面。它讲的是怎样写这一页，下一个 agent 才会照着做。

`skills/in-progress/` 和 `skills/misc/` 是草稿和一次性的辅助。它们不在上面这条链上。
