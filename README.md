Language: [English](#english) | [中文](README_zh.md)

# Feature Dev

A **Knowledge-Driven Development (KDD)** AI Coding skill for Claude Code. Before writing any code, it reads your team's project knowledge from an Obsidian vault — architecture, conventions, data schemas, historical decisions — so every implementation decision is grounded in real business context, not guesswork.

## Why

AI writes code fast. But in real projects, the hardest part isn't *how* to write the code — it's knowing which module is affected, what a field actually means, whether a legacy rule still applies, or why that one table must go through cache.

This skill enforces a simple rule: **AI must read project knowledge before it writes code.**

## The 6-Stage Flow

```
Requirement → Knowledge Loading → Clarification → Plan → Coding → Testing → Archive (manual)
```

1. **Requirement** — Pull or paste the task
2. **Knowledge Loading** — Read `INDEX.md` from the Obsidian vault, match relevant docs
3. **Clarification** — Ask questions informed by loaded knowledge
4. **Plan** — Output a change plan with cited knowledge sources
5. **Coding** — Implement following project architecture & conventions
6. **Archive** — Manually triggered; summarize what was learned back into the vault

## Setup

1. Organize your project knowledge in Obsidian under a directory like `coding/your-project/`. Must include an `INDEX.md`.

2. Place `feature-dev.json` next to the skill file:

```json
{
  "knowledge_base_root": "/path/to/your/obsidian/coding"
}
```

The skill auto-matches your current project directory name to the Obsidian vault subdirectory.

3. Invoke the skill in Claude Code:

```
/feature-dev
```

## Prerequisites

- [Obsidian](https://obsidian.md) with a project knowledge vault
- Optional: Obsidian MCP server for richer knowledge access
- Optional: A task/requirement MCP service

## Key Design

- Knowledge is the source, not prompts — architecture, conventions, and glossary live in Obsidian, not in `CLAUDE.md`
- Every plan decision must cite a source: knowledge doc, code artifact, or user confirmation
- A traceability table links requirements → knowledge → changes → tests → archive
- Knowledge expiry: when vault docs conflict with actual code, the doc is flagged as stale
