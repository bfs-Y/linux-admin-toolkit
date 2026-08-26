# STANDARDS
 
Every tool in this repo, in either language, is held to these. A tool that
violates any applicable rule is not "done, needs polish later." It's not
done.
 
## Shared principles (every tool, either language)
 
1. Idempotent, or explicitly refuses double-execution with a clear error
   (e.g. a lockfile).
2. `--dry-run` (or equivalent preview mode) for anything destructive or
   state-changing.
3. Meaningful, documented exit/return codes — never ambiguous, never the
   reverse of what actually happened.
4. Logs what it did, not just that it ran — a stranger debugging at 3am
   should be able to reconstruct events from the log alone.
5. Validates its inputs and preconditions before doing anything
   irreversible.
6. Any tool flagged in `ROADMAP.md` as requiring a security review does not
   get marked "done" until `SECURITY-REVIEW.md` is filled out for that
   specific implementation (bash and python are reviewed independently —
   one passing never grandfathers the other).
 
## Bash-specific contract
 
- `set -euo pipefail` at the top of every script; any deliberate deviation
  is commented and justified inline.
- Double-execution guarded via a lockfile pattern where relevant.
- Writes are atomic: temp-file-then-rename, never a direct in-place write
  that could leave a partial file if interrupted.
- `--help` output exists and states what the script will change, before it
  changes anything.
- No unquoted variable expansion where word-splitting or globbing could
  cause unintended behavior.
 
## Python-specific contract
 
- Every public function is type-hinted; the repo's `mypy` config runs in
  strict mode and every tool must pass it clean.
- No bare `except:` and no unjustified broad `except Exception:` — catch by
  specific type, or justify the broad catch in a comment and re-raise/log
  with full context.
- `subprocess.run([...], shell=False)` with an explicit argument list —
  never a shell-interpolated string — unless the deviation is commented and
  justified.
- Uses the `logging` module, not bare `print`, for anything beyond direct
  CLI output meant for a human right now.
- At least one test in `tests/` proves the tool's most dangerous failure
  mode is handled correctly — not just a happy-path test.
- Exits via `sys.exit(n)` with a documented code; an uncaught exception is
  never the normal exit mechanism.
- Dependencies declared and pinned (or range-pinned) in `pyproject.toml` —
  never assumed to already exist in the ambient environment.
 
## The mandatory five-artifact cycle (per implementation)
 
1. **BREAK** — a specific, reproducible failure mode triggered deliberately
   (bad input, wrong user, double-execution, interrupted mid-write, missing
   dependency, etc.).
2. **FIX** — diagnosed and handled with evidence (logs/tracebacks) first,
   code changes second.
3. **HARDEN** — a durable pattern that prevents the whole class of failure,
   not just the specific instance found.
4. **TESTLOG** (`test-log.md`) — dated, close to a transcript: real commands,
   real output, never paraphrased.
5. **POSTMORTEM** (`postmortem.md`) — 3–5 sentences: real root cause, how it
   was found, one thing that now must never silently become false about
   this tool's environment or assumptions.
 
