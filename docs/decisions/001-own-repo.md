# 001: The lab lives in its own repo

*Locked 2026-10-07, planning session 1.*

**Decision:** SaaS Support Lab lives in its own repo, cloned from `climb-tracker`.

**Alternative considered:** building it inside `climb-tracker`.

**Why:** I predicted that a planted expired-token bug in `climb-tracker` would answer 401 at the gym and lose my real climb.
In my words: "so planted bugs never break the app I use at the gym."
