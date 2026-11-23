---
name: poke-holes
description: Interview the user about a plan, design or idea before any work starts, one question at a time, hardest-to-reverse decisions first, each with a recommended answer, until the open decisions are settled, then write a decision record. Use when the user asks to be grilled, questioned, challenged or interviewed about a plan, says "poke holes in this", "what am I missing", "ask me questions before you start", or wants to stress-test a spec, architecture, product idea, launch or proposal. Skip when the user asks for a written review or critique in a single reply, asks to just build it, or when the task is so small that a wrong guess costs minutes.
license: MIT
metadata:
  author: gala-ud
  version: 0.1.0
---

# Poke holes

A plan fails on the decision nobody made. Asked to "ask me questions", an
agent sends ten at once, half of them answered in the repository and none
ranked. This skill runs an interview and ends with a decision record.

## Process

1. **Read first**: the plan and everything you can reach (repository,
   linked documents, earlier messages). Whatever the material answers is
   not a question; note it as "Found" with its location.

2. **List the open decisions**, privately. A decision is open where the
   plan is silent, vague ("fast", "simple", "later", "users"), contradicts
   itself or the code, or rests on something nobody checked. Note for each
   what a wrong guess breaks and how hard that is to undo.

3. **Order them.** First: what is expensive to undo (data model, public
   API, money, security, legal, what is out of scope). Then: decisions that
   other decisions depend on. Then the rest. Drop a question when both
   answers lead to the same next step.

4. **Ask one question per message**, in this form, and nothing else:

   ```markdown
   **Q3 of about 8 - <topic>**
   <The question, in one sentence, answerable in a few words.>
   Why it matters: <what gets built differently depending on the answer>
   I'd pick: <an answer>, because <a reason from their material>
   ```

   Where it is a choice, list the options as a, b, c above "I'd pick" so
   the user can reply with a letter. Where only the user can know (budget,
   deadline, who the customers are), replace the last line with "Only you
   know this one." The message has exactly one question mark. "Where do
   files live and how long are they kept?" is two questions: ask the one
   that is harder to undo and queue the other. Nothing follows the last line.

5. **Handle the answer** before asking the next question:
   - Restate the decision in one line.
   - If it opens a new decision, queue it and update the count.
   - If it contradicts an earlier answer or the code, ask which stands.
   - "You decide" or "I don't know": take your recommendation and mark it
     Assumed.
   - Too vague to build from: ask once more with an example, then mark Open.
   - If the user picks against your recommendation, record their choice.
     State your concern once, in one line, with the consequence.

6. **Stop** when no remaining question would change what gets built first,
   or the user says enough. After 12, say how many are left and ask.

7. **Write the decision record** below. Do not start building.

## Decision record

```markdown
## Decision record: <plan>

**Decided**
1. <decision> - <reason, in the user's words where possible>

**Found in the material**
- <fact that answered a question> (`path:line` or document section)

**Assumed** (I chose; reverse if wrong)
- <assumption> - <what to change if it is wrong>

**Still open**
- <question> - blocks: <which part of the work>

**Changed by this interview:** <what differs from the plan as first given, or "nothing">
**Riskiest thing left:** <one line>
```

Omit empty groups. Every answer appears in exactly one of the first four.

## Rules

- **One question per message.** Never a list, never two joined by "and",
  no "also tell me". No code, files or build steps during the interview.
- **Never ask what you can look up.** Check the material before every
  question, including the ones added mid-interview.
- **Every question carries a recommendation** unless only the user can
  know. "It depends" is not a recommendation.
- **Never invent an answer.** What the user did not answer is Assumed (your
  choice, labelled) or Still open, never Decided.
- **No flattery and no filler**: no "great question", no summary of the
  plan back to the user, no praise of the answer.
- **Ask about consequences**: "Can two people edit one invoice at once?"
  beats "How do you feel about concurrency?"
