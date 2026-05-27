# Test The Guide

Use this process when someone new to CKB tries the guide.
The goal is to find where the documentation stops helping, not to prove that the author can explain the missing step live.

## Current Validation Scope

The repository-maintained validation logs were produced on macOS arm64.
Linux, Windows, and additional macOS machines should be treated as community reproduction targets until their results are recorded in [Community Reproduction Results](../validation/community-reproduction-results.md).

## Tester Profile

Prefer a tester who:

- has not contributed to this repository
- has no prior CKB setup experience
- can use a terminal
- can share command output from their own machine

## Test Rule

The tester should follow the main path without live hints:

1. [Quick Start](../quick-start.md)
2. [Branching Paths](../branching-paths.md)
3. [Troubleshooting Matrix](../troubleshooting-matrix.md)
4. [FAQ](../faq.md)
5. [How to Verify](../how-to-verify.md)

If an observer is present, the observer should stay silent until the tester stops or asks for help.
Where the tester stops is the next documentation problem to fix.

## What To Record

Record:

- operating system and version
- terminal shell if known
- on Windows, whether the tester used Windows PowerShell, PowerShell 7, Git Bash, or WSL
- prior CKB experience
- start time and end time
- path attempted: Path A, Path B, or Path C
- the first step that was unclear
- command output or error
- whether the tester could recover using the Troubleshooting Matrix

Do not publish personal home paths or usernames.
Replace them with `$HOME` or `<local-user>` before adding the result to the repo.

## Done Criteria

A cold-start test is useful when it answers:

- Did the tester reach the first JSON-RPC success signal?
- Did the tester know what success looked like?
- If the tester failed, did the guide point to the next useful action?
- Which sentence, command, or missing output example caused confusion?

## Where To Report

Use the GitHub issue template:

- `Cold Start Guide Test`

After the result is reviewed and sanitized, summarize it in:

- [Community Reproduction Results](../validation/community-reproduction-results.md)
