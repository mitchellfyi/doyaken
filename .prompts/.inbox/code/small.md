---
id: code
variant: short
title: Code - build, fix, improve, review (short)
tags: [code]
inputs:
  - key: what
    label: What should I work on?
    type: textarea
---

Define "done" from CI/scripts/lint/tests. No hacks - fix root causes. 
For each item: restate, implement smallest clean change, add/adjust tests, update docs.
Apply DRY/SOLID/KISS/YAGNI. 
Run format+lint+typecheck+tests+build+security/migrations/docs as relevant. 
Output pass/fail vs intent + summary + risks + PR comment.
