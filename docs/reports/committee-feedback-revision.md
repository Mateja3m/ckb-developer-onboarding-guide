# Committee Feedback Revision Report

## Summary

The guide was restructured to match the committee request:

`Quick Start -> Branching Paths -> Troubleshooting Matrix -> FAQ -> How to Verify`

The main path is now shorter, action-first, and focused on helping a beginner reach one verified CKB JSON-RPC response.

## What Was Changed

- `README.md` now shows only the required beginner path and success signals.
- `docs/quick-start.md` is the shortest path using public RPC first.
- `docs/branching-paths.md` separates the guide into Path A public RPC, Path B local node, and Path C full local check.
- `docs/troubleshooting-matrix.md` maps common failures to cause, fix, verification command, and related section.
- `docs/faq.md` gives short answers and points readers back to the right guide section.
- `docs/how-to-verify.md` provides the reproducible checklist: environment, steps, expected output, pass/fail criteria, and evidence location.

## What Was Reduced Or Moved

- Removed milestone/status wording from the main path.
- Removed the old numbered document sequence from the README.
- Moved longer background, concept, and support pages into `docs/reference/`.
- Kept validation material in `docs/validation/` as evidence only, not as the reader-facing guide.
- Preserved previous reports in `docs/reports/`.

## Verification Evidence

Current evidence is located in:

- `docs/validation/environment-validation-findings.md`
- `docs/validation/ckb-node-and-rpc-validation-findings.md`
- `docs/how-to-verify.md`
- `validation-logs/2026-05-11-how-to-verify-rerun.md`

Fresh reruns can be recorded in:

- `validation-logs/` using `docs/validation/validation-log-template.md`

## Feedback Mapping

| Committee feedback | Revision made |
| --- | --- |
| Too much low-information-density content | Reduced the main path to commands, expected output, pass/fail criteria, and next links |
| Unclear structure | Rebuilt navigation around the requested five-part flow |
| Missing shortest path and branching paths | Added public RPC first, then local node and full local paths |
| Not beginner-friendly enough | Added clear prerequisites, success criteria, and failure destinations |
| Missing verification evidence | Added `docs/how-to-verify.md` and linked existing validation evidence |
| Work-log style content | Moved background/report-style material out of the main path |

## Review Note

No previous reports were deleted.
The old supporting material is preserved in `docs/reference/`, but it is no longer the required onboarding path.
