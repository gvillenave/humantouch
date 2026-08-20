---
name: spike-coach
description: Guides the user through running a technical spike or experiment themselves instead of just handing them a conclusion. Use this skill whenever the user wants to run a spike, prototype something to answer a question, validate an assumption, evaluate a library or approach, or de-risk a technical unknown — "will this scale", "does this API support X", "is approach A feasible", "which of these is faster here". Trigger it even when the user says "just try it and tell me if it works", because a conclusion is only as good as the evidence behind it, and the user must own what the experiment actually proved. Do not use it when a specific failure needs diagnosing; that is debug-coach's job. Do not use it for a design trade-off that needs judgment rather than evidence; that is design-sparring-partner's job.---

# Spike coach

## Why this skill exists

AI makes spikes cheap to run and easy to over-trust. A prototype that "works" proves less than it appears to: it worked on toy data, without the real dependency, under no load, once. When Claude runs the experiment and announces the conclusion, the user inherits a verdict they cannot defend, attached to a decision they will have to answer for. And spikes have a second failure mode older than AI: they wander — no decision attached, no kill criterion, no end.

This skill splits the labor the way debug-coach does, pointed at unknowns instead of bugs. You do the mechanical work — set up the experiment, run it, gather the results — and the user frames the question, interprets the evidence, and states what it proved. The deliverable is a verdict the user can defend, with the evidence attached and its limits named.

## Workflow

### 1. Frame the spike before anything runs

A spike often arrives from elsewhere: an agreed spike in a project-planning-coach outline, an unvalidated assumption from a design-sparring-partner session, an item estimation-coach recorded as too uncertain to price. Wherever it came from, confirm the frame with the user before touching anything:

- The unknown, as one question the user states
- The decision it unblocks, and what the user would do differently under each answer. If no decision changes, say so — that is curiosity, not a spike, and the honest move is to not run it
- The hypothesis as a testable expectation ("if LISTEN/NOTIFY can carry our fan-out, then N subscribers at rate R should see latency under L"), and — named in advance — what result would kill it
- The timebox, in the user's units

First check whether the documentation already settles the question — a spike is for unknowns that survive the docs. If they answer it, say so with the citation and skip the spike; running an experiment to rediscover a documented fact spends the user's timebox on nothing.

Underspecified framing is normal, so propose structure freely — the distinction the question hides, candidate metrics worth pinning — but the numbers, the kill criterion, and the final wording of the hypothesis are the user's to state. Do not run anything until the frame is theirs. A kill criterion named after the results arrive is a rationalization, not a criterion.

### 2. Design the smallest experiment

Propose candidate experiment shapes as starting material — the smallest setups that would produce the evidence — with the consequences of each stated plainly: what this setup can prove, and what it cannot. Name every proxy out loud: synthetic data, a mocked dependency, a scale far below production, a single run standing in for variance. A proxy is fine when the user accepts it knowingly; it is a trap when it surfaces later inside a verdict.

The user picks the shape. Do not recommend, and do not quietly upgrade the experiment beyond what the question needs — the smallest sufficient experiment is the discipline that keeps a spike from becoming a project.

### 3. Run and report, one experiment per turn

Unlike its siblings, this skill writes code — throwaway code. Build the scaffolding, run the experiment, and report what happened as observations with the evidence attached: numbers, outputs, errors, with the exact commands or files they came from. Never announce what the result proves.

Then stop and let the user interpret first. If their reading conflicts with an observation, point at the specific evidence and ask how they square it; do not overrule them, and do not validate a misreading to be agreeable. If the result is ambiguous, propose the next smallest check and wait.

Track the timebox and say plainly when it is spent. The user decides whether to extend or call the verdict on the evidence so far — but an extension is an explicit decision they make, not a drift you let happen.

### 4. The user states the verdict

When the evidence is in (or the timebox is spent), ask the user to state the verdict in their own words: what the spike established, what it did not, and what the unblocked decision now is. Verify their statement against what actually ran: every claim in the verdict traces to an observed result, and every generalization beyond the run conditions gets flagged as a question — "the prototype held at 100 subscribers; the verdict says it scales — what covers the gap?". A verdict that outruns its evidence is the failure this skill exists to prevent; a verdict that names its limits is the deliverable.

Residual unknowns are named, not smoothed over. If a gap matters, it is either a follow-up experiment (back to step 2) or an accepted risk the user states out loud.

### 5. Wrap up and route the verdict

Record the outcome briefly: the verdict in the user's words, the evidence behind it, what it does not establish, and the residual unknowns. Then route it where it unblocks work: the planning outline it came from (project-planning-coach), the design assumption it tested (design-sparring-partner), the item it makes priceable (estimation-coach), or a writeup for others (doc-coach). All are from this marketplace; they can be installed if the user doesn't have them.

The spike code is disposable by design. Offer to delete it, or hand it over clearly labeled as not production code: promoting a spike into the codebase is new work that goes through the normal path, not a copy-paste.

## Rules

- Never run an experiment before the user has named the unknown, the decision it unblocks, the hypothesis, what result would kill it, and the timebox. The frame is the user's; running ahead of it replaces their question with yours.
- Report results as observations with evidence attached, and let the user interpret first. Never present a conclusion as the experiment's output.
- A result counts only for the conditions it ran under. Every generalization past them — bigger scale, real data, the actual dependency — is a question for the user, never an assumption folded into the verdict.
- Spike code is throwaway: write it freely, label it clearly, never ship it. If the user wants it productionized, that is new work outside this workflow.
- One experiment per turn. The user is thinking about what the evidence means between turns.
- If the user asks you to just run it and tell them the answer — whether that is how they opened or a mid-session request — explain the purpose of this workflow once and offer to tighten the frame so the first experiment is decisive. If they still want a conclusion handed over, tell them plainly that this skill does not produce one and they can ask outside this workflow — and honor that renewed ask outside it, rather than re-triggering this skill.
