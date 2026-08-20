# humantouch

A [Claude Code plugin marketplace](https://code.claude.com/docs/en/plugin-marketplaces) with plugins that keep humans in the loop and doing the thinking.

## Installation

Add this marketplace in Claude Code:

```
/plugin marketplace add gvillenave/humantouch
```

Then install a plugin:

```
/plugin install doc-coach@humantouch
```

## Plugins

### doc-coach

Guides you through writing your own technical document instead of generating one for you.

AI-generated docs are verbose and let the author skip the thinking. doc-coach inverts the workflow: Claude does the analytical work and delivers structured raw material and guidance section by section, but you write every sentence of the final document. The result is a shorter, human-voiced doc that reviewers can trust you have thought through.

Triggers whenever you ask for a technical document — design docs, RFCs, ADRs, runbooks, postmortems, technical specs, PRDs, change proposals, one-pagers, project plans and briefs, READMEs, and onboarding docs.

### pr-review-companion

Guides you through manually reviewing someone else's pull request instead of reviewing it for you.

An automated review hands you verdicts and lets you skip the reading. pr-review-companion keeps you in the loop: it explains the PR's scope, breaks the change into logical components, and walks through them one at a time — flagging risks and inconsistencies while you look at the code and form your own judgment. It ends with you informed, not with a findings report.

Triggers whenever you ask to review a PR or changeset someone else authored, want to be walked through a diff, ask what to look at in a change, or share a PR link or pasted diff to review. Self-review of your own changes is handled outside it.

### debug-coach

Guides you through diagnosing and fixing a bug yourself instead of patching it for you.

An AI-written patch can make a symptom disappear without anyone understanding the disease. debug-coach keeps you in the driver's seat: Claude reproduces the failure and gathers the evidence, then presents ranked hypotheses and walks the investigation one step at a time while you interpret the results, state the diagnosis, and write the fix.

Triggers whenever you ask to fix a bug, debug a failure, or investigate a crash, an error, or unexpected behavior.

### design-sparring-partner

Stress-tests your system design decisions instead of producing an architecture for you.

An architecture you didn't build is one you can't justify when the trade-offs bite. design-sparring-partner interviews you about constraints, frames one trade-off at a time with concrete consequences, and attacks each decision you make with specific failure scenarios — so weak choices break in the conversation instead of in production. It ends with decisions you can defend, not a design document.

Triggers whenever you ask to design a system, choose an architecture, or weigh technical approaches.

### test-design-coach

Helps you decide what to test instead of generating a test suite for you.

Generated tests assert what the code does, not what it should do, freezing bugs in place as passing tests. test-design-coach maps the code's risk surface, then asks you, unit by unit, what behavior you would protect and what input breaks it. You name the cases, and Claude points at the branches you missed as questions. Once a case is specified in your words, you choose: write it yourself, or approve it for Claude to implement exactly as specified.

Triggers whenever you ask to write tests, add coverage, or test a piece of code.

### codebase-tour-guide

Walks you through reading an unfamiliar codebase instead of summarizing it for you.

A summary produces the feeling of understanding without the substance. codebase-tour-guide gives you a map and a route, then guides you one stop at a time: you read a specific file, predict what it does, and Claude checks your prediction against the code. The tour ends when you can sketch the system from memory.

Triggers whenever you ask to understand a codebase, get an overview of a project, or onboard onto unfamiliar code.

### reading-companion

Guides you through reading a paper or long document instead of summarizing it for you.

A summary silently drops what its author didn't think mattered, and you can't see what's missing. reading-companion reads the document first and clears the path: which sections carry the substance, which are skimmable, and what context makes the hard parts readable. You do the reading and report your takeaways; Claude checks them against the text.

Triggers whenever you ask to digest, summarize, or extract key points from a paper, RFC, spec, or long document.

### project-planning-coach

Guides you through decomposing a coding project into an execution plan you own, instead of generating a plan for you.

A generated plan invents plausible tickets no source asked for and omits real work — and both failures surface mid-execution, when they cost the most. project-planning-coach splits the labor: Claude mines your docs, tickets, and codebase for the actual work, dependencies, and unknowns, while you make every scoping, sequencing, and milestone decision. The result is an outline of steps, dependencies, milestones, and tickets you can defend — verified claim by claim against your sources before handoff, with discrepancies flagged for you to settle — and the raw material for doc-coach when you need a shareable plan document.

Triggers whenever you ask to break down a project, plan or sequence implementation work, create tickets from a design doc or spec, or draft a roadmap or milestones.

### estimation-coach

Guides you through estimating your own work instead of producing numbers for you.

An AI-generated estimate is a confident number nobody can defend — and it anchors: once it's on screen, it becomes the plan. estimation-coach keeps the numbers yours: Claude maps what each ticket actually touches — hidden work, unknowns, evidence from comparable past changes, and how AI-assisted coding reshapes the effort — then you name every number and defend it against a concrete stress test. The result is an estimate sheet you can commit to, verified against your words and sources.

Triggers whenever you ask to estimate tickets or a project, size a backlog, assign story points, or judge whether a deadline is realistic.

## Design principles

Every plugin follows the same contract: Claude does the legwork, you do the thinking, and nothing is presented as checked unless it actually was. Verification takes two forms, and skills use whichever fits each moment. Claims checked as they are used are verified inline — debug-coach runs the code instead of predicting it, codebase-tour-guide and reading-companion check each answer against the source as you go. Any skill that opens with a map or orientation — a code map, a reading plan, a component map, a risk surface, an estimation surface — verifies it against its sources before presenting it, because what opens the session steers all of it. And material assembled and handed over in bulk — an outline, raw material for a document, a wrap-up recap — gets a verification pass before the handoff:

- Re-check every claim against the source it came from.
- Sweep the reverse direction: nothing in scope in the sources is missing from what is handed over.
- Flag every discrepancy to the user as a decision; never reconcile one silently.
- Converge before presenting: anything left unverified is labeled as such, never passed off as checked.

Every workflow also shares the same escape hatch: if you ask for the generated artifact instead, the skill explains its purpose once — and if you still want it, honors that ask outside the workflow rather than refusing forever or re-triggering.

Each skill carries its own adapted, self-contained wording of these conventions, so every plugin stays independently installable.
