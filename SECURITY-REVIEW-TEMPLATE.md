# Security Review Template
 
Copy this into `SECURITY-REVIEW.md` inside any tool folder flagged as
requiring review in `ROADMAP.md`. If the tool has both a bash and a Python
implementation, answer all five questions **independently for each** — a
review pass on one implementation never grandfathers the other.
 
**Required for**: any tool whose normal operation is destructive or
irreversible — deletes, overwrites, disables, locks out, isolates, or
modifies live state in a way that isn't trivially undone by re-running the
tool.
 
**Not required for**: tools that only read, report, or alert.
 
---
 
## [Implementation: bash / python]
 
**1. What's the worst thing this tool can do if run with wrong arguments,
wrong user, or against the wrong host?**
 
_(answer here)_
 
**2. Does it need root, or one specific capability/sudo rule — and is that
scoped as narrowly as possible?**
 
_(answer here)_
 
**3. Is `--dry-run` output verified to match real-run behavior, with a test
that would fail if they diverged?**
 
_(answer here)_
 
**4. What's the blast radius if this tool itself is compromised or
trojaned?**
 
_(answer here)_
 
**5. Who is authorized to run it, and is that enforced (permissions,
sudoers, a check inside the tool) or only documented?**
 
_(answer here)_
 
---
 
Repeat the block above under a second `## [Implementation: python / bash]`
heading if the tool has both.
