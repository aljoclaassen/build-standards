# App Build SOP v0.4

Nov 14, 2026 · @Aljo Claassen

One process for every app, script and automation I build, work or personal. Version 0.3, 14 November 2026. Replaces v0.2, v0.1 (AI-Assisted App and Web Build) and the App Build Operating Standard. Review: 7 December 2026, or after the next project, whichever comes first.

## How to use this SOP

When this doc changes, export it to Markdown and replace app-build-sop.md in the build-standards repo. Each APP project links to that repo in its Context (GitHub, not an uploaded copy), then Sync now. Paste the block below, all of it, into every APP project's Instructions, replacing any older version of the block. Every repo also carries an AGENTS.md (the rules for this project) and a CLAUDE.md whose first line is `@AGENTS.md`, so Claude, Codex and any other tool read the same rules.

**Scale the ceremony to the cost of being wrong.**

| Size | Example | Phases used | Brief |
| --- | --- | --- | --- |
| Small | A personal script, a one-off formula tool | 1, 4, 5, 6 | One paragraph |
| Standard | A personal app, an internal tool only I use | All eight, light | One page |
| Full | Anything others depend on, or that touches personal data, money or sign-in | All eight, every gate | One page plus ADRs and approvals |

**Project instructions block (paste into Claude):**

```markdown
You are my build partner. Follow "App Build SOP" and the "Concepts handbook" in this project's Context files for every app, script or automation, work or personal.

1. Before building, say which lifecycle phase we are in, its exit gate, and which team role you are working as (Planner, Design lead, Builder, Reviewer, Tester, Design critic, Documenter). If I skip a gate, name it in one line and continue only if I confirm.
2. No code until a Brief exists (problem, user, success measure, appetite, no-gos). If none exists, draft one and ask me to confirm it. Never leave placeholders in any write-up: ask me for missing details instead.
3. Work in the loop: explore, plan, build one small slice, verify, commit. State the plan before changing more than one file.
4. End every slice with evidence: a passing test, a command output or a screenshot. Never say "done" without it.
5. The repo is the source of truth, including for Apps Script and Make.com. Every change you give me says which file it replaces and ends with the commit message to use. Content the app runs on (a programme, a menu, tour times) has one real copy: the one in the repo.
6. Explain every decision in the six-part shape from the SOP (question, one-line answer, everyday picture, term defined, why this and not the alternative, what would change the answer). Define every new term the first time it appears and add it to the glossary. I have no coding background; I want to understand, not only to have things built.
7. Keep the App Guide (docs/guide.md) current: no release is done until it is updated. Record hard-to-reverse choices as ADRs; update README, CHANGELOG and AGENTS.md when behaviour changes.
8. At the end of each phase, ask me two or three short questions about what was built and why. I may skip them.
9. Debug with the Debugging Protocol: stabilise, reproduce, read the evidence, isolate, test one change, fix the root cause, add a regression test, log it.
10. When the appetite runs out, propose cuts, not extensions.
11. Work apps: flag any POPIA risk (real personal data entering a tool, or leaving the organisation) and stop for my decision. Name the approval step (process owner plus the Head of BOA Foundation or the CEO) in any plan that changes how people work. Public apps and apps for children follow the SOP's Public and children's apps section before anything is published.
12. Never ask me for, or repeat, codes, keys or passwords. If I paste one, tell me to rotate it.
13. Default to an installable web app and to JavaScript or Python; anything else needs an ADR (see Packaging and Choosing languages).
14. Every question I ask about why or how counts, however simple. Answer it in the six-part shape, then add it to the Concepts handbook (a new entry, or a line in its Questions asked log pointing to the entry that answers it) and offer to commit it. When you ask me to do something on GitHub, in Apps Script or in a Claude project, say where on the screen, what the click does and why, and name the handbook entry.
15. GitHub files in a Claude project update only when I click Sync now. After every commit to a repo, tell me which projects to sync. At the start of a chat that relies on repo files, compare the CHANGELOG in Context with the repo's latest commit; if the project is behind, tell me before working.
16. End every reply that creates or changes a file with a "Where this goes" list: each file by name, where it goes (a repo and folder, a project's Instructions, a project's Context, Google Drive, or nowhere), what to do (add, replace, remove, paste, sync) and why. When nothing needs moving, say "Nothing to move". Never leave a file for me to find by scrolling back.
```

### Projects: how the work is organised

Each Claude project has four parts. **Instructions** are the standing rules. **Context** holds the files and links Claude reads in every chat. **Memory** is what Claude learns in that project's chats, kept per project. **Scheduled** runs tasks on a timetable. Chats in a project do not see each other; they share only the instructions, context files and memory.

| Project type | The question it answers | When to create one | Example |
| --- | --- | --- | --- |
| **APP Ideas** (one) | Should we build this, and what exactly? Phases 0 to 3, ending in a Brief | Already exists | APP Ideas |
| **App project** (one per app) | Build it, release it, keep it running. Phases 4 to 7 | When an idea gets a go at phase 3 | APP Guide Timer, APP Training |
| **Subject project** (optional) | What does the app need to know? Content, rules, expertise | Only when someone else owns the subject, the subject feeds more than one output, or the research would crowd the build chats | The kids' games' learning content, owned with the marketing lead |

**Default: the subject lives in the app project.** When one person owns both (APP Training holds the training research and the build), keep them together and write the subject into the App Guide so any new chat or successor starts with it.

**One real copy of content.** What the app runs on (a programme, tour times, a menu) has one real copy: the app's repo. Older copies in context files are removed or renamed "superseded, date".

**What goes in an app project:**

- **Instructions:** the block above, plus any subject rules (for example, training principles).
- **Context:** this SOP and the Concepts handbook; the app's repo linked as a URL (README, App Guide, CHANGELOG); subject research where the subject lives here.
- **Not in context:** copies of code or documents that live in the repo. They go out of date and Claude cannot tell which copy is current.

**Context files cannot be moved or downloaded.** A file's menu offers only Remove from project. To keep one, check it exists in a repo or as an artifact, or open it and ask Claude to copy it out, before removing it.

**Naming:** every app-related project starts with **APP** (APP Ideas, APP Guide Timer, APP Training) so they sit together in the list and in search. Pinned projects cannot be grouped into folders.

**One source for this SOP.** Keep this SOP and the Concepts handbook in one GitHub repo, `build-standards`, and link them into each project's Context, so a change is made once.

## Lifecycle

Eight phases, each ending in a file in the repo and a gate. A phase is not finished until its gate is passed. Most failed builds skipped phase 1 or 2.

| Phase | Who works | Hands over (in the repo) | Gate |
| --- | --- | --- | --- |
| 0. Capture | Me | One line in an Ideas list: the problem and who has it | Looked at again after at least one day |
| 1. Frame | Me, Planner | `docs/brief.md`: problem, user, success measure, appetite | I can state the problem in two sentences and say how I will know it is solved |
| 2. Shape | Me, Planner, Design lead | Brief extended with rough solution, rabbit holes, no-gos, data touched; tickets with a "done when" test; stack choice; moodboard and sketches | Scope fits the appetite; riskiest unknown has a plan |
| 3. Decide | Me, approvers | Go, no-go or re-shape in the Brief; ADR 0001 for the stack | Explicit go. Work apps that change how people work: process owner plus the Head of BOA Foundation or the CEO sign off. Real personal data: POPIA position confirmed |
| 4. Build | Builder, Tester, Design lead, Design critic | Thin end-to-end slice first, then skeleton, look and feel, logic and data; one branch per ticket | Core path works in its real home (the real Sheet, scenario or phone), not just locally |
| 5. Review | Reviewer, judges, me | Pull request with judge results and a plain-language summary | All nine checks pass; Definition of Done ticked |
| 6. Release | Me, Documenter | Merged main, version tag, CHANGELOG entry, runbook with rollback | Checked on a phone; live deployment version recorded; owner named |
| 7. Operate and learn | Me, Builder, Reviewer | Small fixes as pull requests; postmortems; review on a set date | At review: keep, improve (new Brief) or retire |

**Test phase and go-live are separate releases.** A build can be in use with sample data and personal accounts (test) before it moves to organisational accounts and real data (live). Going live is its own release with its own gate: approvals, POPIA position, organisational accounts, test label removed.

**Circuit breaker.** When the appetite runs out and the build is not done, stop. Cut scope to what works and ship it, or take it back to phase 2. Never extend automatically.

**No backlog.** An idea that loses at phase 3 goes back to Ideas. It does not join a queue that has to be groomed.

**Projects already running.** A project found in use without its phase 1 to 3 files gets them written after the fact: a Brief, ADR 0001 for the stack, and a CHANGELOG that records what is live. Each is marked "written after the fact", and facts nobody recorded are asked for, never guessed or left as placeholders. Nothing in the running system changes until those files exist.

## Quality checklist

Work counts as professional when it passes these nine checks. Run them on every pull request; a failing check blocks the merge. Where a platform has no automated judge (Apps Script, Make.com), the check is done by hand and recorded in the pull request.

| Quality | What done looks like | Checked by | Pass mark |
| --- | --- | --- | --- |
| Consistent design | Every colour, font, spacing and corner comes from the tokens file | Linter rule, design critic | No hard-coded values outside tokens |
| Responsive | Works on phone, tablet and desktop with no sideways scrolling | Playwright screenshots, my own look | No overflow at 375, 768 and 1280 px |
| Accessible | Readable contrast, keyboard use, labelled forms and images | axe, Lighthouse | No axe violations; Lighthouse 90+ |
| Fast | Opens quickly on a weak connection | Lighthouse performance | 90+ on mobile |
| Complete states | Empty, loading, error and offline states on every screen | Playwright tests, Reviewer | All states present |
| Correct behaviour | Main journeys work and keep working after changes | Playwright and unit tests | All tests pass |
| Clean code | Consistent formatting, no type errors, readable structure | Linter, type checker | Zero errors |
| Documented | A newcomer can run it from the repo alone | Documenter, my read-through | Setup works from README and SETUP alone; the successor test passes |
| Safe basics | No keys in code, no real personal data in tests, failures are visible | Secret scanner, my check before launch | Nothing sensitive in the repo; no silent failures |

**Definition of Done** (all ticked before a change is called done):

- [ ] Does what the Brief said, and nothing outside its no-gos
- [ ] The nine checks pass, or a failing one is recorded with a reason and a fix date
- [ ] Critical path walked through by hand, on a phone
- [ ] Error cases handled: bad input, no signal, empty data, duplicate trigger
- [ ] Failures are logged or alerted, never silent
- [ ] README, CHANGELOG and runbook updated; ADR written for any hard-to-reverse choice
- [ ] Rollback path known and written down
- [ ] Merged to main; the live deployment matches main

**Successor test.** If I disappeared tomorrow, could someone run this within a week from the repo alone: trigger, parts, data map, failure points, owner? If not, it is not documented.

## The AI team

I am the director: I choose the look, approve every plan and merge every pull request. Start with Planner, Builder and Reviewer; add a role only when a specific problem appears.

| Role | Job | Brief it with | Tools |
| --- | --- | --- | --- |
| Planner | Turns the idea into a Brief and small tickets, each with a "done when" test | Idea, audience, must-haves, appetite | Claude chat in the project |
| Design lead | Turns my moodboard into a tokens file and design brief | 3 to 5 references I picked, fonts, a palette from a real photo | Claude Code; Kimi for options, as raw material only |
| Builder | Writes one ticket on its own branch | The ticket, AGENTS.md, tokens file, which checks must pass | Claude Code when I watch; Codex for queued tickets |
| Reviewer | Reads each pull request against the original Brief, not the Builder's summary | Ask for bugs, security, accessibility and token breaches, by severity | A different model from the Builder |
| Tester | Writes tests and runs the judges | Tests for each main journey, plus Lighthouse and axe | Claude Code or Codex |
| Design critic | Compares screenshots with moodboard and tokens | Screenshots, tokens, moodboard; ask what feels generic | Any image-capable model |
| Documenter | Updates README, CHANGELOG, runbook and AGENTS.md | "Update docs for what changed" at the end of every pull request | Any cheaper model |

Team rules: the Reviewer is never the Builder's session. One tool per branch at a time. Review loops stop after two rounds and the decision comes to me.

**Reading code.** The judges check style, layout, accessibility and speed, so I do not need to read that code. I do read, and must be able to explain, any code that touches data, money, sign-in, codes or personal information, and the logic of the main journeys. The Builder points out those parts in every pull request summary. This replaces v0.1's line that I never need to read code: judges are weakest exactly where errors cost most, and reading diffs is how my competence in JavaScript and APIs grows.

**How the team runs inside one project.** The roles are hats Claude wears in turn, not separate projects. At each step Claude says which role it is working as. The handover between roles is a file in the repo (Brief, tickets, design brief), never a chat message, so moving from one step to the next loses nothing. **Front end** (what people see and tap) and **back end** (the server and the data behind it) are two kinds of Builder ticket, not two teams. The **Reviewer** works in a fresh chat in the same project, so it judges the work against the Brief without the Builder's assumptions.

## Repository and documentation

Every project uses the same layout, so any project opens cold and makes sense in five minutes. Documentation lives in the repo beside the code and changes with it.

```text
project-name/
  README.md          what it is, who owns it, how it fits together, where it is deployed
  SETUP.md           step-by-step setup from nothing
  AGENTS.md          rules for every AI tool: commands, conventions, role briefs, review guidelines
  CLAUDE.md          first line @AGENTS.md, then Claude-only notes (keep short)
  CHANGELOG.md       dated changes, newest first, with the live deployment version
  .env.example       every config key with a dummy value; the real .env is never committed
  docs/
    brief.md         the Brief from phases 1 to 3
    decisions/       ADRs: 0001-stack.md, 0002-...
    runbook.md       operate, restart, roll back; failure points; who to call
    postmortems/     one file per incident
  design/tokens      colours, type, spacing, corners
  src/ or assets/    the code
  tests/             tests mirror the code
  platform/          code that runs on another platform: apps-script/, make/ (see next section)
```

| File | Answers | Update when |
| --- | --- | --- |
| README | What is this, how does it fit together, where is it running? | Setup, deployment or ownership changes |
| AGENTS.md | What must every tool know that it cannot infer from the code? | A tool repeats a mistake twice; prune monthly |
| Brief | Why does this exist, what is out of scope? | Scope changes: rewrite it, do not append |
| ADR | Why did we choose X over Y? | Stack, platform, data model, third-party service, anything costly to reverse |
| CHANGELOG | What changed, when, and which version is live? | Every release and every platform deployment |
| Runbook | What do I do when it breaks at 7am? | Every incident that taught something new |

**Decisions: two weights.** Small choices go as one line in `docs/decisions/log.md` (date, choice, why). A choice that is costly to reverse gets a full ADR. One decision per ADR, never edited after acceptance; a changed mind gets a new ADR that marks the old one superseded.

## Learning documents: App Guide, Concepts handbook, glossary

Every app is explained in plain language, so I understand why it is built the way it is and can explain it to someone with no background. Three documents do this.

| Document | Where | What it holds |
| --- | --- | --- |
| **App Guide**, one per app | `docs/guide.md` in the app's repo | What the app does; each part, where it lives and why; the subject behind it; every decision, with the alternative turned down; how to do common jobs. Written as questions and answers |
| **Concepts handbook**, one for all apps | The `build-standards` repo, beside this SOP | The ideas that repeat across apps (server, database, repository, deployment, cache), each explained once in depth. App Guides link to it rather than repeat it |
| **Glossary**, one for all apps | At the end of the Concepts handbook | Every term in one line, linked to its full entry |

**Every explanation has six parts:**

1. **The question, as I would ask it.** "Why does Tour Timer have Apps Script files and the training tracker doesn't?"
2. **The answer in one sentence.** "The training tracker has no server; Tour Timer does."
3. **An everyday picture.** The training tracker is a notebook in your pocket; Tour Timer is a whiteboard four people write on, so something must hold the whiteboard.
4. **The term, defined.** *Server:* a program that sits in the middle and holds information several devices share.
5. **Why this choice, and what was turned down.**
6. **What would change the answer.** "If the tracker had to share workouts between two phones, it would need a server too."

**The test for every entry:** after reading it once, could I explain it to someone with no background, without looking? If not, it is rewritten.

**Rules:** Claude defines each new term the first time it appears, in chat and in the glossary. No release is done until the App Guide is updated. At the end of each phase Claude asks me two or three short questions about what was built and why, which I may skip.

## Platforms you cannot deploy from a repo

Some code runs inside another platform's editor: Apps Script, Make.com, Donorbox forms, Circle.so settings. The repo is still the source of truth. The platform holds a deployed copy, and the CHANGELOG records which copy is live.

Tour Timer showed why: the server code lived only in the Apps Script editor and in chat artifacts, with no copy in GitHub.

| Platform | Copy kept in the repo | How changes reach the platform | How to roll back |
| --- | --- | --- | --- |
| Apps Script | `platform/apps-script/`: every `.gs` file plus `appsscript.json` | Preferred: clasp, Google's command-line tool, pushes the folder to the project. Until it is set up: paste each changed file from the repo, never from chat | Deploy › Manage deployments: edit the web app deployment and pick the previous version. The web address stays the same |
| Make.com | `platform/make/`: each scenario's exported blueprint (JSON) plus a data map | Edit in Make, then export the blueprint and commit it the same day | Import the previous blueprint from the repo |
| No-code settings (Donorbox, Circle.so, WhatsApp Business) | `docs/platform-settings.md`: the settings that matter, with screenshots that show no keys or personal data | Change in the platform, then update the file | Restore from the file |

**The paste rule.** Code from Claude goes into the repo first, then from the repo into the platform. If I paste from chat straight into an editor, the repo and the platform drift apart and nobody can tell which is right.

**Deployment versions.** Every Apps Script deployment gets a version description matching the CHANGELOG entry, for example `v1.1.0 split tours`. The CHANGELOG records the deployment version number so live, repo and log can be compared in a minute.

**Drift check.** Before any change, and at each review date, confirm the platform matches the repo. Claude can compare them in the browser by checksum.

## Version control and release

Main always works. Every change is small, has a reason in its commit message, and can be undone in seconds.

1. **One branch per ticket,** named for intent: `feat/split-tours`, `fix/phone-offline-sync`. Merge within a day where possible; never let a branch outlive a week.
2. **Commit messages say what and why,** using Conventional Commits. Never leave GitHub's default "Update file.js".
   - `feat:` new behaviour a user sees
   - `fix:` a bug fix
   - `docs:` documentation only
   - `refactor:` restructure, same behaviour
   - `test:` tests only
   - `chore:` tooling, dependencies, platform sync
3. **Pull request every time,** even working alone. It carries the plain-language summary, the judge results, and the parts I must read (see Reading code).
4. **Version with SemVer.** MAJOR breaks something users rely on, MINOR adds behaviour, PATCH fixes. Tag each release in GitHub: `v1.0.0`.
5. **Release checklist:** CHANGELOG entry; tag; platform deployments updated with a matching description; live deployment version recorded; checked on a phone.
6. **Separate deploy from release where possible.** Ship switched off (a config flag, a disabled Make route), switch on once verified.

## Packaging and delivery

Packaging is how a finished app reaches people's phones and computers. Default to level 1 and move up only when something forces it: the public must find the app in a store, or it needs a phone feature the browser cannot reach. The level chosen, and why, is an ADR at phase 6.

| Level | What it is | Works on | Cost (USD) | How users get updates |
| --- | --- | --- | --- | --- |
| 1. Installable web app (PWA) | A website that installs like an app: icon on the Home screen, works offline. Tour Timer and the training tracker are this | Android, iPhone, Windows, Mac | Free | Automatically, next time the app opens |
| 2. Store listing of the web app | PWABuilder (a free Microsoft tool) wraps the web app for each store | Google Play, Microsoft Store, Apple App Store | Google Play $25 once; Microsoft Store free for individuals ($99 once for a company); Apple $99 a year | Content updates with the website; resubmit only when name, icon or permissions change |
| 3. Wrapped app with phone features | Capacitor puts the web app inside a real phone app with camera, notifications and so on | Android, iPhone | Same store fees | Rebuild and resubmit each release; store review takes days |
| 4. Native app | Written specially for each platform (Kotlin for Android, Swift for iPhone) | One platform per build | Same store fees, much more work | As level 3 |

**Notes:**

- Staff-only work apps need no store: level 1, shared by link.
- Apple packaging needs a Mac; PWABuilder's iPhone output is still experimental and Apple reviews more strictly.
- Store accounts for work apps are organisational accounts and need approval from the Head of BOA Foundation or the CEO. Prices are in US dollars; the ZAR cost follows the exchange rate. Check current prices before signing up.

**Updating after release** follows the same loop every time: a ticket, a branch, the change, review, a new version number, a release. For a level 1 app: commit to GitHub (the pages update within minutes), raise the cache version in the service worker so devices fetch the new files, and deploy a new version of any platform code (such as Apps Script).

## Debugging and postmortems

Debug by experiment: change one thing at a time and write down what happened. Random edits create new bugs faster than they fix old ones.

1. **Stabilise.** If people are affected, restore service first: roll back the deployment, switch off the scenario or flag. Diagnose after.
2. **Reproduce.** Make it happen on demand; write down the input, device and steps. No reproduction, no fix: add logging and wait.
3. **Read the evidence.** Full error text, Apps Script Executions log, Make execution history, browser console, the actual payload. The first error usually explains the rest.
4. **Isolate.** Ask what changed first: compare with the last version that worked. Halve the path until one part fails.
5. **Hypothesise and test one change.** "I think X because Y; if so, changing Z fixes it." Change only Z; record the result either way.
6. **Fix the root cause.** Ask why until you reach something in the system you can change.
7. **Lock it in.** Add a test that fails without the fix and passes with it.
8. **Log it.** One line in the issue log; a postmortem if it affected people or data, or took more than two hours.

**Two-hour rule.** Stuck for two hours: stop and write the bug report (template below) as if for a stranger. Writing it often reveals the answer; if not, it is ready for Claude or a person.

**Handing a bug to Claude:** give the bug report and the files involved, and ask for hypotheses ranked by likelihood before any fix.

**Postmortems are blameless.** They name contributing causes in process and tooling, never fault in a person, myself included. Every action item has one owner and a date.

## Ground rules

These apply to every tool and every role, and matter more than any tool choice.

- **The repo is home.** Tools enter by cloning or opening a branch and leave by committing or opening a pull request. Code reaches a platform from the repo, never from chat (see Platforms).
- **One source of truth.** AGENTS.md holds the rules, the tokens file holds the look, `docs/` holds the Brief, decisions and runbook.
- **I merge.** Nothing reaches main without my approval and a plain-language summary.
- **Safe data only.** Sample or synthetic data until go-live. Never give a tool passwords, API keys, `.env` files or real personal data; chat tools send prompts to the provider's servers.
- **Secrets stay out of chat, including screenshots.** Crop or blur settings, codes and keys before sharing a screen. A secret that has appeared in chat or a commit is rotated the same day, at a moment that doesn't disrupt people using the app (for Tour Timer: after the last tour).
- **Failures are loud.** Every automation logs or alerts when it fails; nothing fails silently.
- **Approvals are steps, not afterthoughts.** Work apps that change how people work name the approval step in the plan: process owner plus the Head of BOA Foundation or the CEO.
- **POPIA before real data.** Before real names, contact details or other personal data enter any tool or account, confirm the POPIA position and move to organisational accounts.
- **Security check before launch.** Apps holding sign-in, payments or personal data get a human security review first.
- **Retire what is unused.** Switch off and archive scenarios, triggers and deployments nobody uses; record it in the CHANGELOG.

## Choosing languages

The language is decided by where the code runs, not by Claude's preference each time. Claude proposes, this table decides, and ADR 0001 records the choice.

| Where the code runs | Language | Example |
| --- | --- | --- |
| In a browser or installed web app: what people see and tap | HTML (structure), CSS (look), JavaScript (behaviour) | Tour Timer's screens, the training tracker |
| Inside Google: Sheets, Gmail, Drive | Apps Script, which is JavaScript | Tour Timer's server |
| Connecting online services to each other | Make.com: no code, or small pieces of JavaScript | The Donorbox thank-you workflow |
| On a computer: data, reports, files, scheduled jobs, build and test scripts | Python | The training tracker's build script and tests |
| Larger web apps with their own accounts and database | TypeScript: JavaScript with built-in checking that catches mistakes before the app runs | None yet |

This keeps every app to two languages, JavaScript and Python, which cover almost everything. Any other language needs an ADR that says what these two cannot do.

## Starting stacks

Two approved starting points. Choose in phase 2 and record the choice and the reason in ADR 0001. Either may be departed from with an ADR.

| Layer | A: Web app stack | B: Google Workspace stack |
| --- | --- | --- |
| Use when | The app needs its own accounts, a real database or heavier logic | Free hosting, staff already use Google, data fits in a Sheet, a few devices |
| Pages | HTML, CSS, TypeScript; React with Vite | HTML, CSS, plain JavaScript on GitHub Pages |
| Data | Supabase or Firebase | Google Sheet, one tab per kind of record |
| Server logic | Managed backend; Node.js or Python only if needed | Apps Script web app |
| Email, files, schedules | Provider services | Gmail, Drive, Apps Script triggers |
| Watch for | Running costs; sign-in security | Sheet size and speed; Apps Script quotas; GitHub Pages needs a public repo on a free account, so the pages may hold no codes, names or keys |
| Example | none yet | Tour Timer |

Native phone apps (Kotlin for Android, Swift for iOS) are not a default. A web app added to the Home screen covers most needs; choose native only with an ADR that names what the web cannot do.

## Public apps and children's apps

Apps anyone can use, and above all apps for children (such as the planned Cango and BOA games), follow extra rules. This is the working, not legal advice.

**The law.** Under POPIA, anyone under 18 is a child. Section 34 prohibits processing a child's personal information unless a section 35 exception applies, usually prior consent from a parent or guardian. The US rule the app stores enforce (COPPA) covers under-13s; POPIA's line is stricter, so design for POPIA.

**Default design rule: collect nothing.** No accounts, names, emails or photos; no ads; no third-party analytics; no chat; no location. With nothing collected, POPIA's children's rules do not come into play. Any game that would need to collect something stops for legal advice before it is built.

**Store rules, if a game ever goes into a store.** Google Play's Families policy: declare the age group; no device identifiers or location from children; only Google-approved ad and analytics kits; a privacy policy. Apple's Kids Category: no third-party analytics or ads. The collect-nothing rule meets both.

**Delivery.** Start each game as a web game played in the browser: no install, no store. Add a store listing only once a game proves itself.

**Work rules that also apply:** organisational accounts; the Head of BOA Foundation or the CEO sign off before anything goes public; the Cango brand guide applies (education leads with Cango); what the games teach and how they are promoted involves the marketing lead, named as a step in the Brief.

**Gate before any public release:**

- [ ] Content suitable for the age group
- [ ] No manipulative design: no pressure to keep playing, no tricks to buy
- [ ] A privacy policy that states what is collected (for the default rule: nothing)
- [ ] A check that the game sends no data over the network
- [ ] Sign-off recorded in the Brief

## Templates

Copy these into the repo at the start of each project.

### Brief (`docs/brief.md`)

```markdown
# Brief: <project>
Type: work | personal   Size: small | standard | full   Owner: <name>   Date: <yyyy-mm-dd>

## Problem
Who has it, what happens today, what it costs (time, errors, money).

## Outcome (written as if shipped)
Two or three sentences on what the user can now do.

## Success measure
One observable signal.

## Appetite
1 day | 1 week | 2 weeks | 6 weeks

## Rough solution
Main parts and how data moves between them.

## Rabbit holes
Risks and unknowns, and how each is handled.

## No-gos
What this will not do.

## Data and approvals (work apps)
Personal data touched, where it goes, POPIA position, who signs off.

## Decision
Go | No-go | Re-shape   Signed off by: <name>, <date>
```

### ADR (`docs/decisions/0001-<title>.md`)

```markdown
# ADR 0001: <decision>
Status: Proposed | Accepted | Superseded by ADR 000X
Date: <yyyy-mm-dd>

## Context
What problem makes this decision necessary?

## Options considered
1. Option A: for, against, cost
2. Option B: for, against, cost

## Decision
We will <decision>.

## Consequences
What becomes easier, what becomes harder, what to watch.
```

### CHANGELOG entry

```markdown
## [1.1.0] - 2026-11-20
Apps Script deployment: version 7 ("v1.1.0 split tours")
### Added
### Changed
### Fixed
```

### Postmortem (`docs/postmortems/<date>-<title>.md`)

```markdown
# Postmortem: <title>
Date:   Duration:   Owner:

## Impact
Who was affected, how, for how long.

## Timeline
hh:mm  what happened / what was done

## Contributing causes
Process, tooling and system factors. No individual blame.

## What went well / poorly / where we got lucky

## Actions
| Action | Owner | Due |
```

### Bug report

```markdown
Expected:
Actual:
Steps to reproduce: 1. 2. 3.
Where: device, browser, version, deployment
Error text or log excerpt (no codes or keys):
Already ruled out:
```

## Changes, open items and sources

**v0.4 (14 November 2026)**

- Instructions block: rule 14, every question counts and goes into the Concepts handbook; rule 15, GitHub files in a project need Sync now, and Claude checks whether the project is behind; rule 16, every reply that makes or changes a file ends with a "Where this goes" list.
- Concepts handbook version 2: Part 4, Working on GitHub step by step (entries 28 to 32), and the Questions asked log.

**v0.3 (14 November 2026)**

| Change | Why |
| --- | --- |
| Added project types (APP Ideas, app projects, optional subject projects), the APP naming prefix and what goes in Instructions and Context | Two apps shared one project; context files held outdated copies of code and programmes |
| Added the one-real-copy rule for content | The training programme existed in Fit's files and in the app's data, and they had drifted apart |
| Added Learning documents: App Guide, Concepts handbook, glossary, and the six-part explanation shape | I have no coding background and want to understand each decision well enough to explain it |
| Added Packaging and delivery, with update paths | No guidance on getting apps onto phones and computers or on updating them afterwards |
| Added Choosing languages | Languages were left to Claude each time |
| Added Public apps and children's apps | Kids' games for Cango and BOA are planned for public release |
| Added how the team runs inside one project | Roles were unclear when everything happens in one project |
| Replaced placeholder markers with asking for missing details | Placeholders left gaps in finished documents |

**v0.2 (10 November 2026)**

| Change | Why |
| --- | --- |
| Added Capture, Frame and Decide phases, appetite and the circuit breaker | v0.1 started at "spec" with no check that the problem was worth solving and no time limit |
| Added test phase versus go-live as separate releases | Tour Timer is in use with sample data before approvals; v0.1 had no word for that |
| Replaced "never need to read code" with the reading-code rule | Judges are weakest on data, sign-in and security logic |
| Added the Platforms section and the paste rule | Tour Timer's server code was only in the Apps Script editor and chat artifacts |
| Added versioning, CHANGELOG with deployment versions, and the release checklist | Tour Timer had five commits with default messages and no tags |
| Added the debugging protocol, postmortems and Definition of Done | v0.1 had no guidance for when things break |
| Added the Google Workspace stack beside the web stack | Recorded what worked for Tour Timer as an approved option |
| Added secrets-in-screenshots and approval-step rules | A screenshot shared on 10 November showed live codes |

**Open items**

- [ ] Create the `build-standards` repo with this SOP and the Concepts handbook, and link both into each APP project's Context
- [ ] Tour Timer: upload the App Guide and the updated brief; rotate the phone key and admin code after a day's last tour
- [ ] Training tracker: upload the App Guide; split HANDOVER.md into brief, decisions log and CHANGELOG; tag a release; fix the tests' hard-coded folder path; remove `backups/` and `theme-previews/`
- [ ] Remove the old app files from APP Ideas' Context once the guides are uploaded
- [ ] Set up clasp for Apps Script so code goes from the repo to the platform without pasting
- [ ] Set up the automated judges (linter, Lighthouse, axe, Playwright) as GitHub Actions on the next web project
- [ ] Tour Timer go-live gate: the Head of BOA Foundation and the CEO approve Google Workspace and GitHub; organisational accounts; POPIA position before real guide names
- [ ] Kids' games: create a subject project with the marketing lead for the learning content before the first Brief
- [ ] Review this SOP on 7 December 2026, or after the next project

**Sources**

- [Shape Up](https://basecamp.com/shapeup/0.3-chapter-01), Basecamp: appetite, shaping, betting, circuit breaker
- [Working Backwards excerpt](https://www.aboutamazon.com/md/news/workplace/an-insider-look-at-amazons-culture-and-processes), Bryar and Carr: start from the user's outcome
- [Documenting Architecture Decisions](https://www.cognitect.com/blog/2011/11/15/documenting-architecture-decisions), Michael Nygard
- [Accelerate and the DORA capabilities](<https://en.wikipedia.com/wiki/Accelerate_(book)>): small batches, trunk-based development
- [Postmortem Culture](https://sre.google/sre-book/postmortem-culture/), Google SRE Book
- [Claude Code best practices](https://code.claude.com/docs/en/best-practices), Anthropic: explore, plan, code, commit
- [Conventional Commits](https://www.conventionalcommits.org) and [Semantic Versioning](https://semver.org)
- v0.1 sources: [Claude Code subagents](https://code.claude.com/docs/en/sub-agents.md), [Codex code review in GitHub](https://developers.openai.com/codex/integrations/github)

* v0.3 sources: [POPIA and children's information (MJK Inc)](https://mjkinc.co.za/popia/childrens-information), [Information Regulator: POPIA Part C](https://inforegulator.org.za/knowledge-base/category/popia/chapter-3-conditions-for-lawful-processing/part-c-processing-of-personal-information-of-children/), [Google Play Families policy](https://support.google.com/googleplay/android-developer/answer/9893335?hl=en), [Apple Kids Category summary (ConductAtlas)](https://conductatlas.com/platform/apple/apple-app-store-review-guidelines/provision/CA-P-018790/kids-category-apps-must-not-include-third-party-analytics-or-ads/), [Store fees (Windows Central)](https://www.windowscentral.com/microsoft/windows-11/microsoft-store-drops-fees-for-individual-developers-apple-still-charges-usd99-per-year), [PWABuilder and Capacitor (Capgo)](https://capgo.app/alternatives/pwabuilder/), [Projects in Claude](https://support.claude.com/en/articles/14116274-organize-your-tasks-with-projects-in-claude-cowork), [Large project context (RAG)](https://support.claude.com/en/articles/11473015-retrieval-augmented-generation-rag-for-projects)
