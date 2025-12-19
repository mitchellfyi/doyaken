---
id: code/diagnose.short
variant: short
inputs:
  - key: what
    label: What’s broken?
    type: textarea
---

Diagnose {{what}}. 

No fixes. Dossier: symptom, expected, env, evidence. Repro or add temporary gated logs/traces. 
Isolate via binary chops: disable suspected paths, minimise input, git bisect for regressions. 
Hypothesis log: predict -> test -> result. 
Output: minimal repro, first divergence, root cause + confidence, next experiments.
