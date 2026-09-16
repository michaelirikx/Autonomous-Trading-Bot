# Shared Truth Protocol

This directory is the single source of truth for ChatGPT, Grok, humans, and automation.

## Canonical files

1. `project.json` — current state, agent names, authority, invariants, and approved next step.
2. `decisions.json` — append-only accepted owner decisions.
3. `schemas/handoff.schema.json` — evidence-bearing exchange format.
4. Repository code, tests, and merged documentation — implementation evidence.

`AGENTS.md` and `GROK.md` are bootstrap instructions. They must point here and must not maintain a second copy of project truth.

## Required read sequence

Before analysis, planning, or edits:

1. Read `truth/project.json`.
2. Read `truth/decisions.json`.
3. Run `python scripts/validate_truth.py`.
4. Identify the current Git commit.
5. Treat anything not supported by these files or repository evidence as `UNVERIFIED`.

## Required write sequence

1. Work from the latest default branch.
2. Put changes on a branch and use a pull request.
3. For a truth change, append or supersede a decision, update `project.json`, and increment `truth_revision`.
4. Attach evidence: file path, test result, commit, or explicit owner decision.
5. Run the validator before handoff.
6. Do not claim a proposal or unmerged handoff is accepted truth.

## Conflict handling

If two sources disagree, apply `authority.precedence` from `project.json`. If ambiguity remains, stop and ask the owner. Safety-sensitive actions fail closed. Never resolve a conflict by inventing a value, weakening a gate, or silently rewriting history.

## Handoffs

A handoff transports evidence; it does not override canonical truth. Validate each handoff against `schemas/handoff.schema.json`. Every factual claim must be marked `CONFIRMED` with repository evidence or `UNVERIFIED`.

## Secrets

Never commit API keys, exchange credentials, webhook secrets, account identifiers, or private customer data. Store only variable names and setup guidance.
