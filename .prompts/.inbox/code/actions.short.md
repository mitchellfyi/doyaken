---
id: code/actions.short
variant: short
title: CI - GitHub Actions (short)
tags: [ci, github-actions]
inputs:
  - key: what
    label: What should CI do?
    type: textarea
---

Design/update Actions for {{what}}.

Read repo instructions first. 
Keep YAML thin - call repo scripts (follow existing scripts convention). 
Set least-privilege permissions, pin 3rd-party actions to SHAs, 
add PR concurrency cancel-in-progress, cache deps, upload failure artefacts, document workflows + how to run locally, 
and include a clear debug mode. Ensure required checks match workflow job names.
