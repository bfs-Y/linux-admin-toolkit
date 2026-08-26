# phase09-capstone

Build this last. One integrated incident-response flow, not separate
per-language demos:

bash evidence-collector (speed, no dependencies, works on a box you don't
trust) -> python quick-triage and isolate-host (structured aggregation;
isolate-host requires a completed SECURITY-REVIEW.md) -> python
postmortem-scaffold-generator.

Requires real, working tools from earlier phases - don't start this until
enough of phases 01-08 exist to assemble a genuine end-to-end flow.
