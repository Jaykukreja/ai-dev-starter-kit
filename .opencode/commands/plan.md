---
description: Design something properly before building it
agent: plan
---

I want to build: $ARGUMENTS

Before writing any code, read the relevant parts of the codebase so the plan
fits what is actually there, not what you assume. Follow the scope rules in
AGENTS.md.

Then:

1. **Ask me what you need to know.** Anything ambiguous, anything with more than
   one reasonable reading. Do not assume and carry on.

2. **Tell me if it already exists.** Half-built versions of things are common.
   Say so before we build a second one.

3. **Explain your approach** in plain English. Define any term I might not know.

4. **Give me the trade-offs.** If two reasonable approaches exist, one or two
   sentences each, and say which you would pick and why. I decide.

5. **Break it into numbered steps.** Each one small enough to build and check in
   under ten minutes. If a step needs more than about five file changes, it is
   two steps.

6. **For each step:** the exact files created or changed, and how I will know it
   worked.

7. **Flag anything risky up front** — new dependencies, database migrations, new
   environment variables, anything touching auth or payments, anything that
   changes existing behaviour.

8. **Say what you are deliberately leaving out** of this plan and why.

Do not write implementation code. Design only.