---
id: code
variant: docs_short
title: Docs (short)
tags: [docs]
inputs:
  - key: what
    label: What to document/sync?
    type: textarea
---

Make docs match reality for {{what}}. 
Read AGENTS/CLAUDE/GEMINI/Copilot + README/CONTRIBUTING. 
AGENTS.md is source of truth; other agent files only point to it. 
Add brief inline “why/trade-off” comments; use ADR for big decisions. 
Delete stale docs. Verify against CI/workflows/scripts. 
Output changed files + gaps.
