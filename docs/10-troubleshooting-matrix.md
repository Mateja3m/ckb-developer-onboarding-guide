# 10. Troubleshooting Matrix

## Goal

Provide a fast issue-to-cause-to-next-action lookup table for the early CKB onboarding flow.

## How To Use This Page

When something goes wrong:

1. Match the symptom as closely as possible.
2. Pick the simplest likely cause first.
3. Run the suggested next action before changing multiple things at once.

This matrix is intentionally limited to early onboarding problems.

## Matrix

| Symptom | Likely Cause | What To Check First | Next Action |
| --- | --- | --- | --- |
| `command not found` | Missing tool or shell path issue | Which exact command failed | Return to prerequisites and confirm the tool is installed and visible in the current shell |
| `curl: (6) Could not resolve host` | DNS or connectivity issue | Whether the failure is target-specific or general | Recheck HTTPS connectivity using the environment setup flow and record the exact hostname |
| `offckb node` shows a missing-binary message on first run | First-run binary is not present yet | Whether the process continues into download and startup | Keep watching for recovery instead of assuming the first line is final failure |
| `offckb node` prints a warning log | Startup warning or noisy output | Whether the process still reaches the startup signal | Treat the step as successful only if the node reaches a stable running state |
| No valid JSON-RPC response from local request | Node is not running, wrong endpoint, or malformed request | Whether the node process is still active and whether the request used the validated format | Restart from the validated node flow and retry the exact validated request |
| Browser says `POST or OPTIONS is required` | Wrong HTTP method | How the endpoint was tested | Stop using a browser visit as the RPC test and switch back to the documented JSON-RPC POST request |
| RPC works on one local endpoint but another step mentions a different one | Endpoint confusion between local services | Which exact endpoint succeeded on your machine | Record the successful endpoint and avoid substituting values casually |
| `get_tip_block_number` returns a low value | Early local chain state | Whether the response structure is valid JSON-RPC | Treat a valid JSON-RPC body as success even if the tip height is low |
| Tool exists but behaves differently in a new terminal session | Session or environment mismatch | Whether the command works in the same shell where setup was performed | Reconfirm tool availability in the actual shell session you are using for onboarding |
| One successful step makes later failures more confusing | Premature assumption that the whole setup is done | Which part of the flow was actually validated | Reset the scope of the problem and identify the last clearly successful checkpoint |

## Verification

You are using this matrix correctly if:

- you pick one symptom at a time
- you avoid changing multiple variables at once
- you record the exact failing command or output before improvising a fix

## Expected Output

At the end of this page, you should have:

- a faster way to classify common onboarding failures
- a simpler rule for what to check first
- less trial-and-error during early debugging
