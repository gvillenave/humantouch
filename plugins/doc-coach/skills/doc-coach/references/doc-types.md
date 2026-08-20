# Technical document types

Starting points for outlines. Adapt to the audience and cut aggressively. Each section lists the question it answers for the reader. "Failure mode" is what to warn the user about for that doc type.

## Design doc / RFC

Purpose: get reviewers to a confident yes/no on a proposed approach.

- Summary: what is proposed and why should I keep reading?
- Context and problem: what hurts today, and for whom?
- Goals and non-goals: what does success mean, and what is explicitly out of scope?
- Proposed design: what will be built, at the level reviewers need to judge it?
- Alternatives considered: what else was on the table and why not?
- Risks and open questions: what could go wrong, what is undecided?
- Rollout plan: how does this land safely?

Failure mode: exhaustive detail in the design section while alternatives get one dismissive line each. Reviewers care most about the alternatives.

## ADR (architecture decision record)

Purpose: record one decision and its reasoning so future readers do not relitigate it.

- Status and date: is this decision active?
- Context: what forces made a decision necessary?
- Decision: what was decided, in one or two sentences?
- Consequences: what gets better, what gets worse, what are we now committed to?

Failure mode: length. An ADR longer than a page stops being read. Push the user toward brutal brevity.

## Runbook

Purpose: let an on-call responder act correctly under stress, possibly at 3am, possibly unfamiliar with the system.

- Symptoms: how do I know I am in this scenario?
- Impact: who is affected and how urgent is this?
- Diagnosis steps: how do I confirm the cause, in order?
- Remediation: exact commands and actions, with expected output.
- Escalation: when do I stop and page whom?

Failure mode: explanation where instruction is needed. Every step must be executable verbatim by someone who does not understand the system. Background belongs elsewhere.

## Postmortem

Purpose: turn an incident into prevention without assigning blame.

- Summary and impact: what happened, how bad, for how long?
- Timeline: what happened when, including detection and mitigation?
- Root cause and contributing factors: why did this happen, beyond the trigger?
- What went well / what went poorly: what should we keep or fix in our response?
- Action items: what specific changes, owned by whom, by when?

Failure mode: a timeline dump with no analysis, or action items too vague to verify ("improve monitoring").

## Technical spec

Purpose: define behavior precisely enough that implementers and testers agree on done.

- Overview: what is being specified and for whom?
- Requirements: what must the system do, numbered and testable?
- Interfaces and data: what are the exact contracts?
- Edge cases and error behavior: what happens when things go wrong?
- Out of scope: what should implementers not build?

Failure mode: ambiguity hiding in prose. Push the user toward numbered, testable statements.

## README / onboarding doc

Purpose: get a newcomer from zero to productive with minimum reading.

- What this is: one paragraph, what does this project do and for whom?
- Quick start: shortest path to running it locally.
- Common tasks: the 3 to 5 things people actually come here to do.
- Where to learn more: links, owners, support channels.

Failure mode: completeness. READMEs rot in proportion to their length. Everything beyond the quick start should be a link, not content.

## PRD (product requirements document)

Purpose: align product and engineering on what to build and why, before anyone designs how.

- Problem and opportunity: what user problem exists, and what evidence supports it?
- Goals and success metrics: how will we know it worked, in numbers?
- Users and use cases: who is this for and in what scenarios?
- Requirements: what must the product do, prioritized (must / should / could)?
- Out of scope: what are we deliberately not building?
- Open questions and dependencies: what is unresolved or blocked on others?

Failure mode: solutioning. A PRD that prescribes implementation crowds out the problem and requirements, and success metrics that cannot be measured make the whole doc unfalsifiable.

## Change proposal

Purpose: convince stakeholders to replace an existing process, architecture, or standard with a better one.

- Current state: how does it work today, and why was it built that way?
- Problem: what does the status quo cost us now, with evidence?
- Proposed change: what specifically changes, stated as before and after?
- Impact and migration: who is affected, what must they do differently, and how do we transition?
- Alternatives, including doing nothing: why is this change worth the disruption?
- Deprecation and timeline: when does the old way stop being supported?

Failure mode: ignoring why the current state exists and understating migration cost. A proposal that does not steelman the status quo alienates the people who own it, and they are usually the approvers.

## Proposal / one-pager

Purpose: get a decision maker to approve direction and resources.

- Ask: what decision or resources are being requested?
- Why now: what happens if we do nothing?
- Plan: what will be done, at milestone level?
- Cost and risk: what does this take and what could sink it?

Failure mode: burying the ask. Decision makers read the first five lines; the ask goes there.

## Project plan / brief

Purpose: give stakeholders enough confidence in the shape of upcoming work to endorse it: what will be built, in what order, and what done means.

- Goal and non-goals: what exists at the end, and what is explicitly not being done?
- Milestones: what lands, in what order, and what does "done" mean for each?
- Dependencies and sequencing rationale: why this order, and what blocks what?
- Risks, unknowns, and spikes: what could move the plan, and what is being derisked first?
- Deferred work: what was consciously pushed out, so it reads as a decision rather than an omission?

Failure mode: pasting the ticket backlog into the document. Stakeholders need the shape of the work and the reasoning behind the order; ticket-level detail belongs in the tracker, linked rather than inlined.

Variant — kickoff doc: same skeleton, different audience. The purpose is aligning the team that will do the work, not winning endorsement: lead with ownership, sequencing, and how decisions will get made. Failure mode: writing an approval pitch for people who already said yes.
