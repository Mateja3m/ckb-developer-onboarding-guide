# Branching Paths

Choose one path after [Quick Start](quick-start.md).

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

PASS:

- response includes `"jsonrpc":"2.0"` and `"result"`

FAIL:

- use [RPC endpoint unreachable](troubleshooting-matrix.md#rpc-endpoint-unreachable)
- use [Invalid JSON-RPC response](troubleshooting-matrix.md#invalid-json-rpc-response)

Evidence:

- record command, endpoint, and response in [How to Verify](how-to-verify.md)

## Path B. Local Node

Use this when you need local logs and local devnet control.

Prerequisites:

- Path A passes
- npm can install global packages

Commands:

```bash
npm install -g @offckb/cli
offckb --help
offckb node
```

Keep `offckb node` running.
In another terminal, run:

```bash
echo '{"id":2,"jsonrpc":"2.0","method":"get_tip_block_number","params":[]}' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

PASS:

- `offckb --help` works
- `offckb node` reports `CKB devnet RPC Proxy server running on http://127.0.0.1:28114`
- local RPC returns `"jsonrpc":"2.0"` and `"result"`

FAIL:

- `offckb` fails: [offckb command missing](troubleshooting-matrix.md#offckb-command-missing)
- local RPC fails: [RPC endpoint unreachable](troubleshooting-matrix.md#rpc-endpoint-unreachable)
- response is unclear: [Invalid JSON-RPC response](troubleshooting-matrix.md#invalid-json-rpc-response)

Evidence:

- record startup line and local RPC response in [How to Verify](how-to-verify.md)

## Path C. Full Local Check

Use this when Path B works and you also need the local indexer health check.

Prerequisites:

- Path B passes
- `offckb node` is still running

Command:

```bash
echo '{"id":2,"jsonrpc":"2.0","method":"get_indexer_tip"}' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

PASS:

- response includes a `result` object
- `result` includes `block_hash` and `block_number`

FAIL:

- local service unavailable: [RPC endpoint unreachable](troubleshooting-matrix.md#rpc-endpoint-unreachable)
- invalid response: [Invalid JSON-RPC response](troubleshooting-matrix.md#invalid-json-rpc-response)
- endpoint confusion: [Wrong network or wrong endpoint](troubleshooting-matrix.md#wrong-network-or-wrong-endpoint)

Evidence:

- record endpoint and full indexer response in [How to Verify](how-to-verify.md)
