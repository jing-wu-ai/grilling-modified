# grilling-modified

A modified fork of the [`grilling`](https://github.com/mattpocock/skills/tree/main/skills/productivity/grilling) agent skill by [Matt Pocock](https://github.com/mattpocock/skills) (MIT licensed).

The original is a "relentless interview" skill: it interviews the user round by round until a shared understanding is reached. This fork reworks it from a pure interview drill into an **investigate-first, evidence-driven questioning workflow** that stops as soon as the problem is decision-ready.

## What changed vs. the original

### 1. Investigate before asking
The original starts interviewing immediately. This fork requires the agent to first inspect all available context (conversation, files, logs, docs, prior decisions) and build an internal evidence map with four categories: established facts, reasonable inferences, material gaps, and user decisions. Questions are only asked about genuine gaps — never about something the agent could have looked up itself.

### 2. Two modes instead of one relentless loop
- **General grilling** (default): clarification + stress-testing as two stages of one workflow. Used when the real question, goal, or constraints are unclear, or when there aren't exactly two live options.
- **Two-sided steelman**: only for real decisions between exactly two clear, mutually exclusive options. Both sides get their strongest case before a pivotal question is asked. If the binary turns out to be false, the workflow returns to general grilling.

The original had a single mode and no mode routing.

### 3. Stop at 95% confidence instead of an empty frontier
The original's completion criterion is "the frontier is empty: every branch of the design tree visited". This fork replaces that with a practical **95% confidence threshold**: stop questioning as soon as the remaining unknowns would not change the recommended direction. It also explicitly forbids chasing unreachable certainty — if evidence has stopped reducing uncertainty, state the blocker instead of asking forever.

### 4. Questions no longer carry recommended answers
The original's question template attaches "➡️ your recommended answer" to every question. This fork removes that during problem-framing and diagnosis, because a suggested answer biases the diagnosis. A recommendation is allowed only for bounded implementation choices after the problem is already framed.

### 5. A gate before every question
Each question must pass five checks: answerable from evidence? already answered? a low-risk default would do? would the answer actually change the outcome? is it genuinely a user decision? Questions that fail the gate are not asked.

### 6. Asking mechanics
- Uses the host's structured question interface when available; falls back to concise Markdown otherwise.
- Multiple-choice labels are numbers (`1`, `2`, `3`) so users can answer compactly (`Q1=2, Q2=4`).
- Each round states in one sentence what the previous answers changed in the working judgment.
- Detects user fatigue and stops asking when the detail should already exist.

### 7. Cross-answer consistency check and per-round replanning
In long design interviews, users tend to pick the locally best answer to each question. Each answer looks right on its own, but together they conflict, so the plan never converges. The original treats every answer as settled and moves on. This fork adds a **between-rounds** step, run after every answer round before any new question:

- **Decision ledger.** Every settled answer is recorded with the priority or trade-off it implies (for example, "ship in three months" implies speed over completeness). Each new answer is compared against the whole ledger, not only the previous round. The agent looks for four kinds of problem: direct conflict, competing priorities for the same limited resource, a combined constraint breach, and a broken earlier premise.
- **Flag even small conflicts.** The agent quotes both statements, explains the collision and what keeping each side would mean, and asks which one wins. It must not reconcile them silently or proceed as if both were true. Mere directional pull is labelled a *tension* and noted rather than escalated, so conflicts are not manufactured.
- **Replan every round.** The frontier is rebuilt instead of following a list drafted up front. The next step is chosen in a fixed order: resolve conflicts, then clarify vague answers, then ask new frontier questions. Among questions of similar impact, the one that would settle or prune the most other branches goes first.
- **Concrete readings of vague answers.** Answers like "either is fine" or "it depends" get two or three concrete interpretations to choose from instead of a guessed meaning.
- **Topic checkpoints.** When a topic settles, a few lines list what is settled, what is still open, and possible next steps.
- **Stop condition tightened.** The 95% threshold is not met while any conflict in the ledger is unresolved.

This addition was inspired by a community prompt that asks the agent to flag even subtle micro-decision contradictions each round. That prompt also asks for a recommended answer on every question; this fork deliberately does not adopt that part (see §4).

### 8. `grill-me` entry point rewritten
The original `grill-me` just calls the Skill tool with "grilling". This fork rewrites it as an explicit entry point that reads the sibling `grilling/SKILL.md` directly and follows it with the user's request as the topic — more portable across agent hosts — and fails loudly instead of improvising if the sibling skill is unavailable.

### 9. Two new reference files
The original ships one `SKILL.md`. This fork splits the detail into:
- [`grilling/references/general-grilling.md`](grilling/references/general-grilling.md) — the two-stage clarify/stress-test workflow
- [`grilling/references/two-sided-steelman.md`](grilling/references/two-sided-steelman.md) — the steelman-both-sides decision workflow

## Layout

```
grilling/           # main model-invoked skill (SKILL.md + references + openai.yaml)
grill-me/           # explicit $grill-me user-invoked entry point
```

## Install

Copy the `grilling/` and `grill-me/` folders into your agent skills directory, e.g. for opencode:

```
~/.agents/skills/grilling
~/.agents/skills/grill-me
```

## Credits

- Original skill: [mattpocock/skills](https://github.com/mattpocock/skills) — MIT License, © Matt Pocock
- This fork: MIT License, modifications © 2026 jing-wu-ai
