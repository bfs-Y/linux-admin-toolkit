# linux-admin-toolkit

A Linux admin/DevOps tooling repo. Every tool that genuinely warrants both a
bash and a Python implementation carries both, side by side, in its own
folder. Tools that only make sense in one language stay single-language —
the choice is justified per tool, in that tool's own `README.md`, not
asserted once here.

**Why two languages in one repo, not two repos:** the bash version favors
fast, dependency-free scripts for domains where shell's guarantees
(idempotency, clear exit codes, `--dry-run`) are enough. The Python version
exists for domains where real typing, real exceptions, structured data, and
a test suite actually earn their cost — API clients, multi-host
orchestration, anything doing non-trivial parsing or state tracking.
Building both, on the same tools where it's warranted, is the clearest way
to demonstrate *when* to reach for which — see `notes/design-decisions.md`
for the per-tool reasoning as it's written.

## Status

**Currently in planning/scaffold stage.** The structure below is fully
specified in `ROADMAP.md`; no tool implementation has started yet.
`phase00-toolkit-meta` is built first — every later tool depends on its
shared CLI framework, logging config, and test harness — followed by
phases 01-08 in any order, with `phase09-capstone` built last, once enough
real tools exist to assemble into one incident-response flow.

## Structure

    linux-admin-toolkit/
    +-- README.md                      -- this file
    +-- ROADMAP.md                     -- full tool list, status, build order
    +-- STANDARDS.md                   -- the non-negotiable contract every tool follows
    +-- SECURITY-REVIEW-TEMPLATE.md    -- required for any destructive/irreversible tool
    +-- notes/                         -- cross-cutting design notes and incidents
    +-- pyproject.toml                 -- shared config for all python/ subtrees
    |
    +-- phase00-toolkit-meta/          -- BUILD FIRST
    +-- phase01-monitoring-and-alerting/
    +-- phase02-backup-and-recovery/
    +-- phase03-user-and-access-management/
    +-- phase04-log-analysis-and-forensics/
    +-- phase05-system-audit-and-compliance/
    +-- phase06-deployment-and-automation/
    +-- phase07-incident-response-tooling/
    +-- phase08-performance-and-capacity/
    +-- phase09-capstone/               -- BUILD LAST

## Per-tool layout

Dual-implementation (most tools):

    tool-name/
    +-- README.md              -- what it does, why both versions exist
    +-- SECURITY-REVIEW.md     -- present ONLY if flagged in ROADMAP.md
    +-- bash/
    |   +-- tool-name.sh
    |   +-- break/ fix/ harden/
    |   +-- test-log.md
    |   +-- postmortem.md
    +-- python/
    |   +-- src/ tests/
    |   +-- break/ fix/ harden/
    |   +-- test-log.md
    |   +-- postmortem.md

Single-language tools use the same shape minus the other language's folder,
with the README stating explicitly why.

## Rules that apply to every tool, no exceptions

- Idempotent, or explicitly refuses double-execution.
- `--dry-run` for anything destructive.
- Meaningful, documented exit/return codes.
- Logs what it did, not just that it ran.
- Validates preconditions before acting.
- A `SECURITY-REVIEW.md` is required for any tool whose normal operation is
  destructive or irreversible -- see `ROADMAP.md` for which tools are flagged
  and `SECURITY-REVIEW-TEMPLATE.md` for the five questions each review
  answers, independently, per implementation.

See `STANDARDS.md` for the full bash and Python contracts.
