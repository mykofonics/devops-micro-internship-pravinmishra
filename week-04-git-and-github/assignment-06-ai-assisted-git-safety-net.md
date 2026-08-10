Assignment 6 — Building an AI-Assisted Git Safety Net (PR Ready Check)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

Task 0 — Confirm Your Fork and Create a Feature Branch

Screenshot 1 — Output of git remote -v and git branch showing the new branch

<img src="screenshots\Task_6_0_1.png">

Notes

**1. Why create a dedicated branch instead of doing this work on main?**

A feature branch isolates my changes from main, keeping the main branch stable while I develop and test. It enables focused code reviews through Pull Requests and prevents unfinished or faulty work from affecting the primary branch.

Task 1 — Stage a Change With Realistic Risk

Screenshot 1 — Output of  `git status` showing the staged file on feature/ai-pr-ready
<img src="screenshots\Task_6_1_2.png">

Notes

**1. Why does this assignment use an obviously fake key instead of a real one?**

A fake AKIA-formatted key safely tests secret-detection mechanisms by matching the structure of a real AWS key without exposing valid credentials. This validates the detection process while avoiding any security risk.



# Task 2 — Write a Real Git Pre-Commit Hook

Screenshot 2 — `hooks/pre-commit` open in VS Code showing the full script

<img src="screenshots\Task_6_2_3.png">

Screenshot 3 — Output of `git config core.hooksPath` confirming it points to `hooks`

<img src="screenshots\Task_6_2_4.png">

Notes

**1. Why is `hooks/pre-commit` tracked in the repo instead of living only in `.git/hooks/`?**

Since .git/hooks isn't tracked by Git, hooks aren't shared with collaborators. Using a tracked hooks/ directory with core.hooksPath ensures every developer uses the same version-controlled hook.



**2. Compare this to `PreToolUse` from Week 2 Assignment 6. What does each one intercept, and what do they have in common?**

PreToolUse blocks unsafe AI tool calls before execution, while a Git pre-commit hook blocks unsafe commits before they're created. Both act as automated policy gates, enforcing fixed rules before irreversible actions occur.


Task 3 — Prove the Hook Blocks the Risky Commit

Screenshot 4 — Terminal showing `git commit` rejected with the hook's "BLOCKED" message naming the exact file
<img src="screenshots\Task_6_3_5.png">

Notes

**1. Which line in `hooks/pre-commit` matched your fake key, and why did it match?**

if git diff --cached -- "$file" | grep -qE 'AKIA[0-9A-Z]{16}|-----BEGIN (RSA|OPENSSH|PRIVATE) KEY-----'; then
It matched because the regex AKIA [0-9A-Z]{16} looks for "AKIA" followed by 16 uppercase letters/digits — and AKIAABCDEFGHIJKLMNOP fits that exact shape.


**2. Could this hook have caught a poorly-named variable that stores a secret without the `AKIA` prefix? What does that tell you about the limits of a fixed rule like this?**

It can't catch that — the hook only matches its exact patterns (AKIA... or PEM headers), not variable names or context. This shows a fixed rule only catches what it's explicitly written to look for; anything outside that exact shape slips through undetected. 
 
Task 4 — Build the `/pr-ready` Skill


Screenshot 5 — `SKILL.md` frontmatter showing `allowed-tools: Bash, Read, Grep` (no `Write`) and `disable-model-invocation: true`

<img src="screenshots\Task_6_4_6.png">

Screenshot 6 — `/pr-ready` output while the risky file is still staged, showing it flagged the secret and/or debug statement
<img src="screenshots\Task_6_4_7.png">

Notes

**1. Why does `/pr-ready` have `Bash` and `Read` but not `Write`?**

/pr-ready requires only Bash and Read permissions to inspect Git status, staged changes, and file contents. It intentionally excludes Write, ensuring the AI can analyse and advise but cannot modify files, commit, or push changes, following the principle of least privilege.



**2. The pre-commit hook and `/pr-ready` both looked at the same staged diff. Did they flag the same things? What did one catch that the other didn't?**

Both the pre-commit hook and /pr-ready detected the fake AWS key, but only /pr-ready identified the leftover debug statement because it understands context, not just patterns. The hook provides automatic enforcement, while /pr-ready offers contextual review and recommendations. Together, they complement each other by combining deterministic checks with AI-assisted analysis.



Task 5 — Fix the Issues and Re-Verify

Screenshot 7 — `git commit` succeeding after the fix (no BLOCKED message)

<img src="screenshots\Task_6_5_8.png">

Screenshot 8 — Second `/pr-ready` run showing a clean risk report and a drafted PR title + description

<img src="screenshots\Task_6_5_9.png">

Notes

**1. What exactly did you change to satisfy the pre-commit hook?**

I replaced the hardcoded AWS key with an environment variable, following secure secret management practices, and removed the debug statement that exposed the credential. These changes satisfied both the pre-commit hook and /pr-ready by eliminating hardcoded secrets and preventing credential leakage without affecting the script's functionality.



Task 6 — Push and Open a Pull Request Using the AI Draft

Screenshot 9 — Your Pull Request showing the base repository is your own fork, plus the title and description, with the `/pr-ready` draft visible for comparison (paste it in the PR conversation or your notes below)

<img src="screenshots\Task_6_6_10.png">
<img src="screenshots\Task_6_6_10b.png">


#### PR Link


### Notes

**1. What, if anything, did you edit in the AI's drafted PR description before using it? Why?**

I revised the AI-generated PR description to include all major changes and removed any unverified claims. This ensures the Pull Request accurately reflects the completed work and only makes assertions I have confirmed myself.



**2. If you had blindly copy-pasted the AI's draft without reading it, what could go wrong?**

An AI-generated PR description is only a draft. I reviewed and refined it to ensure it accurately represented the completed work, included all key changes, and contained only claims I had personally verified.

**3. Why does this PR need to target your own fork instead of the shared upstream repository?**

This work is specific to my learning environment, so I opened the PR within my own fork instead of upstream. This keeps the shared repository clean while still demonstrating the complete Git and GitHub workflow.


Task 7 — Map the Workflow to the Agentic Loop


Notes

**1. Which step(s) represent Gather?**

The pre-commit hook running git diff --cached and file size checks, and /pr-ready running git diff --cached/git status — both collect raw facts about the staged changes before judging anything. 

**2. Which step(s) represent Analyze?**

The hook checks the diff against its regex/size rules, and /pr-ready reviews the same diff for secrets, debug code, mixed concerns, and drafting a PR title/description. 

**3. Which step is the human act, and why must a human—not Claude—run `git commit`, `git push` commands and open the PR?**

Editing scripts/notify.sh, running git commit, git push, and opening the PR. A human must do this because these actions are irreversible and externally visible—/pr-ready was built without write access and was told never to commit, push, or open PRs, so only a person can take responsibility for the actual change. 

**4. Which step is Verify?**

Re-running the hook and /pr-ready after the fix—the commit succeeding with no BLOCKED message and /pr-ready reporting a clean risk report—confirms the issue is actually resolved. 

**5. In one or two sentences: Why do you need *both* the fixed-rule pre-commit hook and the AI skill? Isn't one enough?**

The hook guarantees deterministic, zero-tolerance enforcement but only for exact patterns it knows; the AI catches contextual issues (like debug code or mismatched descriptions) a fixed rule can't express but can't be trusted to catch everything or act on its own—so you need the hook for certainty and the AI for judgment. 

Task 8 — LinkedIn Post

LinkedIn Post URL
https://www.linkedin.com/posts/oyeku-michael-2215a920_dmibypravinmishra-git-github-ugcPost-7486545775964069888-GRF7/?utm_source=share&utm_medium=member_desktop&rcm=ACoAAARb4_kBmnrqkDDsuuYPPXrVCKNYnevZPAo

<img src="screenshots\LinkedIn post for assignment 6.png">
