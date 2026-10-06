# SaaS Support Lab — Project Record

> Context file: the idea, the MVP and the history. The tutoring rules are in `CLAUDE.md`, and
> sessions start from `learning/progress.md`. The build plan is `learning/plan.md`.

## Who I am

- **Background:** HTML and CSS websites, some Python, a Unity (C#) platformer. Learned JavaScript, Node,
  Express and PostgreSQL by building Climb Tracker (sessions 1–11, Sept–Oct 2026; its full record is in that repo).
- **Goal:** a job in support or application support in Barcelona. This lab is my main evidence for it.
- **How I learn best:** fast with ideas, limited working memory (ADHD). One small step per message,
  depth over volume, analogies to Unity, Python and Climb Tracker, every step ends with something working.
  The full rules are in `CLAUDE.md`.

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
