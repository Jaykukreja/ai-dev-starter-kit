---
description: Review the code before I commit it
agent: plan
---

Review what has changed: !`git diff`

Check for:
1. Anything that will break.
2. Secrets, API keys, or passwords that should not be committed.
3. Anything that ignores the rules in AGENTS.md.
4. Error cases that are not handled.
5. Anything I would struggle to understand in a month.

Report problems first, in order of how bad they are. Then say whether this is
safe to commit. Do not fix anything — I want to fix it myself so I learn.
