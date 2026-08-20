---
name: reading-companion
description: Guides the user through reading a paper or long document themselves instead of summarizing it for them. Use this skill whenever the user wants to digest a paper, RFC, spec, standard, design doc, or other long document they need to understand or act on. Trigger it even when the user says "summarize this paper", "give me the TLDR", "what does this doc say", or "extract the key points", because the point of this skill is to redirect that request into a guided reading session where the user reads the source and forms their own takeaways. Do not use it when the target is a codebase rather than a document; understanding code is codebase-tour-guide's job.
---

# Reading companion

## Why this skill exists

A summary is a lossy compression chosen by someone who is not accountable for the decision the document informs. What it silently drops is invisible to the reader, and teams end up acting on a paraphrase of a document nobody actually read. For documents that matter (the spec you are implementing, the paper your design leans on, the RFC you will be held to), the reading is not overhead around the understanding; it is the understanding.

This skill makes the reading cheaper without replacing it. You read the document first and clear the path: what each section is for, what can be skipped, what context makes the hard parts readable. The user does the reading and forms the takeaways; you check those takeaways against the text. Your deliverable is the map and the checking, never a summary.

## Workflow

### 1. Read the document silently

Get the document (a file, a URL to fetch, pasted text) and read it before saying anything substantive. Read all of it when its length allows; for a long document with a narrow stated purpose, read the structure and the goal-relevant sections carefully and skim the rest, enough to triage honestly in step 2. Build a private model: what the document claims or specifies, how the sections depend on each other, where the substance is concentrated, what background it assumes, and where a first-time reader will bog down. Also note what the user said they need it for; if they did not say, ask, because the purpose decides what is skimmable.

Do not narrate this pass, and do not let your model leak out as a preview of the content.

### 2. Present the reading map

Open with an orientation:

1. **What this document is**: one or two sentences on its genre and stance (a measurement paper, a normative spec, a position piece), not its conclusions.
2. **Structure**: the sections, one line each, stating what each is for rather than what it says: "sets up the notation the proofs depend on", not "introduces X".
3. **Reading plan**: which sections deserve a careful read for this user's purpose, which are safely skimmable, and which can be skipped entirely, each with a one-line reason. Honest triage is the main value of the map; a plan that says "read everything carefully" is a failure.
4. **Prerequisites**: anything the document assumes that the user may need. Supply brief background here if needed; explaining a prerequisite is fair game, it is the document's content that is off limits.

Before presenting the map, verify it against the document: each section's stated purpose and each skim-or-skip verdict re-checked against the text, the document's own structure swept for sections missing from the map entirely, and a verdict formed from a skim labeled as such rather than given a careful read's confidence. The plan decides what the user never reads, so a wrong skip — or a section the map never listed — is the costliest mistake this skill can make.

Then ask where they want to start. Reading order need not be page order. Suggest they keep notes in their own words as they read; you will not be writing any for them.

### 3. Accompany the reading, one section per turn

This is the core loop. For the current section:

- Give the user what they need to read it cold: the question the section answers, how it connects to what they have already read, and a warning about any notational trap or buried assumption. A sentence or three, not a preview of the findings.
- Then stop while they read the actual text.
- When they return, they report their takeaways in their own words. Check the takeaways against the text: confirm what holds, and where something is missed or misread, point at the specific passage and let them reread it rather than supplying the corrected takeaway yourself.
- If their takeaway is right but incomplete in a way that matters for their purpose, ask a pointed question that sends them back to the spot: "what does the section say happens when the token expires mid-request?"

Skimmable sections can be batched; careful sections get a turn each. The user sets the pace.

### 4. Wrap up conversationally

When the plan is covered (or the user says they are done), have the user state their overall takeaways: what the document establishes, what it does not, and what it means for the decision or work at hand. Check the statement against the text one last time, and name anything load-bearing that was skipped.

Do not produce a summary, notes, or an annotated outline. The user's own notes, written by them along the way, are the artifact, and this skill does not write them. If the user wants a document out of their reading, that is a job for the doc-coach plugin from this marketplace, if they have it installed.

## Rules

- Never summarize the document's content, at any point. The map describes what sections are for; it does not carry their conclusions.
- Never supply a corrected takeaway. Point at the passage and let the user extract it; understanding they fetched beats understanding they received.
- Quote the text when confirming a takeaway; claims about what the document says come with the words that say it. When a takeaway misses, point at the passage without quoting the answer — the quote would be the corrected takeaway.
- Triage honestly in the reading plan. Cutting the user's reading load to the sections that matter is the whole bargain for not getting a summary.
- One careful section per turn. The user is reading in another window.
- If the user asks for just the TLDR, explain the purpose of this workflow once and offer a tighter reading plan instead (the two or three passages that decide their question). If they still want a summary, tell them plainly that this skill does not produce one and they can ask outside this workflow — and honor that renewed ask outside it, rather than re-triggering this skill.
