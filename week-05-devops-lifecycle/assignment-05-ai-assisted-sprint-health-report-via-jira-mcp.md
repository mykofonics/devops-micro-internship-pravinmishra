# Assignment 5 — AI-Assisted Sprint Health Report via Jira MCP

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will connect Claude Code to your Jira board through an MCP server, the same way you connected it to GitHub in Week 2, and build a read-only `/sprint-health` skill. The skill reads your current sprint through Jira's API and reports sprint velocity, stories at risk of missing the sprint, and items missing an estimate — but it must never create, edit, comment on, or transition a single ticket itself. You will prove that boundary holds by making a real change on the board yourself and confirming the skill only ever reports, never acts.

---

# Task 1 — Create a Jira API Token

## Goal

Generate an API token from your Atlassian account that the MCP server will use to authenticate with your Jira site. Do not screenshot the token value itself.

### Evidence

#### Screenshot 1 — Jira API token creation confirmation page showing the token name, with the token value not visible

![alt text](<screenshots/Screenshot_1_assig_5_1.png>)

### Notes You Must Write (Very Important):

Why does the MCP server need your site URL and account email in addition to the token?

Site URL: usually ask the question (where to..) tells the server which Jira site to connect to (Atlassian hosts many separate sites, not one global address).
Account email — usually ask the question (who is..) the server which user the token belongs to, since Jira Cloud auth pairs email + token together.
Token — usually ask for the proof. Proves the request is actually authorized.


# Task 2 — Create .mcp.json at the Project Root

## Goal

Create or update `.mcp.json` at your project root with a Jira MCP server block, following the same shape as the GitHub MCP server you configured in Week 2.

### Evidence

#### Screenshot 2 — `.mcp.json` open in VS Code showing the Jira server configuration

![alt text](<screenshots/Screenshot_2_assig_5_2.png>)

### Notes You Must Write (Very Important):

Compare this jira block to the github block from Week 2 Assignment 5. The GitHub server ran via npx (a Node.js package); this one runs via uvx (a Python package) — what stays exactly the same shape despite that difference, and why doesn't Claude Code care which language a given MCP server is written in?

Answer:
Both blocks follow the same command / args / env shape — only the actual values differ (npx vs uvx, different package names). Claude Code doesn't care which language the server is written in because it just launches it as a subprocess and communicates over the standard MCP protocol, the same way a browser doesn't care if a website's backend is Python or Node.

# Task 3 — Add Your Credentials to settings.local.json

## Goal

Add your Jira site URL, account email, and API token to `.claude/settings.local.json`, and confirm that file is listed in `.gitignore` so it is never committed.

### Evidence

#### Screenshot 3 — `settings.local.json` open in VS Code showing the `env` section, with the actual token value blurred or covered

![alt text](<screenshots/Screenshot_3_assig_5_3.png>)

### Notes You Must Write (Very Important):

Why must JIRA_API_TOKEN live in settings.local.json and never in .mcp.json?

.mcp.json is committed and shared with the project, so anything in it becomes permanently visible in git history, a token there would leak the moment someone runs git add .. settings.local.json is gitignored and personal, which is exactly where secrets belong.

# Task 4 — Verify the Connection with /mcp

## Goal

Restart Claude Code and confirm the Jira MCP server shows as connected.

### Evidence

#### Screenshot 4 — `/mcp` output showing `jira: connected`

![alt text](<screenshots/Screenshot_4_assig_5_4.png>)

# Task 5 — Run a Live Query to Prove Real Board Data

## Goal

Ask Claude to list the issues in your current active sprint through the Jira MCP connection, and confirm the result matches what you see on your live board in the browser.

### Evidence

#### Screenshot 5 — Claude's response showing the live sprint issue list retrieved via Jira MCP

![alt text](<screenshots/Screenshot_5_assig_5_5.png>)

### Notes You Must Write (Very Important):

How did you confirm this was real board data and not something Claude guessed?

I confirmed it by comparing the report to my real Jira board — the issue keys, statuses, and points matched exactly, and after I manually changed a ticket, the next report reflected that change.

# Task 6 — Build the /sprint-health Skill

## Goal

Create a `/sprint-health` skill restricted to read-only Jira tools plus `Read`, with no issue-mutating tools and no `Write`. Run it and confirm it produces a report covering sprint velocity, at-risk stories, and items missing an estimate.

### Evidence

#### Screenshot 6 — `SKILL.md` frontmatter showing `allowed-tools` limited to read-only Jira tools plus `Read`, with `disable-model-invocation: true`

![alt text](<screenshots/Screenshot_6_assig_5_6.png>)


#### Screenshot 7 — `/sprint-health` output showing the full triage report against your real sprint

![alt text](<screenshots/Screenshot_7_assig_5_6.png>)

### Notes You Must Write (Very Important):

1. Which Jira MCP tools does this skill's allowed-tools list include, and which mutating tools (create issue, update issue, transition issue, add comment) does it deliberately exclude?

Included: jira_search, jira_get_issue, jira_get_sprint, jira_get_board, and Read — all read-only.

Excluded: any tool that creates, updates, transitions, or comments on an issue none of those appear in allowed-tools, and Write is excluded too.

2. Why does a Scrum Master need this restriction more than almost any other role in this course?

Add your answer here

The Scrum Master is accountable for the board's accuracy every ticket change needs a real person behind it. If the AI could silently edit or move tickets, that accountability breaks and no one would know what actually happened.

# Task 7 — Prove the Skill Never Mutates the Board

## Goal

Manually update one ticket on your board in the browser (for example, move a story to "Done" or add a missing estimate), then run `/sprint-health` again and confirm the new report reflects your change — proving the skill only ever reads live state and never wrote to the board itself.

### Evidence

#### Screenshot 8 — Second `/sprint-health` run showing the report now reflects your manual board change

![alt text](<screenshots/Screenshot_8_assig_5_7.png>)

### Notes You Must Write (Very Important):

Map this assignment to Gather → Analyze → Human Act → Verify from Week 3 Assignment 6. Which step did you perform manually in the browser, and why must that step stay human?

Answer:
Gather — the skill pulled sprint data via Jira MCP. 
Analyze — it calculated velocity and flagged at-risk stories. 
Human Act — I manually changed the ticket in the browser myself. 
Verify — I re-ran the skill and confirmed the report reflected my change.

Act is the step that must stay human, because it's the one that asserts something happened on the board. if the AI could do it, a wrong call would silently become the recorded truth with no one accountable for it.

