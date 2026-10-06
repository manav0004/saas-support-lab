# Progress

## Now
Session 1 (2026-10-07): planning done. 4 decisions + MVP locked (`plan.md`, `project.md`). Repo cloned from climb-tracker (41 commits); `origin` still points at the local climb-tracker folder.
NEXT: 1.1, the lab's own GitHub repo (point `origin` at it, push). Before it: read the new learning files and the decision-record drafts, then commit them myself after `git diff`.
Warm-up: the shaky HTTP method ↔ SQL link (below), asked as "in Postman, which method adds a climb, which SQL runs, which status comes back?"

## Solid (did it correctly) — carried from Climb Tracker
- Forms, `preventDefault`, `Number()` for HTML text, a server-side 400 check placed above the INSERT.
- `fetch` + JSON body; `try`/`catch` + `response.ok`; dates with `toDateString()`; redraw the list from the data.
- `.gitignore`, `.env`, `process.env`; a parameterized INSERT with `$1`–`$6`; deployed on Render myself.

## Planning evidence (session 1, decisions only, no code yet)
- Separate environments: predicted 401 + a lost gym climb if the bug lived in climb-tracker.
- 404 vs 403: chose "not allowed" first; after a 3-line trace found it leaks which accounts exist; applied 403 to `/admin/users` myself.
- Token expiry: "a stolen token stops working after 15 minutes"; expired mid-session → keep the climb, re-login, save.
- Logs: search by user first. MVP: mapped 4 failures to features; missed the coach link; logs stay because tickets need proof.
- Said "lock it" once before checking the list; the follow-up question was answered right.

## Shaky (bring back one per session) — carried from Climb Tracker
- HTTP method ↔ action ↔ SQL (POST = add = INSERT, 201; GET = read = SELECT).
- Data object fields vs page elements; `undefined` vs empty (`[]`, `{}`).
- Comparison symbols (`=` assigns, `===`/`!==` compare); says "should work" untested.
- SQL is text: values go through `$1` + the array, never a JS variable inside the query.
- Timing / `await`: "not called yet" vs "data not there yet".

## Parking lot
- Password reset · Stay logged in (no re-entering the password) · Edit a climb · Coach comments · Rate limits (429)
