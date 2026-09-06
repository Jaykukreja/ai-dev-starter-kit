---
description: Build one step from the plan
agent: build
---

Build this one step: $ARGUMENTS

Before you write anything, read the files this will touch plus one or two
similar files elsewhere, and match what is already there. Then tell me in one
sentence what you are about to change and why.

Only this step. Nothing extra. Follow every rule in AGENTS.md.

Stop and ask instead of proceeding if it needs a new dependency, a database
migration, a new environment variable, more than five file changes, or if the
plan conflicts with what is actually in the code.

When done, tell me:
- What changed, one line per file
- How to check it worked — the exact command or the exact thing to click, and
  what I should see
- What you noticed but deliberately left alone, and why
- What could break elsewhere as a result