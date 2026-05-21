# Common Errors And Remediation

## Goal

Document the beginner-facing onboarding failures that are most likely to appear in this repository's CKB flow, using validated observations and clearly scoped beginner remediation steps.

## Requirements

Before using this page, complete:

- [Environment Setup](environment-setup.md)
- [CKB Node Setup](ckb-node-setup.md)
- [RPC Basics](rpc-setup.md)

This page focuses on early onboarding failures, not advanced debugging.

## 1. `command not found`

### Symptom

A required local tool such as `node`, `npm`, `git`, `curl`, or `offckb` is not available in the current shell.

### Likely Cause

- the tool is not installed
- the tool is installed but not visible in the current shell
- the current session needs to be restarted after installation

### Remediation

1. Return to the prerequisites page and rerun the exact tool checks.
2. Confirm whether the failure affects one tool or multiple tools.
3. If the tool was just installed, reopen the terminal and test again.
4. Do not continue into CKB-specific setup until the missing tool issue is resolved.

## 2. `curl: (6) Could not resolve host`

### Symptom

The terminal cannot resolve a hostname during a network check.

### Likely Cause

- DNS resolution problem
- VPN or proxy issue
- firewall restriction
- target-specific connectivity problem

### Remediation

1. Confirm whether the failure is specific to one hostname or affects general HTTPS access.
2. Use the environment setup guidance that already validated a real HTTPS target.
3. Do not treat this automatically as a CKB-specific node or RPC failure.
4. Record the exact hostname and exact `curl` output before changing anything else.

## 3. Missing-Binary Message During `offckb node`

### Symptom

The first node startup appears to fail because a required CKB binary is missing.

### Likely Cause

On the validation machine, the tool recovered automatically by downloading the required binary on first run.

### Remediation

1. Keep reading the output instead of treating the first alarming line as the final result.
2. Check whether the process continues into download, install, and startup messages.
3. Only treat the step as failed if the flow stops without reaching a stable startup signal.

## 4. Warning-Looking Startup Output

### Symptom

The node prints a warning-style log during startup.

### Likely Cause

Not every warning-style line is a hard failure. The validation notes already recorded a warning log before a successful startup signal.

### Remediation

1. Look for the final startup signal before deciding the step failed.
2. Keep the full output in your notes.
3. Distinguish between "unexpected but recovered" and "process exited without success."

## 5. RPC Endpoint Opened In A Browser

### Symptom

The developer opens the RPC endpoint directly and sees:

`Used HTTP Method is not allowed. POST or OPTIONS is required`

### Likely Cause

The endpoint was tested with the wrong HTTP method.

### Remediation

1. Do not use a browser visit as the RPC validation step.
2. Return to the validated JSON-RPC POST example from the RPC page.
3. Treat this as a request-method mismatch, not immediate proof that the node is broken.

## 6. RPC Request Fails Because The Node Is Not Running

### Symptom

The RPC request does not return the expected JSON-RPC response because the local process is no longer active.

### Likely Cause

- the node was stopped accidentally
- the developer reused the same terminal and interrupted the process
- the workflow was not split between a node terminal and an RPC terminal

### Remediation

1. Confirm that the node process is still running in the original terminal.
2. Restart the node if necessary using the validated local flow.
3. Repeat the RPC request only after the local startup signal returns.

## 7. Confusion About `localhost:8114` Versus `127.0.0.1:28114`

### Symptom

The node startup mentions one endpoint, while the documented RPC example uses another.

### Likely Cause

The repository already observed that both local-looking endpoints can respond successfully, which makes early onboarding confusing if the beginner expects one single value everywhere.

### Remediation

1. Record the exact endpoint that worked on your machine.
2. Do not casually swap ports unless you are validating them deliberately.
3. Use the validated request flow first, then compare notes afterward.

## 8. Low Tip Block Number Looks Like Failure

### Symptom

The RPC response returns a low value such as `0x0`, and the developer assumes the step failed.

### Likely Cause

The beginner is reading the block height as the success signal instead of reading the valid JSON-RPC response structure as the success signal.

### Remediation

1. Check whether the response includes a valid JSON-RPC structure.
2. Confirm that the request returned `"jsonrpc":"2.0"` and a `"result"` field.
3. Treat a low value as possible early chain state, not automatic failure.

## Verification

You are aligned with this page if you can do three things:

- name the likely category of a failure before changing commands
- describe the difference between a tooling problem and a node/RPC problem
- explain which issues in this repository were already observed in local validation

## Expected Output

At the end of this page, you should have:

- a clearer map of likely onboarding failures
- a short remediation path for each one
- less temptation to guess blindly when the first step goes wrong
