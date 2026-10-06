# 003: Tokens that last 15 minutes

*Locked 2026-10-07, planning session 1.*

**Decision:** after the password check, the server gives a signed token that lasts 15 minutes.

**Alternative considered:** tokens that last 30 days.

**Why:** "a stolen token stops working after 15 minutes."

**Accepted cost:** tokens expire during a gym session, so the app must "keep her climb, ask her to log in again, then save it."
