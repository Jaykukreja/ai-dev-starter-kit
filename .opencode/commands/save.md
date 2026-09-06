---
description: Commit my work safely
agent: build
---

Help me save my work.

1. Show me what has changed: !`git status --short`

2. Check for anything that must not be committed — secrets, API keys, tokens,
   connection strings, `.env` files, large binaries, debug logging left in.
   Flag them and stop.

3. Tell me if this looks like more than one logical change. One commit per
   feature or fix keeps history useful.

4. Suggest a commit message describing WHY, not just what. Reference a ticket
   if the branch name has one.

5. Show me the exact command. Wait for my approval before running anything.

Never `git push` unless I explicitly ask. Never `git reset`, never
`git commit --amend`, never force anything.