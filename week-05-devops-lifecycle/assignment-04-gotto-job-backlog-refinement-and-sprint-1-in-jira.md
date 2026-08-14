# Assignment 4 — Gotto Job: Backlog Refinement & Sprint 1 in Jira

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this 90-minute, time-boxed exercise, you will act as a Scrum team — or run in Solo Mode, playing every role yourself — to turn the Gotto Job template into a value-ordered backlog, estimate the work in story points, plan Sprint 1, open the burndown chart, and ship one small UI-only increment (text, color, spacing, a label, or a CTA — no backend changes).

---

# Task 1 — Roles & Mode Setup (Team vs Solo)

## Goal

Choose Team Mode or Solo Mode, and document how each Scrum role (Product Owner, Scrum Master, Dev Lead, DevOps Lead) was handled.

### Evidence

#### Screenshot 1 — Jira "Create project" screen, or the project sidebar after creation

![alt text](<screenshots/Screenshot_1_assig_4_1.png>)

### Notes

Write one line for each role: PO (what you prioritized), SM (how you ensured process), Dev Lead (what you built), DevOps Lead (how you shipped).

1. PO: I prioritized the stories most tied to the core conversion path — the Apply Now CTA, primary CTA color, and Remote badge — over lower-urgency polish like footer links, because they most directly help a job seeker notice and act on a listing.
2. SM: I kept the process on track by ranking the backlog by value before sprint planning, capping Sprint 1 at 4 points across 3 stories to keep scope realistic for the time-box, and using the Sprint board and burndown chart to keep progress visible rather than tracking it informally.
3. Dev Lead: I built the hero tagline update on the live index.html — changing the headline text to "Find your next role, fast." — after locating the correct file path and fixing the Nginx root misconfiguration that was blocking the change from showing.
4. DevOps Lead: I shipped it by setting up Nginx on EC2, deploying the Gotto Job source files to /var/www/gotto-job, correcting the Nginx root directive to point at the right folder, committing the change with git, and verifying it live via the public IP.

# Task 2 — Create the Jira Project (Team-managed → Scrum)

## Goal

Create a Team-managed Scrum project named `Gotto Job – Team <#>` (Team Mode) or `Gotto Job – <YourName>` (Solo Mode).

### Evidence

#### Screenshot 2 — Project created page showing the project name and key

![alt text](<screenshots/Screenshot_2_assig_4_2.png>)

# Task 3 — Create the Epic

## Goal

Create the Epic `Improve Gotto Job UI discoverability & trust` to group the UI improvement initiative.

### Evidence

#### Screenshot 3 — Backlog showing the Epic panel with the Epic visible

![alt text](<screenshots/Screenshot_3_assig_4_3.png>)

# Task 4 — Seed the Product Backlog (6–8 Stories + Fibonacci Points + Ranking)

## Goal

Create at least six Stories under the Epic, estimate each with 1, 2, or 3 story points, and rank them by value.

### Evidence

#### Screenshot 4 — Backlog showing the Epic and at least six Stories under it

![alt text](<screenshots/Screenshot_4_assig_4_4.png>)

#### Screenshot 5 — One Story opened showing its Story Points and acceptance criteria filled in

![alt text](<screenshots/Screenshot_5_assig_4_4.png>)

# Task 5 — Planning Poker (Estimate + Debate Notes)

## Goal

Confirm the Story Points (1, 2, or 3) for each Story and record brief reasoning for each estimate.

### Evidence

#### Screenshot 6 — Backlog showing Story Points visible, or two or three Stories opened showing their points

![alt text](<screenshots/Screenshot_6_assig_4_5.png>)

### Notes

For each story, explain in one or two lines why it is a 1, 2, or 3 (mention any debate, even in Solo Mode).

Hero tagline clarity — 1 pt
Single static text change with a known target string; no logic, no conditional states. Low effort, low risk.

Primary CTA color — 1 pt
One CSS/style value applied via existing button class; touches multiple pages but no logic changes.

Job card typography — 2 pts
Requires adjusting the title style within the card template and verifying it doesn't break layout across different title lengths.

Remote badge (UI-only) — 2 pts
Needs conditional logic (only show on cards flagged REMOTE) plus new markup/styling — more than a pure text/color tweak.

Posted on <date> text — 1 pt
Static text addition to the card template; no conditional logic since content is static-acceptable.

Advanced search labels — 2 pts
Touches three separate form fields and needs alignment checked across the whole form, not just one element.

Job detail Apply Now CTA — 1 pt
Single button with a link and basic focus/keyboard accessibility, contained to one page.

Footer trust links — 1 pt
Two links added to an existing footer, routing to pages that already exist — low complexity.

Debate note (Solo Mode):


As PO, I initially leaned toward scoring Remote badge as 1 pt since it looked visually simple. As Dev Lead, I flagged that it needs conditional logic to detect the REMOTE flag per card, which is more effort than a static text/color change — so we settled on 2 pts.

# Task 6 — Sprint Planning: Create Sprint 1 + Sprint Goal + Scope

## Goal

Create Sprint 1, move three or four Stories into it (approximately 3–6 points), set the Sprint Goal, and break each selected Story into Build, Verify, Deploy, and Screenshot Sub-tasks.

### Evidence

#### Screenshot 7 — Sprint 1 with the selected Stories inside it

![alt text](<screenshots/Screenshot_7_assig_4_6.png>)

#### Screenshot 8 — One Story showing the Sub-tasks created

![alt text](<screenshots/Screenshot_8_assig_4_6.png>)

# Task 7 — Reports: Open Burndown Chart

## Goal

Open the Burndown Chart and confirm it exists for Sprint 1. It is acceptable if the chart is not yet populated.

### Evidence

#### Screenshot 9 — Burndown Chart page opened, even if empty

![alt text](<screenshots/Screenshot_9_assig_4_7.png>)

# Task 8 — Ship One Small Increment (Build + Deploy + Proof)

## Goal

Implement one small UI-only Story from Sprint 1, commit it, deploy it live, and move the Story and its Sub-tasks to Done in Jira.

### Evidence

#### Screenshot 10 — Jira board showing the Story moved to Done

![alt text](<screenshots/Screenshot_10_assig_4_8.png>)

#### Screenshot 11 — Git commit output

![alt text](screenshots/Screenshot_11_ASSIG_4_8.png>)

#### Screenshot 12 — Live URL in the browser showing the UI change, with the URL visible

![alt text](screenshots/Screenshot _12_ASSIG_4_8.png>)

# Task 9 — Retro Notes (Scrum Pillar + Value)

## Goal

Add a retro comment covering what went well, what to improve, one Scrum pillar observed (Transparency, Inspection, or Adaptation), and one Scrum value (Openness, Focus, Commitment, Courage, or Respect).

### Evidence

#### Screenshot 13 — Jira retro comment visible

![alt text](screenshots/Screenshot_13_assig_4_8.png>)

# Task 10 — LinkedIn Post (Mandatory)

## Goal

Publish a LinkedIn post about what you delivered, including your live URL, three to five lines on what you did and learned, and one screenshot (Burndown Chart, Sprint board, or the live UI change).

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

https://lnkd.in/p/eCNyb9gu

#### Screenshot 14 — Published LinkedIn post

![alt text](<screenshots/LINKEDIN_week_5_assig_4.png>)

