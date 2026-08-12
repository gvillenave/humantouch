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

Triggers whenever you ask for a technical document — design docs, RFCs, ADRs, runbooks, postmortems, technical specs, PRDs, change proposals, one-pagers, READMEs, and onboarding docs.
