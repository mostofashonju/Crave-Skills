# Prompt Guide — CraveSkill in Claude Code, opencode, and Kilocode

Version 1.0 · Updated 2026-08-30 · Companion file to CraveSkill.md

Step-by-step instructions for giving prompts to CraveSkill in each tool — and the **why** behind every step.

---

## Table of Contents

1. [Why This Guide Exists — the For Why](#1-why-this-guide-exists--the-for-why)
2. [The Three Tools at a Glance](#2-the-three-tools-at-a-glance)
3. [One-Time Setup — Step by Step, Per Tool](#3-one-time-setup--step-by-step-per-tool)
4. [The 7-Step Prompting Session — Every Step with the Why](#4-the-7-step-prompting-session--every-step-with-the-why)
5. [Prompt Library by Mode](#5-prompt-library-by-mode)
6. [Prompting Rules — Do and Don't, with Why](#6-prompting-rules--do-and-dont-with-why)
7. [Troubleshooting — Symptom, Cause, Fix](#7-troubleshooting--symptom-cause-fix)
8. [Quick Reference Card](#8-quick-reference-card)

---

## 1. Why This Guide Exists — the For Why

CraveSkill.md is knowledge sitting on disk. An AI tool will not use that knowledge until two things happen:

| # | Requirement | How It Is Solved |
| --- | --- | --- |
| 1 | The tool must be **pointed at the file** | One-time setup (Section 3) — this repo already ships the pointer files |
| 2 | You must **prompt in the order the skill expects** | The 7-step session (Section 4) — load, context, mode, data, formulas, iterate, save |

### 1.1 What Changes When the Skill Is Loaded

| Without CraveSkill | With CraveSkill |
| --- | --- |
| Generic internet advice | A fixed 10-skill analytical protocol |
| Invented "approximate" prices | Dated, located, sourced wholesale prices |
| Different method every session | Same method every session — repeatable results |
| Walls of text | Tables, lists, and templates |
| Advice you cannot audit | Math shown step by step with assumptions labeled |

### 1.2 Why Use a Coding Agent for a Food Business At All

Claude Code, opencode, and Kilocode are agentic — they can **read files** (load the skill), **browse the web** (fetch today's market prices), **calculate** (costing, statistics, break-even), and **write files** (save your reports). A chat window can only talk. An agent builds you a business folder that compounds week after week.

### 1.3 The One-Line Principle

> Load the skill → set the market context → pick one mode → feed real data → name the formulas → iterate → save to files.

Every step below is one link in that chain. Skip a link and the answer quality drops predictably — the Why column of each step tells you exactly which link you skipped.

---

## 2. The Three Tools at a Glance

| Tool | What It Is | Runs Where | How CraveSkill Loads in This Repo | Strongest For |
| --- | --- | --- | --- | --- |
| Claude Code | Anthropic's agentic coding tool | Terminal (macOS, Windows, Linux) | Skill folder .claude/skills/craveskill/SKILL.md plus pointer in CLAUDE.md — invoke with /craveskill | Web search for live wholesale prices; polished report files |
| opencode | Open-source, model-agnostic terminal agent | Terminal | AGENTS.md at repo root (auto-read); also discovers Claude-style skill folders | Your choice of model, including free and local providers |
| Kilocode (Kilo Code) | VS Code extension agent (Cline / Roo Code family) | VS Code sidebar | AGENTS.md at workspace root (auto-read); optional .kilocode/rules/ folder | Point-and-click workflow; @-mention files; no terminal needed |

### 2.1 Why They Load It Differently

Each tool has its own memory convention:

| Tool | Memory Convention | File This Repo Ships |
| --- | --- | --- |
| Claude Code | Looks for .claude/ folders and a CLAUDE.md memory file | .claude/skills/craveskill/SKILL.md + CLAUDE.md |
| opencode | Reads AGENTS.md at the project root (and Claude-compatible paths) | AGENTS.md |
| Kilocode | Reads AGENTS.md and .kilocode/rules/ from the workspace root | AGENTS.md |

Because all three pointer files ship in this repository, **the same clone works in all three tools** — pick whichever you like, the skill loads the same way.

### 2.2 Which Tool Should You Pick?

| If you… | Pick |
| --- | --- |
| Live in the terminal and want live web price checks | Claude Code |
| Want open-source freedom and any model, free or local | opencode |
| Prefer clicking in VS Code over typing in a terminal | Kilocode |

---

## 3. One-Time Setup — Step by Step, Per Tool

Setup happens once per machine. After this, every session starts with the skill already available.

### 3.1 Claude Code

| Step | Action | Why |
| --- | --- | --- |
| 1 | Install Claude Code and sign in with your Anthropic account | Nothing runs before authentication |
| 2 | Open a terminal **inside the Crave-Skills folder** | Skills and CLAUDE.md are discovered from the directory you launch from — launching elsewhere makes the skill invisible |
| 3 | Type claude and press Enter | Starts a session with the repo as the working directory, so skill discovery runs |
| 4 | Type /skills and check that craveskill appears in the list | Confirms the skill folder and its frontmatter are valid and discovered |
| 5 | Optionally type /craveskill any time | Manual invocation guarantees the skill fires even when auto-detection does not recognize the task |

### 3.2 opencode

| Step | Action | Why |
| --- | --- | --- |
| 1 | Install opencode and run opencode auth login, then choose your model provider | opencode is model-agnostic — it needs to know which model to talk to |
| 2 | Open a terminal inside the Crave-Skills folder | AGENTS.md is discovered from the working directory upward — running from your home folder misses it |
| 3 | Type opencode and press Enter | Starts the session with the repo loaded, AGENTS.md rules active |
| 4 | Ask: which rules files are active in this session? | Verifies AGENTS.md was picked up before you trust any answer |
| 5 | Optional alternative: copy the folder .claude/skills/craveskill into .opencode/skills/ | opencode also discovers Claude-style skill paths — useful if you want the skill isolated from repo rules |

### 3.3 Kilocode (Kilo Code in VS Code)

| Step | Action | Why |
| --- | --- | --- |
| 1 | Install the Kilo Code extension from the VS Code marketplace and sign in | The agent lives inside VS Code, not in a terminal |
| 2 | In VS Code: File → Open Folder → select the Crave-Skills folder | **The classic trap:** opening a single .md file gives the agent no workspace root, so AGENTS.md is never discovered. It must be a folder |
| 3 | Open the Kilo Code panel from the sidebar and pick your model | Same reason as opencode — the agent needs a model assigned |
| 4 | Check Settings → Context → Agent Rules is enabled | Rule loading is a toggle; if it is off, the agent works blind to your instructions |
| 5 | Optional for older versions: place a copy of CraveSkill.md inside .kilocode/rules/ | Older Kilo builds auto-load every markdown file from that rules folder |

### 3.4 What This Repo Already Ships

| File | Read By | Purpose |
| --- | --- | --- |
| CraveSkill.md | All three tools (when pointed to it) | The master skill — 19 sections, 10 analytical skills, 15 templates |
| .claude/skills/craveskill/SKILL.md | Claude Code, opencode | Auto-triggering skill wrapper with frontmatter |
| CLAUDE.md | Claude Code | Always-on pointer — the skill is mentioned in every session |
| AGENTS.md | opencode, Kilocode | Always-on pointer for both tools |
| prompt.md | You | This guide |

If you did setup right, you can skip the wake-up prompt in Step 1 below and go straight to your mode — but running it once anyway is the cheapest possible quality insurance.

---

## 4. The 7-Step Prompting Session — Every Step with the Why

This is the core of the guide. Follow these seven steps **in order**, in any of the three tools. Each step shows: what to type, why it works, and what you should see back.

### Step 1 — Wake the Skill

**Type this:**

> Read CraveSkill.md at the repository root and operate as CraveSkill for this whole session. Confirm the skill is loaded, then show me the Quick Start mode menu from Section 2.

| Why | What You Should See Back |
| --- | --- |
| Agents answer only from what is in their context window. Setup files point the agent at the skill, but saying it out loud guarantees all 19 sections are actually read before the first answer. Without this step the agent may answer from general training and merely "sound like" the skill | The mode menu A through I, plus the interactive entry checklist |

### Step 2 — Set the Market Context

**Type this:**

> My business: [cloud kitchen] in [Dhaka], [Bangladesh]. Currency: [BDT]. I buy from [Karwan Bazar and Town Hall Market]. Today: [date]. Latest supplier prices: [paste your price list or bills here].

| Why | What You Should See Back |
| --- | --- |
| Guardrails 1 and 2 of the skill: no costing starts without country, city, and currency — and never a guessed price. Your own supplier bills are trust level 1 in the price sourcing ladder (skill Section 4.2). Anything you do not provide becomes a labeled assumption, never a silent guess | A small confirmed-assumptions table repeating your facts back — this is skill Section 3, step 3 of the session flow |

### Step 3 — Pick One Mode

**Type this:**

> Mode B — cost and price my menu.

| Why | What You Should See Back |
| --- | --- |
| Each mode routes through specific skill modules and output templates. One mode per turn produces a deep, structured answer. Stacking five requests into one prompt produces five shallow ones — the skill's own conversation rule is a maximum of 3 to 4 questions per turn in both directions | At most 3 to 4 short intake questions, matched to your mode |

### Step 4 — Feed Real Data

**Type this:**

> Here is my menu with portion sizes: [paste]. Here are the last 4 weeks of item sales: [paste]. Platform commissions: Foodpanda 30%, foodi 25%, khaodao 25%.

| Why | What You Should See Back |
| --- | --- |
| Menu engineering needs units sold plus margins; unit economics needs your actual commission; break-even needs your fixed costs. Every number you withhold is a guess that compounds through every formula downstream | Your data echoed back in the right template tables (T2, T3, T4), ready for analysis |

### Step 5 — Name the Formulas You Want Used

**Type this:**

> Cost each item using my dated prices, show food cost percentage, flag anything outside my 30% target, and compute platform menu prices with the unit economics equation from Section 5.5.

| Why | What You Should See Back |
| --- | --- |
| Naming the exact section or formula forces the agent to use CraveSkill's math and templates instead of improvising its own method. This is the single biggest quality lever in prompting — vague requests get generic math, named requests get the skill's math | Costing sheets with food cost percentages, flags on out-of-band items, and unit economics tables per platform |

### Step 6 — Challenge and Iterate

**Type this:**

> Beef is up 15% since my last costing. Re-run Mode B, then apply the least cost combination strategy from Section 9.1 to my three costliest ingredients and show me the weekly saving.

| Why | What You Should See Back |
| --- | --- |
| The first answer is the baseline, not the verdict. Sections 9.1 and 9.2 of the skill exist precisely for the second pass — least cost combination and profit maximization are where the actual money is found. Iteration is where a good answer becomes a profitable one | A mix-comparison table: current practice versus least cost combination, with quality constraints checked and savings quantified |

### Step 7 — Save the Outputs to Files

**Type this:**

> Save the updated costing sheet, shopping list, and KPI dashboard as three markdown files with today's date, in a reports folder.

| Why | What You Should See Back |
| --- | --- |
| Chat scrolls away; files persist. Saved reports become next week's baseline and your price-watch history — this is the whole reason to use an agentic tool instead of a chat window | The files created, plus a one-line summary of what is where |

### 4.1 The Weekly Ritual — Bookmark This

**Type this every week:**

> New week. Here are this week's [market name] prices: [paste]. Update my price watch sheet, flag any spike over 5%, re-cost the affected items, and regenerate the weekly shopping list for [forecast] orders per day.

| Why |
| --- |
| Wholesale prices move weekly — especially chicken, oil, onions, and rice. A skill that runs on last month's prices is worse than no skill. One weekly prompt keeps every downstream number honest |

### 4.2 The Monthly Ritual

**Type this every month:**

> Run menu engineering on the last 4 weeks of sales, give me one action per item, refresh break-even, and check my KPI dashboard against targets.

| Why |
| --- |
| Menu engineering is a loop, not an event (skill Section 8.2). Items drift between Stars, Plowhorses, Puzzles, and Dogs as prices and tastes move — a monthly matrix catches the drift before it eats the margin |

---

## 5. Prompt Library by Mode

Copy, paste, and fill the square brackets. These map one-to-one to the mode menu in CraveSkill.md Section 2.

| Mode | Ready-to-Paste Prompt |
| --- | --- |
| A — Chef and Recipe | Mode A: give me kacchi biryani for 60 portions, advanced level, with batch scaling, ratios, critical control points, and the ingredient shopping list |
| B — Costing and Pricing | Mode B: cost and price my menu with today's [market] prices — food cost percentage per item, flags outside [30]% target, and platform prices at [commission]% commission |
| C — Menu Design | Mode C: run menu engineering on my item mix and redesign my menu layout using the Section 8 techniques |
| D — Delivery Platforms | Mode D: compute unit economics per order on [Foodpanda] at [30]% commission and [10]% discount — then verdict: keep, fix, or exit? |
| E — Business Setup | Mode E: I want to open a [25-seat café] in [city] — give me the Stage 1 checklist and the full launch budget |
| F — Shopping Lists | Mode F: generate weekly and monthly shopping lists for [100] orders per day at this mix: [paste item mix] |
| G — Inventory and Waste | Mode G: set par levels and reorder points for my top 15 ingredients and design my count cadence |
| H — Profit and Statistics | Mode H: profit maximization plan — contribution per bottleneck minute, least cost combination on my top costs, and a price elasticity test plan |
| I — Full Audit | Mode I: full business audit — run all ten skills on my data and give me a prioritized roadmap |

---

## 6. Prompting Rules — Do and Don't, with Why

| Rule | Why |
| --- | --- |
| ✅ Do — give city, market, currency, and date in your first message | Guardrails 1 and 2: nothing computes without location and currency |
| ✅ Do — paste your own supplier bills whenever possible | Trust level 1 in the price sourcing ladder — it kills invented prices at the source |
| ✅ Do — pick one mode per turn | Depth beats breadth; the skill's protocol is designed for one routed question at a time |
| ✅ Do — name the section or formula you want used | Forces the skill's math and templates instead of improvised methods |
| ✅ Do — ask for tables and specific template codes (T2, T3, T4…) | The skill's output style is tables — asking for it keeps answers compact and comparable |
| ✅ Do — ask it to label every assumption | Honest numbers you can replace later beat confident numbers you cannot trust |
| ❌ Don't — ask ten questions in one prompt | Answers go shallow and the agent drops half your context — split into turns |
| ❌ Don't — accept an undated price | A price without a date and a market is a violation of guardrail 1 — ask again |
| ❌ Don't — let it cut quality silently to cut cost | Quality is a hard constraint (guardrail 5): every portion or ingredient change must be stated openly and re-priced |
| ❌ Don't — paste passwords, API keys, or customer data into prompts | Basic hygiene: prompts may be stored by model providers — business numbers are fine, secrets are not |

---

## 7. Troubleshooting — Symptom, Cause, Fix

| Symptom | Likely Cause | Fix |
| --- | --- | --- |
| Answer is generic text with no tables | Skill never actually loaded | Send the Step 1 wake-up prompt; in Claude Code run /skills to verify craveskill is listed |
| /skills lists nothing | Session launched from the wrong folder, or SKILL.md is missing | Launch from the repo root; check .claude/skills/craveskill/SKILL.md exists |
| Prices look invented or suspiciously round | Agent skipped the guardrails | Reply quoting skill Section 17 rule 1 — every price must be dated, located, and sourced — then paste your real bills |
| Wall of text instead of tables | Output style rule forgotten mid-session | Reply: redo that answer as tables per the skill's style rules |
| opencode ignores AGENTS.md | Session was started outside the repo | Close, cd into the Crave-Skills folder, restart opencode |
| Kilocode ignores the instructions | You opened a single file instead of the folder | File → Open Folder → select the repo; confirm Settings → Context → Agent Rules is enabled |
| Agent forgets the skill mid-conversation | Long session trimmed the skill out of context | Send: re-read CraveSkill.md and continue from Section [number] |
| Reports never get saved | The agent was never asked, or lacks write access to where you are | Ask it to save under a reports folder inside the repo |
| Same prompt gives different quality each week | No wake-up prompt and no saved baseline files | Use the Step 1 wake prompt plus the weekly ritual — consistency comes from the ritual, not luck |

---

## 8. Quick Reference Card

The whole guide in eight lines:

1. **Open the repo, never a lone file** — folder context is how all three tools find the skill
2. **Wake it** — read CraveSkill.md and show me the mode menu
3. **Context first** — city + market + currency + date + real prices
4. **One mode per turn** — A through I
5. **Name the formula** — quote the section number you want used
6. **Dated prices only** — or clearly labeled assumptions, nothing in between
7. **Iterate** — least cost combination and profit maximization on the second pass
8. **Save to files** — chat is not a filing cabinet

### Reference Notes

| Topic | Where to Verify |
| --- | --- |
| Claude Code skills format and discovery | code.claude.com docs — Extend agents with skills |
| opencode rules and AGENTS.md | opencode.ai/docs/rules |
| Kilocode custom rules and configuration | kilo.ai/docs — Customize → Custom Rules |

---

*Next step: open your tool of choice in this repo, run the Step 1 wake-up prompt, and start with Mode B — your menu, your market, your prices.*
