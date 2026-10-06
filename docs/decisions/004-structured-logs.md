# 004: Structured logs

*Locked 2026-10-07, planning session 1.*

**Decision:** one JSON line per request with `reqId`, `user` and `status`, replacing the plain-text request lines.

**Why:** for a ticket like "Bea says Log failed around 18:20", I'd search by user first, "since it narrows to Bea's requests."
Tickets need real log excerpts as proof.
