# Read OffCKB Startup Output

Use this page when `offckb node` prints a lot of output and you are not sure whether the node started successfully.

## Validation Scope

The repository-maintained startup observations were recorded on macOS arm64.
If your output is different on another operating system, open a `Cold Start Guide Test` issue and include the relevant lines.

## The Main Rule

Do not decide from the first alarming line.
Watch whether the process keeps running and whether it reaches a stable startup signal.

## Success Signal

The repository-validated success signal is:

```text
CKB devnet RPC Proxy server running on http://127.0.0.1:28114
```

PASS:

- the process keeps running
- the startup signal appears
- local RPC works from another terminal

FAIL:

- the process exits
- no startup signal appears
- local RPC cannot connect while the node terminal is still running

## Common Non-Final Output

The first run may show missing-binary or download-related output before it recovers.
That output is not enough by itself to mark the step failed.

Wait for one of these outcomes:

- the success signal appears
- the process exits with a final error
- the output stops and no prompt returns, meaning the process may still be running

## Terminal Setup

Use two terminals:

Terminal 1:

```bash
offckb node
```

Terminal 2:

```bash
echo '{"id":2,"jsonrpc":"2.0","method":"get_tip_block_number","params":[]}' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

Expected Terminal 2 output:

```json
{"jsonrpc":"2.0","result":"0x0","id":2}
```

The exact `result` value can differ.

## What To Paste Into An Issue

Paste:

- operating system
- command run
- the first 10 to 20 relevant output lines
- the final 10 to 20 output lines before the process stopped or before you got stuck
- whether the process was still running
- the local RPC command and output from Terminal 2

Do not paste personal home paths or usernames.
Replace them with `$HOME` and `<local-user>`.

## Next Step

- If the startup signal appears, return to [Path B. Local Node](../branching-paths.md#path-b-local-node).
- If the process exits, use [First-run binary download confusion](../troubleshooting-matrix.md#first-run-binary-download-confusion) or [Warning-looking startup output](../troubleshooting-matrix.md#warning-looking-startup-output).
- If local RPC fails while the node is running, use [Local node process stopped](../troubleshooting-matrix.md#local-node-process-stopped).
