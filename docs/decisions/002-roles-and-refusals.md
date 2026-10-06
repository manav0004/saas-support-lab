# 002: Three roles, and how the server refuses

*Locked 2026-10-07, planning session 1.*

**Decision:** three roles. Climbers own their climbs, coaches only read the climbers linked to them, admins manage accounts.
In my words: "adding or deleting is Bea's job."

**Refusals:** I first chose "not allowed" so a coach would know he needs access. Then I traced what a stranger learns
from "not allowed" versus "doesn't exist", and saw that "not allowed" reveals which accounts exist. So private data gets
a **404**, and public pages get a **403**: "everyone already knows the admin page exists."
