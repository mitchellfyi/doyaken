---
id: code/review.short
variant: short
title: Review - strict (short)
tags: [review]
inputs:
  - key: what
    label: What to review?
    type: textarea
---

Ruthless review of {{what}}. 
Follow repo instructions. 
Ledger (threads/findings). 
Multi-pass: behaviour, design/complexity, security (OWASP), perf/reliability, tests/docs. 
Fix by severity with small commits + tests/docs. No workarounds or skips.
Run repo checks (fmt/lint/type/tests/build/security/migrations/docs). O
Output risks + PR summary.
