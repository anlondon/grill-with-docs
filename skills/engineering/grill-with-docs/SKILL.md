---
name: grill-with-docs
description: Grilling session that challenges your plan against the existing domain model, sharpens terminology, and updates documentation (CONTEXT.md, ADRs) inline as decisions crystallise. Use when user wants to stress-test a plan against their project's language and documented decisions.
disable-model-invocation: true
---

<what-to-do>

Interview me until we reach a shared understanding of this change. Walk only the branches that are related to the current requirement and the change being made. Ask one of those branches only when its requirement is unclear, or the change affects it and that effect cannot be confirmed. Skip a branch that has no relation to this change, even if it is nearby. For each question you do ask, provide your recommended answer.

Speak in the user's language, in everyday words. Every question and every recommended answer uses the same thickness as a glossary entry:

1. One plain sentence that restates the choice. No coined name yet.
2. One short scene, two or three sentences: a specific person, what they did, and the outcome. When the boundary is easy to miss, the same scene names one case that does not count.
3. Then the recommended answer, plus one reason sentence: what happens if we choose this, and what happens if we choose the other. One sentence, not a paragraph.
4. Offer a short name only when the user's words have two readings and those readings would change the next decision. If both readings are the same action, say that action in the plain sentence and the scene, and move on. Do not mint a term. The reason sentence is spoken. It does not go into the glossary entry.

A question that leads with the coined name is not done. A recommendation without the one reason sentence is not done.

Ask the questions one at a time, waiting for feedback on each question before continuing.

When the user has already brought in a product or business reply, do not open questions about what you do not understand, what seems ambiguous, or what appears to contradict the current business but cannot be settled into a requirement. Later, ask one confirmation: restate that reply in one plain sentence and ask whether you heard it right. One confirmation for that reply, then move on.

The user pastes: "If the card is declined, cancel the order. Do not retry." Ask only: "What I heard is that a declined card cancels the whole order and does not retry. Is that right?" Do not go on to ask whether cancel means the whole order or one dish.

Do not ask about a place that has no relation to the current requirement or change. Not being named is not itself a reason to skip: ask when a related place has an unclear requirement, or the change affects it and that effect cannot be confirmed. The user asks to cancel an order when the card is declined. Ask whether money already taken is refunded, because that refund is tied to the cancellation and the reply never said. Do not ask whether the kitchen ticket font changes, because that font is not tied to this cancellation.

If a question can be answered by exploring the codebase, explore the codebase instead.

</what-to-do>

<supporting-info>

## Domain awareness

During codebase exploration, also look for existing documentation:

### File structure

Most repos have a single context:

```
/
├── CONTEXT.md
├── docs/
│   └── adr/
│       ├── 0001-event-sourced-orders.md
│       └── 0002-postgres-for-write-model.md
└── src/
```

If a `CONTEXT-MAP.md` exists at the root, the repo has multiple contexts. The map points to where each one lives:

```
/
├── CONTEXT-MAP.md
├── docs/
│   └── adr/                          ← system-wide decisions
├── src/
│   ├── ordering/
│   │   ├── CONTEXT.md
│   │   └── docs/adr/                 ← context-specific decisions
│   └── billing/
│       ├── CONTEXT.md
│       └── docs/adr/
```

Create files lazily — only when you have something to write. If no `CONTEXT.md` exists, create one when the first term is resolved. If no `docs/adr/` exists, create it when the first ADR is needed.

## During the session

### Challenge against the glossary

When the user uses a term that conflicts with the existing language in `CONTEXT.md`, and the two meanings would change the next decision, call it out in the same order: one plain sentence, one short scene, then the two names.

The glossary says cancellation ends the whole order. A guest ordered a set meal and a drink, and wants to drop only the drink. Ending the whole meal and dropping the drink are different actions. Ask which one they mean.

If the two meanings would not change the next decision, use the glossary's word and continue. Do not stop.

### Sharpen fuzzy language

Propose a new canonical term only when the user's words have two readings and those readings would change the next decision. Use the same order as any other question: one plain sentence, one short scene, then the short name.

The user says "account", and who owns the order depends on which person they mean. A guest asks for a set meal and will pay for it. A staff member only types the order in. The guest is the Customer. The staff member is the User. Ask which one.

The user says the order is void whether the card is declined or the charge times out. Both readings are the same action: the ticket is thrown away. Say that in everyday words and ask the next real question. Do not invent a name for each failure.

### Discuss concrete scenarios

When a relationship inside this change is being discussed, and the requirement is unclear or the effect of the change cannot be confirmed, stress-test it with a specific scenario. The scene goes in the question itself, in everyday words. Do not invent a scenario for a relationship that has no bearing on this change.

### Cross-reference with code

When the user states how something works, check whether the code agrees. If you find a contradiction, surface it in the same order: one plain sentence, one short scene, one reason, then the question.

The user says a guest can drop just the drink. The code throws away the whole order. A guest ordered a set meal and a drink and wants to keep the meal. Dropping only the drink and cancelling the meal are different outcomes. Ask which one is right.

### Update CONTEXT.md inline

When a term is resolved, update `CONTEXT.md` right there. Don't batch these up — capture them as they happen. Use the format in [CONTEXT-FORMAT.md](./CONTEXT-FORMAT.md).

`CONTEXT.md` should be totally devoid of implementation details. Do not treat `CONTEXT.md` as a spec, a scratch pad, or a repository for implementation decisions. It is a glossary and nothing else.

### Offer ADRs sparingly

Only offer to create an ADR when all three are true:

1. **Hard to reverse** — the cost of changing your mind later is meaningful
2. **Surprising without context** — a future reader will wonder "why did they do it this way?"
3. **The result of a real trade-off** — there were genuine alternatives and you picked one for specific reasons

If any of the three is missing, skip the ADR. Use the format in [ADR-FORMAT.md](./ADR-FORMAT.md).

</supporting-info>
