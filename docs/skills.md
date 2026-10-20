English | [中文](./skills.zh-CN.md)

# How the skills fit together

`grill-with-docs` is the start of one build chain. The skills around it do the steps it deliberately does not do: write the spec, split the work, build it, review it, and look back at the tools.

Two kinds of skill show up below.

- **You type the name.** It only starts when you invoke it, such as `/grill-with-docs`. These string a flow together.
- **The agent may pick it up.** You can still type it. When the task matches, the agent reaches for it on its own. These hold one repeatable discipline.

A skill you type may call a skill the agent picks up. It does not call another skill that you have to type.

```txt
grill-with-docs → to-spec → to-tickets → implement → code-review → retro
```

In this fork, `grill-with-docs` is a self-contained skill. It writes terms to `CONTEXT.md`. The rest of the family still talks about `GLOSSARY.md`, which is the upstream name for the same kind of glossary.

## The main chain

**[grill-with-docs](../skills/engineering/grill-with-docs/SKILL.md).** A questioning session that also leaves a glossary. You are about to add "pay later" to checkout, and you and the agent do not yet agree what happens when the card is declined. It asks one question at a time, in everyday words, with one short scene and one reason. A short name is offered only when two readings would change the next decision. Settled words go into `CONTEXT.md` as they are settled.

**[to-spec](../skills/engineering/to-spec/SKILL.md).** Turn the conversation you just had into a spec, and publish it to the issue tracker. The grilling is over. You do not want another round of questions. You want the decisions already made written down as the thing to build, including which modules the change touches.

**[to-tickets](../skills/engineering/to-tickets/SKILL.md).** Cut that spec into small tickets, and say which ticket blocks which. "Save the card" cannot start until "create the customer" exists. Each ticket is a thin slice you could build and check on its own, as a local file or as real blocking links on a tracker.

**[implement](../skills/engineering/implement/SKILL.md).** Build the tickets. Where you agreed a seam needs a test, it drives [tdd](../skills/engineering/tdd/SKILL.md): a failing test first, then the code that makes it pass. Before the commit, it runs [code-review](../skills/engineering/code-review/SKILL.md).

**[code-review](../skills/engineering/code-review/SKILL.md).** Read the diff since a fixed point, on two separate passes so they do not blur together. One pass asks whether the change follows this repo's standards. The other asks whether it does what the spec said. A change can be tidy and still miss the spec.

**[retro](../skills/engineering/retro/SKILL.md).** After the session, look at the agent's workshop rather than the feature. The agent kept guessing the test command, or the repo has no place that says where docs go. It lists the worst of those gaps first.

## Next to grill

**[grill-me](../skills/productivity/grill-me/SKILL.md).** The same kind of interview, with no repo and no files. You are talking through a product idea on a blank directory, and you do not want a glossary written yet.

**[grilling](../skills/productivity/grilling/SKILL.md).** The shared interview habit behind several skills, not a session you usually start yourself. `grill-me`, `triage`, `wayfinder`, and `improve-codebase-architecture` use it so they ask in rounds instead of inventing their own interview. In this fork, `grill-with-docs` no longer delegates to it. The questioning rules live in its own `SKILL.md`.

**[domain-modeling](../skills/engineering/domain-modeling/SKILL.md).** The habit of keeping a glossary and ADRs while you design. Upstream, `grill-with-docs` was a one-line skill that called this for the writing. This fork writes `CONTEXT.md` itself. `domain-modeling` is still here for sessions that should maintain a `GLOSSARY.md`.

**[wayfinder](../skills/engineering/wayfinder/SKILL.md).** The work is too big for one sitting. You are starting a new product, not adding one checkout rule. It draws a map of decision tickets on the issue tracker and resolves them one at a time. A piece of that map that fits in one session can come back down to `grill-with-docs`.

**[ask-matt](../skills/engineering/ask-matt/SKILL.md).** You are not sure which skill to type. It listens to the situation and points at one of the skills you invoke, instead of starting the work itself.

**[setup-matt-pocock-skills](../skills/engineering/setup-matt-pocock-skills/SKILL.md).** Once per repo, before the others. It asks where tickets live, which labels triage uses, and where new docs should be saved. Without this, later skills guess.

**[to-questionnaire](../skills/productivity/to-questionnaire/SKILL.md).** The next decision is in someone else's head. You need a lawyer to say whether a declined card may be retried. It writes a Markdown questionnaire for that person. It asks you who it is for and what you need back. It does not grill the subject itself.

## The rest of the engineering skills

**[triage](../skills/engineering/triage/SKILL.md).** Move an issue through roles: someone names what it is, someone decides if it is in scope, someone is ready to build it. A bug report arrives that is really a feature request. Triage sends it to the right role instead of letting an agent start coding.

**[improve-codebase-architecture](../skills/engineering/improve-codebase-architecture/SKILL.md).** Look through a codebase for modules that do too little behind too much surface, and hand you an HTML report of candidates. You pick one, and it grills that one. It will not untangle an old codebase for you. On a large app, run it every few days as a survey.

**[implement-spec](../skills/engineering/implement-spec/SKILL.md).** Build a whole spec on one integration branch. Tickets that do not block each other run at the same time, each with its own implementer. It still closes with `code-review`. Use this when `implement` one ticket at a time is slower than the spec deserves.

**[prototype](../skills/engineering/prototype/SKILL.md).** Answer a design question with something you mean to throw away. "What should the screen do when the card is declined?" becomes one HTML file you can open, or several very different screens on one route you can switch between. It is not the production checkout.

**[diagnosing-bugs](../skills/engineering/diagnosing-bugs/SKILL.md).** A bug that does not sit still. First make a check that fails every time the bug is present. Then shrink the case, state a hypothesis, add a probe, fix it, and leave a test that would catch the same failure again. The same loop is for a screen that used to render in 100ms and now takes 2s.

**[research](../skills/engineering/research/SKILL.md).** You need an answer from a primary source, not from the model's memory. "What does this payment network actually return when a card is declined?" It reads those sources and writes a Markdown file in the repo with citations. It is meant to run as a background agent.

**[tdd](../skills/engineering/tdd/SKILL.md).** Build one vertical slice by writing a failing test, making it pass, then cleaning up. `implement` calls this at seams you already agreed should have a test. You can also point it at a single bug: the test goes red on that bug, then the fix turns it green.

**[codebase-design](../skills/engineering/codebase-design/SKILL.md).** Shared words for a module that hides a lot behind a small interface, sits on a clean seam, and can be tested through that interface. Other design skills use this vocabulary so they do not each invent a new word for "deep module".

**[pr](../skills/engineering/pr/SKILL.md).** The shape of a pull request description. Lead with the smallest picture that makes the change clear, then show evidence from before and after that it works, then say how dangerous the merge is: easy to undo, or a one-way door, and how far it reaches.

**[wizard](../skills/engineering/wizard/SKILL.md).** Steps only a person can do: create a cloud account, paste a CI secret, click through a dashboard you have never seen. It generates an interactive bash script that walks through those steps and waits for the human at each one.

## Productivity

**[handoff](../skills/productivity/handoff/SKILL.md).** This conversation is full, and another agent has to continue tomorrow. It compresses the conversation into a handoff document so the next agent does not start from a blank page.

**[teach](../skills/productivity/teach/SKILL.md).** You want to learn one concept over several sittings. The current directory is the classroom: notes and exercises stay on disk between sessions.

**[wait-what](../skills/productivity/wait-what/SKILL.md).** A sentence just did not land. You type this immediately. The agent says that sentence again with the missing context, in plain words, using the project's glossary.

**[writing-for-agents](../skills/productivity/writing-for-agents/SKILL.md).** You are writing a document an agent will read later: a skill, an `AGENTS.md`, a `CLAUDE.md`, or a page the agent opens because something pointed at it. It is about how to write that page so the next agent follows it.

`skills/in-progress/` and `skills/misc/` are drafts and one-off helpers. They are not part of the chain above.
