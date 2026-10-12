# SaaS Support Lab: Build Plan

> Learning comes first, not speed. Each task is one session and ends with something I can see working.
> The finish line: I can explain the full trip of a request (login, token, auth and role checks, route, SQL,
> log line, reply) and work an unseen failure live, from customer report to fix.

## 🔒 Locked decisions (session 1, 2026-10-07)

Each was explained in my own words before locking. Climb Tracker's five decisions (JavaScript, plain
HTML/CSS/JS, Node + Express, PostgreSQL, Render + Neon) carry over unchanged.

| # | Decision | Choice | Why (in my words, cleaned up) |
|---|---|---|---|
| 1 | Where the lab lives | Its own repo, `saas-support-lab`, cloned from `climb-tracker` | "So planted bugs never break the app I use at the gym." |
| 2 | Who uses it | Three roles: climber (owns their climbs), coach (reads linked climbers only), admin (manages accounts) | "Adding or deleting is Bea's job." |
| 2b | How the server refuses | **404** when admitting the thing exists would leak private data (Carla's climbs); **403** when it's public knowledge (`/admin/users`) | "Not allowed" told a stranger that climbers 1 and 3 exist; "doesn't exist" is safer. "403, since everyone already knows the admin page exists." |
| 3 | How users log in | Password, then a signed token that lasts **15 minutes**, sent in the `Authorization: Bearer` header | "A stolen token stops working after 15 minutes." When it expires mid-session: "keep her climb, ask her to log in again, then save it." |
| 4 | Logs | One JSON line per request: `time`, `reqId`, `user`, `method`, `url`, `status`, `ms`. The `reqId` is shown in error messages | Search a ticket by `user` first ("it narrows to Bea's requests"), then time, then status; a `reqId` in the ticket jumps straight to the line. |

## 🧱 The sections

### 1. The lab's own home
- [x] **1.1 Its own GitHub repo.** Create `saas-support-lab` on GitHub and point `origin` at it (it points at the local `climb-tracker` now). ✅ `git push` puts the 42 commits on GitHub. *(Done 2026-10-12: github.com/manav0004/saas-support-lab.)*
- [ ] **1.2 Its own database.** A new Neon database with the `climbs` table, and a `.env` for the lab. ✅ A climb logged in the lab doesn't appear in Climb Tracker.
- [ ] **1.3 Its own live URL.** A new Render service for the lab. ✅ The lab and Climb Tracker run side by side at two URLs.

### 2. Users and passwords
- [ ] **2.1 Postman.** Send my existing `GET` / `POST /api/climbs` from Postman instead of the page. ✅ A saved request returns my climbs, and a bad effort gets the 400.
- [ ] **2.2 A `users` table and register.** `POST /api/register` stores the email and a *hashed* password. ✅ In Neon, the password column holds a hash, never the password.
- [ ] **2.3 Login checks the password.** `POST /api/login` compares the password with the hash. ✅ Right password → 200, wrong → 401, and both show in the terminal.

### 3. Tokens: the server knows who you are
- [ ] **3.1 Login hands out a token.** ✅ Postman shows a token with a 15-minute expiry.
- [ ] **3.2 A middleware checks the token** before the climbs routes run. ✅ No token → 401, a token edited by hand → 401, a valid token → my climbs.
- [ ] **3.3 Climbs belong to a user.** A `user_id` column, and every query filters by it. ✅ Two accounts each see only their own climbs.
- [ ] **3.4 Expiry.** ✅ After 15 minutes (or a 1-minute test setting) the same request gets 401.

### 4. Roles and coaches
- [ ] **4.1 Roles.** A `role` column, and an admin-only `GET /api/admin/users`. ✅ Bea gets 403, the admin gets the list.
- [ ] **4.2 Coach links.** A `coach_links` table and a way for the admin to link a coach to a climber. ✅ The link shows in Neon.
- [ ] **4.3 Coaches read linked climbers.** ✅ Marc reads Bea's climbs, gets 404 for Carla's, and can't add or delete either.

### 5. The page logs in
- [ ] **5.1 A login form**, and the page sends the token with every `fetch`. ✅ I log in on my phone and see only my climbs.
- [ ] **5.2 The expired-token test (decision 3).** ✅ A climb typed after expiry is kept, I'm asked to log in, and it's saved.

### 6. Structured logs
- [ ] **6.1 JSON log lines with `reqId`**, replacing the plain logger. ✅ Every request prints one JSON line.
- [ ] **6.2 `reqId` in error replies and on the page.** ✅ Given a `reqId` from the screen, I find its line in Render's logs.

### 7. Postman tests
- [ ] **7.1 A collection with tests** for every route and its status codes. ✅ One run, all green; a planted bug turns one red.

### 8. Break it on purpose, and work it like support
One failure per session: plant it (a commit), receive it as a customer report, reproduce, read the logs,
find the cause, fix (a second commit), write the reply and the ticket with the real log excerpt.
✅ Each session ends with one finished ticket in `docs/support/`. Over the section: 10 tickets, 3 incident
reports, 3 runbooks, and the known-issues page.

### 9. The portfolio
- [ ] **9.1 README** that a recruiter can read in 2 minutes, linking the live URL, the tickets and the journal.
- [ ] **9.2 The 10-minute walkthrough** of one incident, from report to fix, recorded.

## 🎯 The final exam

Without notes: the full trip of a request, from login to the token, the auth and role checks, the route,
the SQL, the log line and the reply. Then one failure I haven't seen before, live, from customer report to fix.
