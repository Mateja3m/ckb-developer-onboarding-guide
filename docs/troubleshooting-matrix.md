# Troubleshooting Matrix

## Goal

Find the next check quickly when a beginner command fails.

## How To Use This Page

Match the symptom first.
Run the verification command before you change anything else.
Then return to the related section and retry the documented step exactly as written.

## Quick Lookup

| Symptom | Start Here | Verification Command |
| --- | --- | --- |
| `node` fails | [Node.js missing or wrong version](#nodejs-missing-or-wrong-version) | `node --version` |
| `curl` fails | [curl missing](#curl-missing) | `curl --version` |
| `offckb` fails | [offckb command missing](#offckb-command-missing) | `offckb --help` |
| endpoint cannot be reached | [RPC endpoint unreachable](#rpc-endpoint-unreachable) | `curl --head https://google.com` |
| response is not valid JSON-RPC | [Invalid JSON-RPC response](#invalid-json-rpc-response) | rerun the documented public RPC request |
| local node looks stuck | [Local node not syncing](#local-node-not-syncing) | rerun the local RPC request |
| endpoint or network is unclear | [Wrong network or wrong endpoint](#wrong-network-or-wrong-endpoint) | record and retry one endpoint |

## Node.js missing or wrong version

- Symptom: `node --version` fails or shows the wrong binary in your shell.
- Likely cause: Node.js is missing, the shell did not reload after install, or another tool manager changed `PATH`.
- Fix: install or reopen the shell, then rerun `node --version` before retrying npm or `offckb`.
- Verification command: `node --version`
- Related section: [Path B. Local Node](branching-paths.md#path-b-local-node)

## curl missing

- Symptom: `curl --version` fails.
- Likely cause: `curl` is not installed or not visible in the current shell.
- Fix: make `curl` available before retrying HTTPS or RPC steps.
- Verification command: `curl --version`
- Related section: [Quick Start](quick-start.md)

## offckb command missing

- Symptom: `offckb --help` fails after installation.
- Likely cause: the global npm bin path is not active in the current shell or the package install did not finish cleanly.
- Fix: rerun `npm install -g @offckb/cli`, reopen the shell, and retry `offckb --help`.
- Verification command: `offckb --help`
- Related section: [Path B. Local Node](branching-paths.md#path-b-local-node)

## RPC endpoint unreachable

- Symptom: hostname resolution fails, the connection is refused, or the request times out.
- Likely cause: network access is down, the hostname is wrong, or the local node is not running.
- Fix: verify general HTTPS access first, then verify the exact endpoint for the path you chose.
- Verification command: `curl --head https://google.com`
- Related section: [Quick Start](quick-start.md)

## Invalid JSON-RPC response

- Symptom: you receive HTML, a method error, empty output, or a body without `jsonrpc` and `result`.
- Likely cause: the request used the wrong method, the JSON was malformed, or the wrong endpoint was tested.
- Fix: copy the documented POST request exactly and retry it before changing ports or fields.
- Verification command: `echo '{"id":2,"jsonrpc":"2.0","method":"get_tip_block_number","params":[]}' | curl -H 'content-type: application/json' -d @- https://testnet.ckb.dev/rpc`
- Related section: [RPC Notes](reference/rpc-setup.md)

## Local node not syncing

- Symptom: the local node appears to start, but the block number stays low or unchanged.
- Likely cause: local devnet is still starting or you checked the value before the node stabilized.
- Fix: keep the node running, wait briefly, and rerun the same local RPC request before changing endpoints.
- Verification command: `echo '{"id":2,"jsonrpc":"2.0","method":"get_tip_block_number","params":[]}' | curl -H 'content-type: application/json' -d @- http://localhost:8114`
- Related section: [Path B. Local Node](branching-paths.md#path-b-local-node)

## Wrong network or wrong endpoint

- Symptom: the command succeeds, but you cannot tell whether it hit public testnet, local RPC, or the proxy port mentioned in startup logs.
- Likely cause: path switching happened before one path was finished.
- Fix: record the successful endpoint, finish the current path, and only then move to another one.
- Verification command: `echo '{"id":2,"jsonrpc":"2.0","method":"get_tip_block_number","params":[]}' | curl -H 'content-type: application/json' -d @- https://testnet.ckb.dev/rpc`
- Related section: [Branching Paths](branching-paths.md)
