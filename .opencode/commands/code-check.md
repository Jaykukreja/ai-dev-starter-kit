---
description: Review code against our standards before committing
agent: plan
---

Review this code: $ARGUMENTS

If no target was given, run !`git diff --stat` and review only the changed
files. If nothing has changed, run !`git ls-files` and review tracked source
files. If more than 20 files would be in scope, stop and ask which folder.

Review against every rule in AGENTS.md.

Report by severity: things that will break, then security, then standards
violations, then suggestions.

For each item: what it is, where it is (file and line), why it matters. Explain
the reasoning — the point is that I understand it, not that I obey it.

Do not fix anything. I fix it myself.

Finish with a one-line verdict on whether this is safe to commit, and list any
rules you skipped as not applicable to this project type.