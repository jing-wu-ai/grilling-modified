---
name: grilling
description: Investigate context, clarify an unclear problem, stress-test a plan or idea, or compare two real options through focused questioning until the solution is decision-ready. Use when the user wants rigorous questioning or uses a grill trigger phrase.
---

Investigate first, then ask only questions that can materially change the problem definition, conclusion, recommendation, risk, or next action. Rigor comes from evidence and question quality, not from a fixed number of questions.

## Investigate before asking

Before the first question, inspect the context already available and build a working baseline. Depending on the task, this can include the current conversation, attachments, relevant workspace files, READMEs, source code, configuration, tests, logs, existing notes, prior decisions, and authoritative external sources. Stay within the requested scope and normal privacy and authorization boundaries; do not search for secrets or unrelated personal material.

Do this investigation yourself with the available tools. Delegate only when it is permitted and materially useful; delegation is not a prerequisite. Do not ask the user to locate, summarize, or re-explain something you can establish from accessible evidence.

Keep an internal evidence map with four categories:

1. **Established facts** — supported by current evidence or an explicit user statement.
2. **Reasonable inferences** — low-risk conclusions, clearly kept distinct from facts.
3. **Material gaps** — unknowns that could change the recommendation, scope, risk, or next action.
4. **User decisions** — genuine preference, priority, trade-off, or authorization choices that evidence cannot settle.

For experience or project cases, use these eight directions as a coverage checklist rather than a fixed questionnaire: starting point, goal, scope, role, key actions, difficulties and collaboration, results and evidence, reflection and transfer. Fill them from evidence first and ask only about material gaps.

Briefly tell the user what you have already checked and your current understanding before asking questions. This lets them correct the baseline without retelling the whole story.

## Route to one of two modes

An explicit user request for a mode wins. Otherwise choose by the structure of the problem, not by keywords alone.

### General grilling — the default

Use [references/general-grilling.md](references/general-grilling.md) when any of these is true:

- the real question, goal, success criterion, or constraints are still unclear;
- the user has a concern, interpretation, plan, claim, or idea to examine rather than two settled options to compare;
- there are fewer than two or more than two live options;
- the apparent binary choice may be false, incomplete, or premature;
- the task needs problem framing before a recommendation can be evaluated.

General grilling includes both clarification and stress-testing. They are stages of one workflow, not separate modes.

### Two-sided steelman

Use [references/two-sided-steelman.md](references/two-sided-steelman.md) only when all of these are true:

- the user needs to make a decision;
- there are exactly two clear, mutually exclusive, realistically available options;
- both options are plausible enough to deserve a serious case;
- the user wants help choosing between them.

If one condition is missing, start with general grilling. General grilling may transition into two-sided steelman once the problem genuinely resolves into two live options. If steelmanning reveals a false binary, return to general grilling and explain why.

## Build and prune the design tree

Map the decision as a **design tree**: each unresolved decision can branch into dependent decisions. Mark branches as settled when the answer is already established by evidence, prior user input, or a safe and reversible inference. Prune branches that are immaterial to the user's goal.

The **frontier** is the smallest set of unresolved, outcome-changing questions whose prerequisites are settled. Do not ask a question merely for completeness, because a generic interview template contains it, or because every conceivable branch has not been visited.

Follow the per-round cadence in the selected mode. General grilling asks up to the two highest-value independent frontier questions in a round. Two-sided steelman asks one pivotal question at a time after presenting both strongest cases. Never impose a total question limit, invent a filler question, or ask a dependent question before its prerequisite is settled.

Before asking each question, apply this gate:

- Can it be answered by reading or checking available evidence? If yes, investigate instead.
- Has the user already answered it, directly or indirectly? If yes, use that answer and state any uncertainty.
- Can a low-risk, reversible default keep progress moving? If yes, recommend and use the default unless confirmation genuinely matters.
- Would a different answer materially change the outcome? If no, do not ask.
- Is this a subjective choice, missing lived experience, high-impact trade-off, or authorization boundary? If yes, ask.

If investigation is still running, continue with independent questions only; defer downstream questions until the evidence arrives.

Before each new round after the first, state in one sentence what the previous answers changed in the working judgment. If they changed nothing, say why and either ask a genuinely different material question or stop.

## Ask clearly

Use the host's structured question interface whenever one is available, permitted, and can represent the questions faithfully. Put multiple questions from the same round into one request. Give each a short header and clear body; use options only when the choice is genuinely bounded, and allow a free-text alternative when supported.

If no structured question interface is available, or it cannot represent the questions faithfully, fall back to concise Markdown. Do not delay the session or ask the user to change tools merely to obtain the interface.

When a question offers multiple choices, label the choices with numbers (`1`, `2`, `3`, `4`, etc.), never letters (`A`, `B`, `C`, `D`). Keep question labels as `Q1`, `Q2`, etc., so the user can answer compactly, for example `Q1=2, Q2=4`.

Each question should say why the answer matters. Do not attach a recommended answer or default when eliciting facts, interpretations, values, goals, constraints, lived experience, or a pivotal trade-off; doing so would bias the diagnosis. A recommendation may be included only for a bounded downstream implementation choice after the problem is already framed. When helpful, mention what was checked so the user can see why this is a real gap. Format it like this:

```
❓ **Q1** - **<question title>**: <question body, might be multiple paragraphs, including multiple choices>

```

Do not force a multiple-choice format when a short open answer is more natural. Do not repeat settled questions in later rounds. If the user sounds tired or says the detail should already exist, stop questioning, inspect the sources again, summarize what is known, and return only with any remaining material gap.

## Stop at 95% confidence

After the initial investigation and after every answer round, assess whether you have at least **95% practical confidence** that you can give a useful, evidence-grounded solution. This is a decision-readiness threshold, not a mathematical probability. It is met when the real problem or decision, goal, success criteria, constraints, evidence boundary, main contrary explanations, and conclusion-changing variables are clear enough that remaining unknowns would not change the recommended direction or next action.

If the threshold is met, stop asking immediately and give the solution. Do not continue merely to visit every branch, eliminate harmless uncertainty, or make the interview feel complete. State any remaining assumptions or evidence limits that matter, but do not turn minor uncertainty into another question. If the threshold is already met after investigation, ask no questions at all.

If confidence remains below 95%, ask the next mode-appropriate frontier question or round and explain why the answer could change the solution. There is no fixed maximum number of questions. Reassess after every answer round.

Do not chase unreachable certainty. If a material fact cannot be obtained, evidence has stopped reducing uncertainty, or the user cannot supply a required preference, do not pretend to have 95% confidence and do not continue indefinitely. State the exact blocker, what would resolve it, and any safe conditional conclusion that the evidence supports.

The session is done when the 95% threshold is met: material branches are settled, assumptions and evidence limits are visible, and remaining unknowns would not change the recommended next step. Follow the selected mode's output contract. Grilling does not itself authorize implementation, high-risk actions, external changes, or expansion of scope; preserve any genuine approval or safety gate required for execution.
