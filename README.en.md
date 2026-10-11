# Agent-Friendly Mark

[日本語](README.md)

A mark for software that is built so AI agents can use it easily.
It is not a strict standard. It states that "my personal projects are built to these criteria."

## Concept

- The mark exists for LLMs (agents) more than for people.
- It goes in the README as a badge.
- The badge links to the repository's `AGENTS.md`.
  - For people it is a sign. For an AI it points to the manual.
- It is the shared mark of the SIL series.
- There are no levels or scores. There is one mark.

## Criteria

An agent with no prior knowledge, given only the repository, should be able to do the following.

- Learn from `AGENTS.md` where to start, a minimal example, and how to check the result.
- Finish a typical task from start to end without help from a person.
- Confirm by itself that the result is correct. A successful exit code with output that differs from what was expected counts as unfinished.
- Learn how to use the software without analyzing the source.
- When something fails, tell from the error message what to do next, and recover without help.

The criteria were decided jointly by the two agents that use the software, Claude and Codex (2026-10-04, Claude Opus 5.5 and Codex gpt-6.1-sol high).

## How to check

Whether a project meets the criteria is checked by having agents actually use it. Look at the action log, not at the agent's impressions.

1. Pick 2 or 3 typical tasks for the software, and the expected result of each.
2. Give Claude and Codex the same version of the repository and the same task instructions, each in a separate new conversation. Do not tell them the steps.
3. Include one safe failure, such as invalid input, and see whether the agent recovers.
4. Find where the agent got stuck in the log, and fix the software or `AGENTS.md`.

What to look at in the log:

- Whether the task was finished and the result was correct
- How many times a person helped
- Whether the agent stalled (including stopping at an interactive prompt)
- Whether it recovered from a failure
- Whether it had to analyze the source to learn how to use the software
- Failed commands, repeated attempts at the same thing, and guessed commands or options that do not exist (these show where to fix)

Failures of the execution environment and obvious mistakes on the agent's side do not count as problems of the software.

Record each check in 1 or 2 lines at the end of the repository's `AGENTS.md`: when, with which models, and which tasks.

## Guidelines for building

These are means of reaching the criteria.

- Every operation is available as a command (CLI).
- Commands run without interaction (flags such as `--yes` are enough).
- Results can be output in a machine-readable form such as JSON.
- The current state can be read with a command (such as `status --json`). No state exists that can only be learned by looking at the screen.
- A change can be tried before it is made (such as `--dry-run`).
- The same command gives the same result.
- Errors state the cause and how to fix it.
- After a failure, it is clear what has already been changed.

## AGENTS.md

See [AGENTS.template.en.md](AGENTS.template.en.md) for what to write.

## Badge

There is one badge: [badges/badge.svg](badges/badge.svg). To check how it looks, open `badges/preview.html` in a browser.

- Dark navy with `>_` (the terminal prompt) and the text "agent-friendly"
- A silver band at the right end, matching the silver of the SIL series

How to put it in a README (the link points to the repository's AGENTS.md):

```markdown
[![agent-friendly](badges/badge.svg)](AGENTS.md)
```

## License

[CC0 1.0](LICENSE). Anyone may use the criteria, the `AGENTS.md` template, and the badge without asking for permission and without credit.
