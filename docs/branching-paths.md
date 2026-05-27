# Branching Paths

Choose one path after [Quick Start](quick-start.md).

Current repository-maintained local-node validation was performed on macOS arm64.
If you are using another operating system, record the result through the `Cold Start Guide Test` issue template.
Windows PowerShell command variants are included for RPC requests, but Windows still needs community reproduction before it is treated as validated.

## Path A. Public RPC Only

Use this when you want the cheapest path.

Prerequisites:

- Quick Start prerequisites pass

Command:

```bash
echo '{"id":2,"jsonrpc":"2.0","method":"get_tip_block_number","params":[]}' \
| curl -H 'content-type: application/json' -d @- \
https://testnet.ckb.dev/rpc
```

On Windows PowerShell, run:

```powershell
$body = '{"id":2,"jsonrpc":"2.0","method":"get_tip_block_number","params":[]}'
curl.exe -H 'content-type: application/json' -d $body https://testnet.ckb.dev/rpc
```

PASS:

- response includes `"jsonrpc":"2.0"` and `"result"`

Example successful output:

```json
{"jsonrpc":"2.0","result":"0x123","id":2}
```

FAIL:

- use [Network or DNS failure](troubleshooting-matrix.md#network-or-dns-failure)
- use [Invalid JSON-RPC response](troubleshooting-matrix.md#invalid-json-rpc-response)

Evidence:

- record command, endpoint, and response in [How to Verify](how-to-verify.md)

## Path B. Local Node

Use this when you need local logs and local devnet control.
For the longer setup explanation, see [CKB Node Setup](reference/ckb-node-setup.md) and [RPC Basics](reference/rpc-setup.md).

Prerequisites:

- Path A passes
- npm can install global packages

Commands:

```bash
npm install -g @offckb/cli
offckb --help
offckb node
```

On Windows PowerShell, run the same install and startup commands.
If `offckb` is not recognized immediately after install, reopen PowerShell and rerun `offckb --help` before starting the node.

Keep `offckb node` running.
If the startup output is long or alarming, use [Read OffCKB Startup Output](how-to/read-offckb-startup-output.md) before deciding that the node failed.
In another terminal, run:

```bash
echo '{"id":2,"jsonrpc":"2.0","method":"get_tip_block_number","params":[]}' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

On Windows PowerShell, run:

```powershell
$body = '{"id":2,"jsonrpc":"2.0","method":"get_tip_block_number","params":[]}'
curl.exe -H 'content-type: application/json' -d $body http://localhost:8114
```

PASS:

- `offckb --help` works
- `offckb node` reports `CKB devnet RPC Proxy server running on http://127.0.0.1:28114`
- local RPC returns `"jsonrpc":"2.0"` and `"result"`

Example successful startup line:

```text
CKB devnet RPC Proxy server running on http://127.0.0.1:28114
```

Example successful local RPC output:

```json
{"jsonrpc":"2.0","result":"0x0","id":2}
```

FAIL:

- `offckb` fails: [offckb command missing](troubleshooting-matrix.md#offckb-command-missing)
- local RPC fails: [Local node process stopped](troubleshooting-matrix.md#local-node-process-stopped)
- response is unclear: [Invalid JSON-RPC response](troubleshooting-matrix.md#invalid-json-rpc-response)

Evidence:

- record startup line and local RPC response in [How to Verify](how-to-verify.md)

## Path C. Full Local Check

Use this when Path B works and you also need the local indexer health check.
For the longer indexer explanation, see [Indexer Setup](reference/indexer-setup.md).

Prerequisites:

- Path B passes
- `offckb node` is still running

Command:

```bash
echo '{"id":2,"jsonrpc":"2.0","method":"get_indexer_tip"}' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

On Windows PowerShell, run:

```powershell
$body = '{"id":2,"jsonrpc":"2.0","method":"get_indexer_tip"}'
curl.exe -H 'content-type: application/json' -d $body http://localhost:8114
```

PASS:

- response includes a `result` object
- `result` includes `block_hash` and `block_number`

Example successful output shape:

```json
{"jsonrpc":"2.0","result":{"block_hash":"0x...","block_number":"0x..."},"id":2}
```

FAIL:

- local service unavailable: [Local node process stopped](troubleshooting-matrix.md#local-node-process-stopped)
- invalid response: [Invalid JSON-RPC response](troubleshooting-matrix.md#invalid-json-rpc-response)
- endpoint confusion: [Wrong network or wrong endpoint](troubleshooting-matrix.md#wrong-network-or-wrong-endpoint)

Evidence:

- record endpoint and full indexer response in [How to Verify](how-to-verify.md)
