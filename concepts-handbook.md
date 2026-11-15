# Concepts handbook

The ideas behind every app I build, explained once, in plain language. Each App Guide links here instead of explaining the same idea again. Version 2, 14 November 2026.

**How to read an entry.** Every entry answers one question in six parts: the question, the answer in one sentence, an everyday picture, the term defined, why it was chosen over the alternative, and what would change the answer. The test for every entry: after reading it once, could you explain it to someone with no background, without looking?

The examples come from two apps:

- **Tour Timer:** a TV in the waiting area shows the next guided tour and a countdown; guides log tours on two phones; an admin page shows reports; a daily report is emailed.
- **Training tracker:** a phone app that runs two training programmes (Heavy Duty and Powerbuilding), logs every set, and works without signal.

## Contents

**Part 1: What an app is made of**
1. What is a web app?
2. What are the front end and the back end?
3. What is a server, and why does Tour Timer need one when the training tracker doesn't?
4. What is a database, and why is a Google Sheet good enough for Tour Timer?
5. What is Apps Script?
6. What is hosting, and what is GitHub Pages?
7. How do the phones and the TV talk to the server? (API and requests)
8. What is JSON?
9. What is the difference between code and data?
10. Where does an app keep information on the phone itself? (browser storage)
11. How does an app keep working without signal? (offline queue and sync)
12. What is a service worker, and what is the cache?
13. What is an installable web app (PWA)?

**Part 2: Keeping the work safe**
14. What is a repository?
15. What is a commit, and what is version history?
16. What are branches and pull requests?
17. What is a deployment?
18. What are releases, tags and version numbers?
19. What is a rollback?
20. What is drift?
21. Why is the repo public, and what must never go in it?
22. What are codes, keys, salts and hashes?

**Part 3: How the building is done**
23. What is a build script?
24. What are automated tests?
25. What are Claude's Instructions, Context files and Memory?
26. What is an artifact?
27. What are the Brief, the ADR and the App Guide for?

**Part 4: Working on GitHub, step by step**
28. Where am I when I'm on GitHub?
29. What happens when I upload a file and click "Commit changes"?
30. Why does a Tour Timer code change touch three places?
31. Why does a Claude project link to GitHub instead of holding uploaded files, and what is "Sync now"?
32. What is the routine after any change, and who does what?

**Questions asked:** every question, with the entry that answers it.

**Glossary** at the end.

---

## Part 1: What an app is made of

### 1. What is a web app?

**Answer:** an app that runs inside a web browser (Chrome, Safari, Edge), so the same app works on any phone or computer.

**Picture:** a web app is like a radio station rather than a CD. A CD has to be made separately for each player; a radio station broadcasts once and any radio can tune in. One web app works on Android, iPhone, Windows and Mac because every one of them has a browser.

**Term:** *web app:* a set of pages written in HTML, CSS and JavaScript that a browser opens and runs. *HTML* gives the structure (headings, buttons, tables), *CSS* gives the look (colours, sizes, layout), and *JavaScript* gives the behaviour (what happens when you tap, countdowns, saving).

**Why this and not a phone app from a store:** a web app is free to publish, needs no store approval, works on every device, and updates itself when you change it. A store app must be built separately for Android and iPhone, costs store fees, and every update goes through review.

**What would change it:** an app that needs phone features a browser cannot reach, or that the public must find in an app store. See the Packaging section of the SOP.

### 2. What are the front end and the back end?

**Answer:** the front end is what people see and tap; the back end is the part behind the scenes that stores information and does the work nobody sees.

**Picture:** a restaurant. The dining room, menus and waiters are the front end. The kitchen, the fridge and the stock room are the back end. Guests never see the kitchen, but nothing reaches the table without it.

**Term:** *front end:* the screens and buttons, running on the person's own device. *Back end:* the server, the database and the rules that run there.

**In our apps:** Tour Timer's front end is the TV page, the two phone pages and the admin page. Its back end is the Apps Script and the Google Sheet. The training tracker is all front end: it has no back end at all (see entry 3).

**What would change it:** whenever information has to be shared between devices, a back end is needed.

### 3. What is a server, and why does Tour Timer need one when the training tracker doesn't?

**Answer:** a server is a program that sits in the middle and holds information that several devices share; Tour Timer has four devices sharing one set of tours, the training tracker has one phone.

**Picture:** the training tracker is a notebook in your pocket: only you write in it, so it can live with you. Tour Timer is a whiteboard in the office that four people write on (the start phone, the end phone, the TV reading it, the admin page). Something has to hold the whiteboard in one place where everyone can reach it. That something is the server.

**Term:** *server:* a program running on a computer that is always on and always reachable over the internet, which other devices send information to and ask information from.

**Why Tour Timer uses Apps Script as its server and not a rented one:** a rented server costs money every month, needs updates and security care, and someone must look after it. Apps Script is free, already inside Google, and Google looks after the computer it runs on.

**What would change it:** if the training tracker had to share workouts between your phone and a friend's, or back them up somewhere other than the phone, it would need a server too.

### 4. What is a database, and why is a Google Sheet good enough for Tour Timer?

**Answer:** a database is where an app's information is kept in an organised way; a Google Sheet works as one when the amount of information is small and people want to read it themselves.

**Picture:** a filing cabinet with labelled drawers. Each drawer holds one kind of record (tours, guides, settings), and every record in a drawer has the same fields.

**Term:** *database:* organised, stored information an app reads and writes. In Tour Timer each Sheet tab is a drawer: Ops (every change ever made), Guides, Settings, Promo, Tours and Change log.

**Why a Sheet and not a real database (such as Supabase):** it is free; staff can open it and read it like any spreadsheet; there is no extra service to sign up for, approve or look after; and Apps Script can read and write it directly.

**What would change it:** a Sheet slows down as it grows into tens of thousands of rows, and it is not built for many people writing at the same instant. Tour Timer's Ops tab grows by a few hundred rows a week, so it needs an archive routine before it gets large. Many devices or a lot of data would mean a real database.

### 5. What is Apps Script?

**Answer:** Google's built-in way to write small programs that work inside Google Sheets, Gmail and Drive, and it can also act as a simple server.

**Picture:** a clerk who lives inside the filing cabinet. The clerk can read and write the drawers (the Sheet), post letters (Gmail), file copies (Drive), set an alarm clock (triggers), and answer questions through a hatch in the wall (the web address the TV and phones call).

**Term:** *Apps Script:* JavaScript that runs on Google's computers, attached to a Google file. *Trigger:* an instruction to run a piece of the script on a schedule, such as Tour Timer's check every 15 minutes to send the daily report. *Web app (in Apps Script):* the script published at a web address so other devices can send it requests.

**Why Apps Script for Tour Timer:** it is free, needs no server of our own, already has permission to use the Sheet, Gmail and Drive, and staff already use Google.

**What would change it:** heavier use than Google's daily limits (called quotas), or a move away from Google Workspace.

**Where its code lives:** the Apps Script editor holds the running copy. The repo folder `platform/apps-script/` holds the master copy (see entries 14 and 20).

### 6. What is hosting, and what is GitHub Pages?

**Answer:** hosting means putting an app's files somewhere the internet can reach them; GitHub Pages is a free host that publishes files straight from a GitHub repository.

**Picture:** writing a poster is not enough; it has to hang on a noticeboard where people walk past. Hosting is the noticeboard.

**Term:** *hosting:* storing files on a computer that is always on and reachable by a web address. *GitHub Pages:* GitHub's free hosting for *static pages*, meaning pages that are just files and run no server code of their own.

**Why GitHub Pages for both apps:** it is free, it publishes automatically every time the repo changes, and the code and the published site live in the same place.

**What would change it:** on a free GitHub account, Pages only publishes from a public repository (see entry 21). An app that must hide its code would need a paid plan or another host.

### 7. How do the phones and the TV talk to the server?

**Answer:** they send short messages, called requests, to the server's web address, and the server sends a reply.

**Picture:** a takeaway counter with a numbered menu. You can only order what is on the menu, in the agreed way; the kitchen checks your order and hands back what you asked for, or says why it cannot.

**Term:** *API (application programming interface):* the menu of requests a server accepts and the replies it gives. *Request:* one message to the server. Tour Timer's API accepts four kinds: `tv` (what is the status now), `phone` (here are my changes, what is new), `admin` (sign in, reports, settings) and `ping` (are you there).

**Why it matters:** the server checks every request before acting. Tour Timer's server refuses a change from a guide not in the Guides tab, a count over 80, or a time more than three days old. A wrong or tampered request gets a refusal with a reason, not a broken Sheet.

**What would change it:** a new feature that needs new information means a new item on the menu, in both the server and the pages.

### 8. What is JSON?

**Answer:** a plain-text way of writing down information so both people and programs can read it.

**Picture:** a form with labels: "name: Thandi, code: 2481". Every value has its label next to it.

**Term:** *JSON:* text in the form `{"name": "Thandi", "active": true}`. Curly brackets hold a record; square brackets hold a list.

**Where you see it:** Tour Timer's phones send changes to the server as JSON, and the Ops tab stores each change as JSON. The training tracker's programmes are JSON files (`hd.json`, `pb.json`).

**Why JSON:** almost every programming language reads it, and a person can open it and read it too.

### 9. What is the difference between code and data?

**Answer:** code is the instructions the app follows; data is the information it works with.

**Picture:** a recipe book and a pantry. The method (heat, stir, bake) is the code; the ingredients are the data. Change the ingredients and the same method makes a different dish.

**Term:** *code:* instructions written in a programming language. *Data:* information the code reads, such as a programme, tour times or a list of guides.

**Why it matters:** keeping them apart means content can change without touching the code. The training tracker keeps each programme in its own data file (`src/hd.json` for Heavy Duty, `src/build/pb.json` for Powerbuilding). Swapping an exercise changes the data; the code that draws the screens stays the same. Tour Timer keeps tour times and guides in the Sheet for the same reason: admin can change them without a programmer.

**What would change it:** nothing; this separation is a standing rule.

### 10. Where does an app keep information on the phone itself?

**Answer:** in browser storage, a small private space each website gets inside the phone's browser.

**Picture:** a locker at the gym that only opens for you, on that one phone.

**Term:** *browser storage (localStorage):* space in the browser where a website can save information that stays after the page closes. It belongs to one browser on one device. The training tracker keeps every logged set there under the name `heavy-duty-tracker-v1`; Tour Timer's phones keep their waiting changes there.

**Why it matters:** it needs no server and works offline. But it lives only on that phone: clearing the browser's data, or losing the phone, loses it. That is why the training tracker has Export and Restore from backup.

**What would change it:** information that must survive a lost phone, or be seen on another device, belongs on a server.

### 11. How does an app keep working without signal?

**Answer:** it saves each action on the device with the time it happened, then sends the saved actions when signal returns.

**Picture:** writing letters while the post office is closed. You date each letter and keep them in a pile; when the post office opens, you post the whole pile, and each letter still carries the date you wrote it.

**Term:** *offline queue:* the pile of saved changes waiting to be sent. *Sync:* sending the pile and receiving what others changed. Tour Timer's phones sync every 15 seconds and straight after a tap. A change that arrives late is marked in the change log with when it was made and when it arrived.

**Why it matters:** the tour start and end points have unreliable signal. Without a queue, a guide's tap would be lost.

**What would change it:** nothing for these apps; any app used outdoors should have one.

### 12. What is a service worker, and what is the cache?

**Answer:** a service worker is a small helper file that lets pages open without signal; the cache is the copy of the app's files it keeps on the device.

**Picture:** a photocopy of the noticeboard kept in your drawer. If you cannot reach the noticeboard, you read the photocopy.

**Term:** *service worker:* a script (in both apps, `sw.js`) that the browser runs in the background to serve pages from the cache. *Cache:* stored copies of the app's files. *Cache version:* a name such as `tour-timer-v2`; changing it tells every device to throw away its old copy and fetch the new files.

**Why it matters:** it is why both apps open in airplane mode. It is also why, after any change to a page, the cache version must be raised; otherwise phones keep showing the old photocopy. The training tracker calls it `VERSION` in `sw.js`, raised together with `appVersion`.

### 13. What is an installable web app (PWA)?

**Answer:** a web app that can be added to the Home screen and behaves like an installed app, including working offline.

**Picture:** a website that moved in: it gets its own icon on the phone and opens full screen, without the browser's address bar.

**Term:** *PWA (progressive web app):* a web app with a service worker (entry 12) and a manifest, a small file giving its name, icon and colours. The training tracker's is `manifest.webmanifest`.

**Why both apps are PWAs:** they install on any device for free, with no app store, and update themselves. This is level 1 in the SOP's Packaging ladder.

**What would change it:** needing a store listing or phone features the browser cannot reach.

---

## Part 2: Keeping the work safe

### 14. What is a repository?

**Answer:** a folder of all an app's files, kept by Git so every past version is saved.

**Picture:** a project binder in which no page is ever thrown away: when a page changes, the new page goes in front and the old one stays behind it.

**Term:** *Git:* the system that tracks every change to a set of files. *Repository (repo):* the folder Git tracks. *GitHub:* a website that stores repositories online. Tour Timer's is `aljoclaassen/tour-timer`; the training tracker's is `aljoclaassen/training-tracker`.

**Why the repo is the source of truth:** copies in chats, artifacts or Claude projects go out of date and nobody can tell which is current. The repo always holds the current version and every earlier one, with a note of why each changed.

### 15. What is a commit, and what is version history?

**Answer:** a commit is one saved change with a message saying why; version history is the full list of commits.

**Picture:** a notebook where you never rub anything out. Each change is written on a new page with the date and a note, and every earlier page is still there to look back at.

**Term:** *commit:* a snapshot of the files at one moment, with a message. Each has an ID, a short code such as `c64e092`. *Commit message:* the note, written as what changed and why, for example "Hex Bar Deadlift as the back day finisher". GitHub's default "Update file.js" says nothing and should be replaced.

**Real example:** the training tracker's Heavy Duty programme before the 8 November change is the version saved on 25 October. You can open it as it was at github.com/aljoclaassen/training-tracker/blob/c64e092/src/hd.json. Nothing saved in the repo needs a separate backup.

### 16. What are branches and pull requests?

**Answer:** a branch is a separate copy to try a change on; a pull request asks for that change to be checked and joined back into the main copy.

**Picture:** drafting a change to the house rules on a photocopy, then bringing it to a meeting where it is read and approved before it replaces the real rules.

**Term:** *main:* the main branch, the version that is live. *Branch:* a parallel copy for one change. *Pull request:* a proposal to merge a branch into main, showing exactly what changed, for review.

**Why:** main always works. A half-finished change never breaks the live app, and every change is reviewed before it goes in.

**Where we are:** both repos so far have been changed directly on main. The SOP asks for branches and pull requests from now on, even when working alone.

### 17. What is a deployment?

**Answer:** putting a version of the code where it actually runs for people.

**Picture:** the printed menu on the tables, as opposed to the draft on the manager's desk. Changing the draft changes nothing until the new menu is printed and put out.

**Term:** *deployment:* the running copy. For GitHub Pages, every commit to main deploys automatically within minutes. For Apps Script it is manual: Deploy, Manage deployments, edit, choose New version. Tour Timer's live server is deployment version 3 (v1.0.1, 13 November 2026).

**Why it matters:** saving code in the Apps Script editor does not change what the phones talk to. Only a new deployment version does. Choosing New deployment instead of editing the existing one creates a new web address that the pages do not know, and the TV and phones lose their connection.

### 18. What are releases, tags and version numbers?

**Answer:** a release is a named, recorded version of the whole app that you can always return to.

**Picture:** an edition of a book. "Second edition" tells everyone exactly which text they have.

**Term:** *tag:* a permanent label on one commit, such as `v1.0.0`. *Release:* a tag plus notes on what changed, shown on GitHub. *Version number (SemVer):* three numbers, MAJOR.MINOR.PATCH. MAJOR goes up when something users rely on changes, MINOR when something is added, PATCH for fixes. *CHANGELOG:* the file listing every release, newest first.

**Real example:** Tour Timer's releases `v1.0.0 test baseline` (10 November 2026) and `v1.0.1` (13 November 2026, two rule changes and a form fix, so a PATCH).

### 19. What is a rollback?

**Answer:** going back to the last version that worked when a new one causes problems.

**Picture:** putting the old menu back on the tables while the new one is fixed.

**Term:** *rollback:* restoring a previous version. For Apps Script: Manage deployments, edit, choose the previous version, deploy; the web address stays the same. For GitHub Pages: revert the commit, raise the cache version.

**Why it matters:** the first step in the debugging protocol when people are affected is to roll back, then find the cause calmly.

### 20. What is drift?

**Answer:** when two copies of the same thing stop matching and nobody is sure which is right.

**Picture:** two people keeping the same diary separately; after a month the entries disagree.

**Term:** *drift:* differences between the repo, the running platform and old copies elsewhere. *Checksum:* a short fingerprint calculated from a file's exact contents; two files with the same checksum are identical.

**Real example:** on 10 November, Tour Timer's Apps Script code was checked by checksum against the latest artifacts: they matched. But the code was not in the repo at all, so a mistake in the editor could not have been undone. The fix was `platform/apps-script/` in the repo. The same reasoning removed the old programme files from Claude's context: the repo's data had moved on, and two disagreeing copies confuse Claude as much as people.

### 21. Why is the repo public, and what must never go in it?

**Answer:** free GitHub Pages only publishes from a public repo, so anyone can read the code; therefore nothing secret or personal goes in it.

**Picture:** a shop window. Anyone walking past can see what is displayed, so the safe and the staff files stay in the back office.

**Term:** *public repository:* readable by anyone on the internet. *Private repository:* readable only by people you invite; Pages from a private repo needs a paid plan.

**The rule:** no admin codes, phone keys, passwords, real names, phone numbers or emails in any file in a public repo. Tour Timer keeps all of those in the Google Sheet, which is private. The sample guide codes in `Code.gs` are fake and are replaced before real use.

**What would change it:** an organisation account with paid plans can publish from a private repo.

### 22. What are codes, keys, salts and hashes?

**Answer:** codes and keys are secrets that prove who is acting; salts and hashes let a phone check a code without the code itself being stored on the phone.

**Picture:** a bouncer with a list of fingerprints rather than a list of passwords. You say your password; the bouncer turns it into a fingerprint and checks it against the list. Someone who steals the list gets fingerprints, not passwords.

**Terms:**
- *Guide code:* each guide's 4-digit code, which records who did what. In Tour Timer it is for attribution, not security.
- *Admin code:* opens the admin page and phone overrides. Keep it to admin staff.
- *Phone key:* the secret part of the phone links. Anyone with a phone link can send changes, so the link is shared only with the team, and a new one is made if a phone is lost.
- *Hash:* a fingerprint made from a piece of text. The same text always gives the same fingerprint, but the text cannot be worked back out of it easily.
- *Salt:* a random value mixed in before hashing, so the same code gives a different fingerprint in a different setup. Never change Tour Timer's salt: every stored fingerprint depends on it.

**Rotate:** to replace a secret with a new one after it has been seen by anyone who should not have it, such as appearing in a screenshot.

**With sample data:** a seen code puts little at risk, because the data is not real; the worst case is fake entries in a test. So rotating can wait, but every code and key is replaced before go-live (Tour Timer: SETUP.md, Part F).

---

## Part 3: How the building is done

### 23. What is a build script?

**Answer:** a program that assembles the finished app from its separate source files.

**Picture:** a printer binding loose chapters into one book. You edit the chapters; the binding is done the same way every time.

**Term:** *build:* turning source files into the files that are published. *Build script:* the program that does it. The training tracker's is `src/build/build.py` (Python): it combines the programme data and the screens into one `index.html`, and writes the theme file and the service worker beside it. Tour Timer has no build step: its files are published as written.

**Why the tracker has one:** the finished app is one large file (about 560 kB). Editing it directly would be error-prone; editing small source files and rebuilding is safer.

### 24. What are automated tests?

**Answer:** small programs that use the app the way a person would and check that it still behaves correctly.

**Picture:** a checklist a robot works through after every change: open the app, log a set, check the target moved, check nothing broke.

**Term:** *automated test:* a script with an expected result; it passes or fails. *Playwright:* a tool that drives a real browser for tests. *Regression:* something that used to work and broke after a change; a test written for a bug stops it coming back.

**In our apps:** the training tracker has 39 Python test scripts in `src/tests/`. Tour Timer's v1 passed 37 of 37 checks before release; its Google parts are tested by hand with the checklist in SETUP.md.

**Known issue:** the training tracker's tests only run after replacing a folder path left over from an old Claude session. Fixing that is an open item.

### 25. What are Claude's Instructions, Context files and Memory?

**Answer:** three things a Claude project gives every chat inside it: standing rules, reference files, and what Claude has learned there.

**Picture:** a new staff member's first morning: the house rules (Instructions), the filing cabinet of reference documents (Context), and notes from previous shifts (Memory).

**Terms:** *Instructions:* the rules typed into the project. *Context files:* files and links Claude reads in every chat (called project knowledge in chat projects). Files linked from GitHub update only when you click Sync now (entry 31). Large context is searched rather than read whole, so clear file names help. *Memory:* what Claude has learned in that project's chats; it stays with that project. Chats themselves do not see each other.

**Why one project per app:** each project's context then holds only that app, so nothing is mixed up between apps, and a successor can be handed one project and one repo.

### 26. What is an artifact?

**Answer:** a page or document Claude creates and saves in your Claude account, with its own link.

**Picture:** a document Claude hands you across the desk, which you can keep in your drawer and share.

**Term:** *artifact:* a saved page, document, deck or file created in a chat. The training tracker began as an artifact (the "Strength and Hypertrophy Plan" page) before it moved to a repo.

**Why apps move from artifacts to repos:** an artifact is fine for a first version, but it has no proper version history, cannot be hosted for others the same way, and a copy in a chat drifts from the real one.

### 27. What are the Brief, the ADR and the App Guide for?

**Answer:** the Brief says why the app exists and what it will not do; an ADR records why a big choice was made; the App Guide explains the whole app in plain language.

**Picture:** a building project's client brief, its signed-off design decisions, and the owner's manual.

**Terms:** *Brief:* problem, user, success measure, appetite (how much time it is worth), no-gos. *ADR (architecture decision record):* one decision per file, with the options considered and why one was chosen; never edited afterwards, only replaced by a new one. *App Guide:* `docs/guide.md`, the plain-language explanation of the app, kept current with every release.

**Why:** in three months nobody remembers why something was done. These three documents make the reasons permanent, and let a successor run the app within a week.

---

## Part 4: Working on GitHub, step by step

These entries explain the clicks: where you are on the screen, what each button does, and why the steps come in the order they do.

### 28. Where am I when I'm on GitHub?

**Answer:** inside one repository, looking at one folder or file, on one branch. The web address tells you which.

**Picture:** a building directory. The account is the building, the repo is the office, the folder is the cabinet, the file is the document.

**Reading the address:** `github.com/aljoclaassen/tour-timer/blob/main/docs/guide.md` reads as: account `aljoclaassen`, repo `tour-timer`, viewing a file (`blob`), on branch `main`, folder `docs`, file `guide.md`. An address with `upload/main/docs` means you are uploading into the `docs` folder on main. An address with `tree` means you are looking at a folder.

**The parts of a repo page you use:**

| Where | What it is | Used for |
| --- | --- | --- |
| Code tab, the file list | The current files | Opening, uploading, replacing files |
| "N commits" link, above the file list, with a clock icon | The version history | Seeing what changed, when and why (entry 15) |
| Releases, in the right-hand column | The named versions | Tagging a release (entries 18 and 32) |
| Settings tab, then Pages | Hosting settings | Only for Tour Timer's pages; rarely touched |

**Why it matters:** you upload into whichever folder you are standing in. Before uploading, check the address shows the right folder, or the file lands in the wrong place.

### 29. What happens when I upload a file and click "Commit changes"?

**Answer:** the file goes into the folder you are in; if a file with the same name is already there, it is replaced, and the old version stays in the history.

**Picture:** putting a new page into the binder in front of the old one (entry 14). Nothing is thrown away.

**The steps and why:**
1. **Add file, then Upload files**, while standing in the right folder. Why: the folder decides where it lands.
2. **The commit summary box** under the uploaded files. Replace "Add files via upload" with what changed and why, for example "fix: bring Core.gs up to date with the live editor". Why: this is the only note future you, or a successor, will see in the history.
3. **Commit directly to the main branch**, then **Commit changes**. Why: main is the live version. For now we work directly on main (entry 16).

**Watch out for Tour Timer:** its pages are hosted from main (entry 6), so uploading into `assets/`, or changing `tv.html`, `phone.html` or `admin.html`, changes what the TV and phones show within a few minutes. Uploading into `docs/` changes nothing that runs. A change to the pages also needs the cache number in `sw.js` raised, so the devices fetch the new files (entry 12).

**What would change it:** once branches are in use, step 3 becomes "create a new branch", and the change goes live only when the pull request is merged.

### 30. Why does a Tour Timer code change touch three places?

**Answer:** the repo keeps the record, but the server's code runs in Google, so it must be pasted there and then deployed separately.

**Picture:** a recipe book (the repo), the kitchen (the Apps Script editor) and service (the deployment). Changing the recipe in the book does not change what the kitchen cooks, and a new dish in the kitchen is not served until it goes out.

**The order, and why:**
1. **Repo first:** commit the change (entry 29). Why: the record is never behind what is running.
2. **Apps Script editor:** paste the changed file in and save. Why: GitHub cannot run Apps Script; the editor is where the server's code lives.
3. **Deploy, Manage deployments, edit (the pencil), Version: New version, add a description such as "v1.0.1", Deploy.** Why: saving in the editor does not change what the phones talk to; only a new version does. Never use "New deployment", which makes a new web address the pages don't know (entry 17).
4. **CHANGELOG and a release** (entries 18 and 32). Why: so anyone can see which version is running.

**Real example:** on 13 November, steps 2 and 3 were done (deployment version 3) and `core.js` was updated, but the repo's copy of `Core.gs` was not. Nothing broke, but the record was wrong. That is drift (entry 20). It was found on 14 November by comparing fingerprints of the files, and fixed.

### 31. Why does a Claude project link to GitHub instead of holding uploaded files, and what is "Sync now"?

**Answer:** a link reads the original in the repo, so there is one copy to keep right instead of one per project. "Sync now" is the button that fetches the newest version.

**Picture:** an uploaded file is a photocopy: right on the day it is made, then quietly out of date. A GitHub link is a key to the filing cabinet. "Sync now" is opening the drawer again to see what is new.

**Term:** *sync:* bringing a copy up to date with the original. In a Claude project, GitHub files are fetched when you add them, and again only when someone clicks **Sync now** in the project's Context. It does not happen on its own, and it cannot be set to happen on a schedule.

**Why links, not uploads:** uploaded files cannot be downloaded or moved later, and each must be replaced by hand in every project that uses it. The APP Ideas project ended up holding 22 uploaded files, some out of date.

**What makes up for the manual sync:** two standing rules in the SOP. After every commit to a repo, Claude tells you which projects to sync. At the start of a chat that relies on repo files, Claude compares what it has with the repo and tells you if the project is behind.

**What would change it:** if Claude projects begin syncing GitHub on their own, the second rule can go.

**Knowing what goes where:** files made in a chat are easy to scroll past. So every reply that makes or changes a file ends with a "Where this goes" list (SOP rule 16): the file, where it goes, what to do with it, and why. The usual places:

| Place | What belongs there | Example |
| --- | --- | --- |
| A repo, in a named folder | Anything the app runs on or is documented by | `docs/guide.md` in `tour-timer` |
| A project's Instructions | Standing rules for Claude in that project | The SOP's instructions block |
| A project's Context | Links to the repo files Claude should read | The `build-standards` repo |
| Google Drive | Private papers that hold names or are history only | The original handovers |
| Nowhere | Working copies once the repo has them | A file Claude sent for you to check |

### 32. What is the routine after any change, and who does what?

**Answer:** change, record, run, release, sync. Each step closes a gap that would otherwise cause drift.

| Step | Who | Where | Why |
| --- | --- | --- | --- |
| 1. Make the change and commit it with a clear message | Claude prepares and uploads after your yes; or you upload | GitHub, the right folder (entries 28, 29) | The record comes first |
| 2. Pages changed: raise the cache number in `sw.js` | Claude | GitHub, `sw.js` | Devices fetch the new files (entry 12) |
| 3. Server code changed: paste it into the editor, then a new version of the existing deployment | You | Apps Script (entry 30) | Only a new version goes live |
| 4. Add a CHANGELOG entry, including the deployment version and cache | Claude | GitHub, `CHANGELOG.md` | What runs is written down |
| 5. Tag a release | You | Releases, then Draft a new release: a new tag such as `v1.0.2` on main, a title, notes copied from the CHANGELOG, Publish | A named point to return to (entries 18, 19) |
| 6. Sync now | You | The app's Claude project, Context | The project sees the new files (entry 31) |
| 7. Check | Claude | Compares the repo, the editor and the deployment | Catches drift early (entry 20) |

A change to documents only (`docs/`, README, CHANGELOG) needs steps 1, 6 and 7; a release is optional.

---

## Questions asked

Every question asked while building, however simple, is a sign that something needed explaining. Each is logged here with the entry that answers it. If no entry answered it, a new entry was written.

| Date | Question | Answered in |
| --- | --- | --- |
| Earlier | I pressed Commit and no message came up; where is step 3? | 29 |
| Earlier | Why one Claude project per app? | 25 |
| Earlier | Aren't knowledge files called context files now? | 25 |
| Earlier | How do I download context files? | 31 (you can't, which is why links are used) |
| Earlier | Is all the training programme history in GitHub? | 15 |
| Earlier | Why is a repo public or private? | 21 |
| 2026-11-14 | Did my 13 November Core.gs paste reach the server, and how can you find out? | 20, 30 |
| 2026-11-14 | What do I do with the README, SETUP, CHANGELOG, runbook and SOP files? | 31 |
| 2026-11-14 | Where do the release notes go? | 32 |
| 2026-11-14 | How do GitHub links in a project make things easier? | 31 |
| 2026-11-14 | Do codes need changing when the data is only samples? | 22 |
| 2026-11-14 | Can syncing happen automatically? | 31 |
| 2026-11-14 | When you tell me to do something on GitHub, where am I and why? | 28, 29, 32 |
| 2026-11-14 | Which of the files you made go where, and how do I avoid scrolling past them? | 31 |
| 2026-11-15 | Where do I find the three new rules to paste? Are the instructions in the SOP the full instructions? | 25 |
| 2026-11-15 | Can you scan the projects to confirm they hold what they need? | 25, 31 |
| 2026-11-15 | Does it matter that I deleted the uploads before saving the handovers? | 31 (Context files cannot be downloaded) |
| 2026-11-15 | What "yes" are you waiting for, and how do I give it? | 29 |

## Glossary

| Term | Meaning | Entry |
| --- | --- | --- |
| ADR | A file recording one big decision and why | 27 |
| API | The menu of requests a server accepts | 7 |
| Apps Script | Google's programs that run inside Sheets, Gmail and Drive | 5 |
| Artifact | A page or document Claude saves in your account | 26 |
| Back end | The behind-the-scenes part: server, data, rules | 2 |
| Branch | A separate copy to try a change on | 16 |
| Brief | Why an app exists, for whom, and what it will not do | 27 |
| Browser storage | Private space on one device's browser for a website's information | 10 |
| Build script | A program that assembles the finished app from source files | 23 |
| Cache | Copies of the app's files kept on the device | 12 |
| Cache version | The name that tells devices to fetch new files | 12 |
| CHANGELOG | The list of releases and what changed | 18 |
| Checksum | A fingerprint of a file's exact contents | 20 |
| Code | Instructions the app follows | 9 |
| Commit | One saved change, with a message | 15 |
| Context files | Files and links Claude reads in every chat of a project | 25 |
| CSS | The language for an app's look | 1 |
| Data | Information the code works with | 9 |
| Database | Organised, stored information an app reads and writes | 4 |
| Deployment | The running copy of the code | 17 |
| Drift | Two copies of the same thing no longer matching | 20 |
| Front end | What people see and tap | 2 |
| Git | The system that tracks every change to files | 14 |
| GitHub | The website that stores repositories | 14 |
| GitHub Pages | Free hosting from a GitHub repository | 6 |
| Hash | A fingerprint made from text | 22 |
| Hosting | Putting files where the internet can reach them | 6 |
| HTML | The language for an app's structure | 1 |
| Instructions | A project's standing rules for Claude | 25 |
| JavaScript | The language for an app's behaviour | 1 |
| JSON | A plain-text way of writing labelled information | 8 |
| Main | The branch that is live | 16 |
| Manifest | A small file giving an installable app's name and icon | 13 |
| Memory | What Claude has learned in a project's chats | 25 |
| Offline queue | Changes saved on the device, waiting to be sent | 11 |
| Phone key | The secret part of Tour Timer's phone links | 22 |
| Playwright | A tool that drives a browser for tests | 24 |
| Public repository | A repository anyone can read | 21 |
| Pull request | A proposal to join a branch into main, for review | 16 |
| PWA | An installable web app that works offline | 13 |
| Quota | A daily usage limit set by a service | 5 |
| Regression | Something that worked and broke after a change | 24 |
| Release | A named, recorded version of the whole app | 18 |
| Repository (repo) | The folder of an app's files, with full history | 14 |
| Request | One message to a server | 7 |
| Rollback | Going back to the last version that worked | 19 |
| Rotate | Replace a secret after it has been exposed | 22 |
| Salt | A random value mixed in before hashing | 22 |
| SemVer | Version numbers in the form MAJOR.MINOR.PATCH | 18 |
| Server | A program that holds information several devices share | 3 |
| Service worker | A helper file that lets pages open without signal | 12 |
| Static page | A page that is just files, with no server code of its own | 6 |
| Sync | Sending saved changes and receiving others' changes; in a Claude project, fetching the latest repo files | 11, 31 |
| Sync now | The Claude project button that fetches the latest GitHub files | 31 |
| Tag | A permanent label on one commit | 18 |
| Trigger | An instruction to run a script on a schedule | 5 |
| TypeScript | JavaScript with built-in checking for mistakes | SOP: Choosing languages |
| Web app | An app that runs in a browser | 1 |
