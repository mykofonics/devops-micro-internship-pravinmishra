# Assignment 7 — AI-Assisted Azure Security Posture Audit

<<<<<<< HEAD
Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI
=======
Part of the DevOps Micro Internship (DMI) with Agentic AI
>>>>>>> upstream/main

---

## Purpose

<<<<<<< HEAD
In this assignment, you will build a read-only Bash script that audits the Azure resources you deployed earlier this week — a virtual machine, a three-tier network with a Load Balancer, a Storage Account, and an Azure Database for MySQL server — for common security misconfigurations. You will connect that script to Claude Code as a reusable `/azure-audit` skill that explains findings and recommends a fix without ever running it, then fix one real finding yourself and prove the fix with a second audit run. This is the same read-only-evidence-then-human-fixes discipline from Week 3, now applied to Azure with the `az` CLI instead of Linux commands — and the cloud-agnostic counterpart to the AWS audit you built in Week 6.

---

# Task 1 — Confirm Your Resources and Create the Workspace

## Goal

Confirm your Azure CLI is authenticated and can see the VM, network, storage account, and MySQL server you built this week, then set up a workspace folder for the audit.

### Evidence

#### Screenshot 1 — `az account show` and `az vm list -d -o table` confirming your subscription and running VM (subscription ID partially blurred)
=======
Build a read-only Bash script that audits Azure resources for common security misconfigurations. Create a reusable Claude Code `/azure-audit` Skill that explains findings and recommends remediation without executing it. Fix one finding yourself and rerun the audit to verify the result.

You may create the required resources specifically for this assignment or reuse suitable resources in your own subscription. A Load Balancer and a deployed application are not required.

---

# Task 1 — Confirm Your Azure Resources and Create the Workspace

## Goal

Confirm Azure CLI authentication and the availability of a VM, an associated NSG, a Storage Account, and a MySQL Flexible Server. Create the workspace with `scripts`, `reports`, and `.claude/skills/azure-audit` directories.

## Evidence

#### Screenshot 1 — Azure CLI showing the subscription name, VM, Storage Account, and MySQL Flexible Server without exposing subscription or tenant IDs
>>>>>>> upstream/main

Add your screenshot here.

---

<<<<<<< HEAD
=======
#### Screenshot 2 — Workspace location and directory structure shown using `pwd` and `find . -maxdepth 4 -type d | sort`

Add your screenshot here.

---

## Notes You Must Write

1. Which Azure resources will be inspected by this audit, and why is each one required?

Write your answer here.

2. Why should you confirm that the resources exist before writing an audit script against them?

Write your answer here.

---

>>>>>>> upstream/main
# Task 2 — Create Project Context and Safety Rules in CLAUDE.md

## Goal

<<<<<<< HEAD
Create a `CLAUDE.md` for this workspace that tells Claude what the audit covers and the safety rules it must follow: never run a mutating `az` command, never claim a finding without report evidence, and always let the human review and run any remediation.

### Evidence

#### Screenshot 2 — `CLAUDE.md` open in your editor showing the project overview, audit workflow, and safety rules
=======
Create `CLAUDE.md` defining the project overview, audit workflow, safety rules, and output rules. Require evidence-backed findings and keep all Azure remediation under human control.

## Evidence

#### Screenshot 3 — `CLAUDE.md` showing the Project Overview, Audit Workflow, Safety Rules, and Output Rules sections
>>>>>>> upstream/main

Add your screenshot here.

---

<<<<<<< HEAD
=======
## Notes You Must Write

1. Why should Claude never be allowed to execute the remediation command itself?

Write your answer here.

2. Which rule prevents Claude from reporting a security problem without evidence?

Write your answer here.

---

>>>>>>> upstream/main
# Task 3 — Use Agentic AI to Plan the Audit Before Writing the Script

## Goal

<<<<<<< HEAD
Ask Claude Code to read `CLAUDE.md` and propose a read-only, four-check audit plan (NSG rules open to `0.0.0.0/0` on port 22 or 3389, storage account public blob access, VM disk encryption status, and Azure Database for MySQL public network access) — without creating or editing any file yet.

### Evidence

#### Screenshot 3 — Claude Code showing the four-check plan, with no files created or modified
=======
Ask Claude Code to read `CLAUDE.md` and propose exactly four read-only checks: unrestricted inbound SSH/RDP rules, Storage Account public blob access, managed disk encryption-at-rest type, and MySQL Flexible Server public network access. Do not allow file creation or modification during planning.

## Evidence

#### Screenshot 4 — Claude Code showing the four-check audit plan, including evidence-gathering commands, healthy and risky results, and why each check matters
>>>>>>> upstream/main

Add your screenshot here.

---

<<<<<<< HEAD
=======
## Notes You Must Write

1. Which part of the Agentic Loop is being designed in this task?

Write your answer here.

2. Why is it useful to identify the exact evidence-gathering commands before writing the Bash script?

Write your answer here.

---

>>>>>>> upstream/main
# Task 4 — Build the Azure Audit Bash Script

## Goal

<<<<<<< HEAD
Write a Bash script that runs the four checks from Task 3 using read-only `az` commands, writes a PASS/WARN/FAIL report with your Full Name, and exits with a different code for a healthy, warning, or failing result. Validate it with `bash -n` and make it executable.

### Evidence

#### Screenshot 4 — Your script open in your editor, showing the check functions and the `az` commands they call
=======
Create `scripts/azure-audit.sh` using read-only Azure CLI commands. Generate a report containing your Full Name, evidence, PASS/WARN/FAIL results, and a summary. Use exit codes **0 for HEALTHY**, **1 for WARN**, and **2 for FAIL**. Validate the script and make it executable.

## Evidence

#### Screenshot 5 — Top of `azure-audit.sh` showing the variables and checks array
>>>>>>> upstream/main

Add your screenshot here.

---

<<<<<<< HEAD
#### Screenshot 5 — Output of `bash -n` (no syntax errors) and `ls -l` showing the script is executable
=======
#### Screenshot 6 — NSG and Storage Account check functions
>>>>>>> upstream/main

Add your screenshot here.

---

<<<<<<< HEAD
# Task 5 — Run the Script and Review the Baseline Report

## Goal

Run the script against your live resources and read the report honestly, even if it shows a real finding — do not fix anything yet.

### Evidence

#### Screenshot 6 — Script output showing your Full Name and all four checks with a PASS, WARN, or FAIL result
=======
#### Screenshot 7 — Managed disk encryption and MySQL check functions

Add your screenshot here.

---

#### Screenshot 8 — `print_summary` function and script exit behavior

Add your screenshot here.

---

#### Screenshot 9 — Successful `bash -n` validation and `ls -l` output showing executable permission

Add your screenshot here.

---

## Notes You Must Write

1. What is stored inside the `checks` array?

Write your answer here.

2. How does the `for` loop execute those checks?

Write your answer here.

3. Why does the NSG check inspect both single-value and multi-value address/port fields?

Write your answer here.

4. Why does the script use different exit codes for HEALTHY, WARN, and FAIL?

Write your answer here.

5. What does the disk encryption check verify?

Write your answer here.

---

# Task 5 — Run the Baseline Audit

## Goal

Run the script, capture its exit code immediately, review all four results, and save `reports/baseline-report.txt` before making any remediation.

## Evidence

#### Screenshot 10 — Baseline audit output showing your Full Name and all four check results
>>>>>>> upstream/main

Add your screenshot here.

---

<<<<<<< HEAD
=======
#### Screenshot 11 — Captured exit code and final report summary

Add your screenshot here.

---

## Notes You Must Write

1. What is the Overall Status of your baseline audit?

Write your answer here.

2. Did any check return WARN or FAIL?

Write your answer here.

3. What evidence supports each finding?

Write your answer here.

4. Which finding represents the highest security risk in your environment? If none were found, state that.

Write your answer here.

---

>>>>>>> upstream/main
# Task 6 — Create and Run the /azure-audit Skill

## Goal

<<<<<<< HEAD
Create a Claude Code skill restricted to read-only tools (no `Write`) that runs your script, reads the report, and explains every finding with the risk of leaving it unresolved — without ever running a remediation command itself.

### Evidence

#### Screenshot 7 — Your skill file's frontmatter showing `allowed-tools` without `Write`
=======
Create `.claude/skills/azure-audit/SKILL.md` with Bash, Read, and Grep permissions, without Write permission, and with manual invocation enabled. The Skill must run the audit, read the report, explain findings and their impact, and recommend remediation and verification commands without changing Azure resources.

## Evidence

#### Screenshot 12 — `SKILL.md` showing frontmatter, tool restrictions, and safety rules
>>>>>>> upstream/main

Add your screenshot here.

---

<<<<<<< HEAD
#### Screenshot 8 — `/azure-audit` output showing the baseline findings and Claude's explanation
=======
#### Screenshot 13 — `/azure-audit` output showing baseline findings, supporting evidence, risk explanations, recommended remediation, and verification commands
>>>>>>> upstream/main

Add your screenshot here.

---

<<<<<<< HEAD
# Task 7 — Fix a Real Finding and Re-Verify

## Goal

Pick one WARN or FAIL finding (or deliberately open an NSG rule to port 22 from `0.0.0.0/0` if your baseline was already clean), save that failing report, run the remediation command yourself — scoped to your own IP, not left open — and confirm the second audit run shows it resolved.

### Evidence

#### Screenshot 9 — Saved report showing the original finding before the fix
=======
## Notes You Must Write

1. Why does the Skill include Bash, Read, and Grep, but not Write?

Write your answer here.

2. What part of the workflow is performed by Bash?

Write your answer here.

3. What part is performed by Claude?

Write your answer here.

4. What additional value does Claude add beyond the script’s PASS/WARN/FAIL result?

Write your answer here.

---

# Task 7 — Fix a Real Finding and Reverify

## Goal

Save the before-fix report, review a recommended remediation, execute the fix yourself, and rerun `/azure-audit` to confirm that the finding is resolved. Save the after-fix report.

If the baseline is clean, use only the controlled temporary SSH-rule exercise permitted in the assignment guidelines. Do not deliberately expose the database or Storage Account.

## Evidence

#### Screenshot 14 — `before-fix-report.txt` showing the original finding
>>>>>>> upstream/main

Add your screenshot here.

---

<<<<<<< HEAD
#### Screenshot 10 — Terminal output of the remediation command you ran yourself
=======
#### Screenshot 15 — Terminal showing the remediation command executed manually by you
>>>>>>> upstream/main

Add your screenshot here.

---

<<<<<<< HEAD
#### Screenshot 11 — Second `/azure-audit` run (or report) showing the finding resolved
=======
#### Screenshot 16 — `/azure-audit` output or `after-fix-report.txt` showing the finding resolved
>>>>>>> upstream/main

Add your screenshot here.

---

<<<<<<< HEAD
### Notes

Compare this assignment to the AWS audit you built in Week 6: which finding categories map to each other across the two clouds, and what stayed exactly the same about the workflow even though the `az`/`aws` commands are completely different?

Add your answer here
=======
## Notes You Must Write

1. Which exact finding did you fix?

Write your answer here.

2. What evidence proved that it existed?

Write your answer here.

3. What command did you run?

Write your answer here.

4. Why did you choose that remediation?

Write your answer here.

5. Did Claude execute the command, or did you?

Write your answer here.

6. Why does keeping remediation under human control matter?

Write your answer here.

7. Map your actions to **Gather → Analyze → Human Act → Verify**.

Write your answer here.

---

# LinkedIn Post — Required

## Goal

Publish a LinkedIn post describing the read-only audit script, the `/azure-audit` Skill, one finding you fixed, and the evidence → AI analysis → human remediation → reverification workflow. Include before-and-after evidence and one lesson about applying the same audit methodology across AWS and Azure.

Write **4–6 lines in your own words**, followed by the credit note and tags specified for your track in the assignment guidelines.

Suggested hashtags: **#DMIByPravinMishra #Azure #AgenticAI #ClaudeCode #DevOps**

## Evidence

#### LinkedIn Post URL

Paste your published LinkedIn post URL here:

`Add your URL here`

---

#### Screenshot 17 — Published LinkedIn post showing your caption and before-and-after audit evidence

Add your screenshot here.

---

# Assignment Files

## Evidence

#### GitHub Repository or Assignment Folder URL

Paste the link containing these files:

- `CLAUDE.md`
- `scripts/azure-audit.sh`
- `.claude/skills/azure-audit/SKILL.md`
- `reports/baseline-report.txt`
- `reports/before-fix-report.txt`
- `reports/after-fix-report.txt`

`Add your repository or folder URL here`
>>>>>>> upstream/main

---

# Submission Instructions

<<<<<<< HEAD
Complete all tasks in sequence.

Your submission must include:
- All 11 required screenshots
- Do not expose your Azure subscription ID, tenant ID, client secrets, or connection strings
=======
- Include your Full Name and Screenshots **1–17** under the corresponding evidence headings.
- Answer every **Notes You Must Write** question.
- Include the required source files and saved reports through your GitHub repository/folder link.
- Include your published LinkedIn post URL.
- Ensure required outputs show your Full Name.
- Use multiple captures under an evidence heading where needed for readability.
- Do not expose subscription IDs, tenant IDs, client secrets, passwords, tokens, connection strings, private keys, or other credentials.
- After saving all evidence, remove temporary resources created specifically for this assignment as directed in the guidelines.
- Submit your work using the method specified in the assignment guidelines.
>>>>>>> upstream/main

---

# Completion Checklist

<<<<<<< HEAD
- [ ] Task 1: Azure resources confirmed and workspace created (Screenshot 1)
- [ ] Task 2: `CLAUDE.md` created with project context and safety rules (Screenshot 2)
- [ ] Task 3: Claude produced a read-only four-check plan before any script existed (Screenshot 3)
- [ ] Task 4: Audit script built, syntax-checked, and executable (Screenshots 4–5)
- [ ] Task 5: Baseline audit run and reviewed honestly (Screenshot 6)
- [ ] Task 6: `/azure-audit` skill created with no `Write` permission and run successfully (Screenshots 7–8)
- [ ] Task 7: A real finding fixed by you (not Claude) and re-verified as resolved (Screenshots 9–11)
- [ ] Notes comparing this to the Week 6 AWS audit completed
- [ ] No subscription IDs, tenant IDs, or credentials exposed
=======
- [ ] Task 1: Required resources confirmed and workspace created (Screenshots 1–2)
- [ ] Task 2: `CLAUDE.md` contains project context, workflow, safety rules, and output rules (Screenshot 3)
- [ ] Task 3: Four-check read-only plan completed before scripting (Screenshot 4)
- [ ] Task 4: Script created, syntax-checked, and executable (Screenshots 5–9)
- [ ] Task 5: Baseline report saved and exit code verified (Screenshots 10–11)
- [ ] Task 6: `/azure-audit` Skill created and run without executing remediation (Screenshots 12–13)
- [ ] Task 7: Finding documented, fixed manually, and verified as resolved (Screenshots 14–16)
- [ ] Baseline, before-fix, and after-fix reports saved
- [ ] All required written answers completed in my own words
- [ ] Required files and GitHub repository/folder URL included
- [ ] LinkedIn post published with the applicable credit note and tags (Screenshot 17)
- [ ] LinkedIn post URL included
- [ ] Full Name visible in required outputs
- [ ] No sensitive information exposed
>>>>>>> upstream/main

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## 📌 Resources

- 🌐 DMI Official Website: https://dmi.pravinmishra.com?utm_source=github&utm_medium=readme  
- 🎓 University: https://university.pravinmishra.com?utm_source=github&utm_medium=readme  
- 💬 Discord Community: https://discord.pravinmishra.com?utm_source=github&utm_medium=readme  
- 📝 Blog: https://dmi.pravinmishra.com/blog?utm_source=github&utm_medium=readme  
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

<<<<<<< HEAD
*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*
=======
*This submission is part of DevOps Micro Internship (DMI) — Agentic AI Track.*
>>>>>>> upstream/main
