# phase00-toolkit-meta

Build this phase entirely before anything else. Every later tool imports or
sources from here instead of reinventing argument parsing, logging setup,
or test scaffolding per tool.

- bash/ - tool-template.sh, self-test-harness.sh, changelog discipline notes.
- python/cli-framework/ - shared click/argparse base.
- python/logging-config/ - shared structured logging setup.
- python/test-harness/ - shared pytest fixtures/conftest.py.
- python/packaging/ - pyproject.toml entry_points so tools install as real CLI commands.
- python/ci-pipeline/ - ruff + mypy + pytest gate.

See root ROADMAP.md for status.
