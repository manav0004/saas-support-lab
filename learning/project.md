# SaaS Support Lab — Project Record

> Context file: the idea, the MVP and the history. The tutoring rules are in `CLAUDE.md`, and
> sessions start from `learning/progress.md`. The build plan is `learning/plan.md`.

## Who I am

- **Background:** HTML and CSS websites, some Python, a Unity (C#) platformer. Learned JavaScript, Node,
  Express and PostgreSQL by building Climb Tracker (sessions 1–11, Sept–Oct 2026; its full record is in that repo).
- **Goal:** get out of retail into application/SaaS support in Barcelona, on a path toward application
  security. This lab is my main evidence for it. The full reasoning is in the next section.
- **How I learn best:** fast with ideas, limited working memory (ADHD). One small step per message,
  depth over volume, analogies to Unity, Python and Climb Tracker, every step ends with something working.
  The full rules are in `CLAUDE.md`.

## 🧭 Career goal and why this project (updated 2026-10-07)

Written so an outside reviewer (e.g. claude-council via `--file=learning/project.md`) has the context with nothing else.

> **Current phase — October 2026 is a learning month, not an applying month.** No job applications this month.
> All time goes to learning: building this lab. Applications start after October. Any advice should respect
> this and not push me to apply now.

- **Where I am now:** working in retail in the Barcelona area, with a non-IT CFGS (vocational higher diploma).
  Self-taught: JavaScript, Node, Express, PostgreSQL, HTML/CSS, some Python, C# (Unity), Linux basics. Good English.
- **The real objective:** not "the easiest tech job I can get", but the best way out of retail that keeps a path
  to technically interesting, hard-to-commoditize work paying €35k+.
- **Targets, in order:**
  1. **Primary:** application/SaaS support (also product support, onboarding, technical support). The most realistic
     first job that still uses my programming.
  2. **High-value:** junior application security (AppSec): secure code review, static analysis, working with developers.
     Junior listings ask for programming, which most security beginners lack and I have.
  3. **Specialization, long-term:** pentesting, web and API first. Built in parallel, not my first job.
  4. **Commercial backup:** ERP / business systems support.
  5. **Escape hatch only:** generic IT helpdesk / M365.
- **Strategy:** one learning month (October 2026), then apply to tech jobs while building security skills
  alongside. Never "study security for a year, then apply": a long study-first plan is the failure mode I want
  to avoid, so the learning-only phase is capped at this month. The first job doesn't need to be in security;
  a year of app support (production apps, APIs, databases, logs, incidents) plus a security portfolio makes a
  junior AppSec application believable.
- **Time split from November 2026, for 6 months:** 40% applications and interviews · 30% security (networking →
  Linux → web security → Burp → OWASP Top 10) · 20% SQL, APIs, troubleshooting, ERP · 10% portfolio.
  October is 100% learning.
- **Certifications:** none bought yet. Fundamentals first; pick one practical cert (eJPT / PNPT / CPTS type) only
  if my target listings keep asking for it.

**Why this project fits both tracks:** a support lab proves the primary target (tickets, logs, incidents,
runbooks). Its login, roles and access rules are exactly where web vulnerabilities live (broken access control,
IDOR, auth flaws), so the same code is the bridge to AppSec: I understand *why* a flaw exists in code I wrote,
not just how to point a tool at it.

**Open question (not decided):** whether to add a security phase after the MVP: plant OWASP-style vulnerabilities
(IDOR, SQL injection, XSS…), exploit them with Burp, write up each finding (impact, evidence, fix), then fix them.
The locked MVP stays as it is until this is decided.

**Source and caveat:** this strategy came from a review with an outside AI consultant against Barcelona job
listings (Oct 2026). Its market claims (e.g. junior AppSec listings asking for Python/JS/C#, junior pentest
listings valuing Burp, CTF write-ups and eJPT/PNPT) are its reading of those listings and haven't been checked yet.

## The idea

Climb Tracker turned into a small multi-user SaaS: climbers log climbs, coaches follow their climbers,
admins manage accounts. Then I break it on purpose and work each failure the way a support agent would,
from the customer's report to the fix, the reply and the write-up.

**Why a separate repo (decision 1):** planted bugs never break the Climb Tracker I use at the gym.
This repo started as a clone of `climb-tracker` on 2026-10-07 (41 commits of history kept).

## ✅ In the MVP (locked 2026-10-07)

The smallest version in which every Career OS failure can happen (expired token, permission error,
bad input, missing record, 5xx), plus the evidence to prove it.

1. **Register and log in.** Passwords stored hashed. Login gives a signed token that lasts 15 minutes.
2. **Climbers add, read and delete only their own climbs.**
3. **An admin links a coach to a climber.** (The link is what lets the server tell Marc's climbers from Carla.)
4. **A coach reads only linked climbers' climbs.** Never adds or deletes ("adding or deleting is Bea's job").
5. **An admin page listing users.**
6. **JSON logs with a `reqId`**, also shown in error messages. Why it's in the MVP: tickets need real log excerpts as proof.
7. **Live on Render and Neon**, separate from Climb Tracker's.

**MVP is done when:** each of the five failures can be triggered on the live URL and found in the logs.

## 🎯 Career OS deliverables (the finish line)

- Live URL and public repo with a commit history over several weeks (bugs introduced and fixed in separate commits).
- Postman collection with tests.
- 10 tickets written as a support agent, 3 incident reports, 3 troubleshooting runbooks.
- A known-issues page and customer-facing replies.
- Proof: real log excerpts tied to each ticket, and a 10-minute recorded walkthrough of one incident from report to fix.

## 🅿️ Parking lot

- Password reset · Staying logged in without re-entering the password · Edit a climb · Coach comments · Rate limits (429)

## Progress log

- **Session 1 (2026-10-07): planning.** Locked 4 decisions and the MVP (see `plan.md`). Highlights: predicted that a planted
  expired-token bug in Climb Tracker would 401 and lose a real gym climb; first chose "not allowed" for a coach outside his
  climbers (helpful), then found from a 3-line trace that it tells a stranger which accounts exist, and switched to 404;
  applied the rule myself to `/admin/users` (403, it's public knowledge). Claude cloned the repo and wrote these files.
