# Troubleshooting Matrix

## Goal

Map beginner failures to one next action.
Do not change endpoints, ports, or tools until you have matched the symptom and run the verification command.

## Quick Lookup

| Symptom | Start here | Verification command |
| --- | --- | --- |
| `node` fails | [Node.js missing or wrong version](#nodejs-missing-or-wrong-version) | `node --version` |
| `npm install -g @offckb/cli` fails | [npm global install fails](#npm-global-install-fails) | `npm --version` |
| `curl` fails | [curl missing](#curl-missing) | `curl --version` |
| hostname or HTTPS fails | [Network or DNS failure](#network-or-dns-failure) | `curl --head https://google.com` |
| `offckb` is unavailable | [offckb command missing](#offckb-command-missing) | `offckb --help` |
| first `offckb node` output looks alarming | [First-run binary download confusion](#first-run-binary-download-confusion) | watch `offckb node` until final startup or exit |
| startup prints warnings | [Warning-looking startup output](#warning-looking-startup-output) | check whether the node keeps running |
| local RPC refuses connection | [Local node process stopped](#local-node-process-stopped) | rerun local RPC while `offckb node` is running |
| browser says `POST or OPTIONS` | [RPC endpoint opened in a browser](#rpc-endpoint-opened-in-a-browser) | rerun the JSON-RPC POST request |
| response is not valid JSON-RPC | [Invalid JSON-RPC response](#invalid-json-rpc-response) | rerun the documented public RPC request |
| local block number is low | [Low block number misread as failure](#low-block-number-misread-as-failure) | inspect JSON-RPC structure |
| endpoint or network is unclear | [Wrong network or wrong endpoint](#wrong-network-or-wrong-endpoint) | record and retry one endpoint |
| indexer response is missing expected fields | [Indexer health check fails](#indexer-health-check-fails) | rerun `get_indexer_tip` |

## Node.js missing or wrong version

Symptom:

- `node --version` fails or returns an unexpected binary/version.

Likely cause:

- Node.js is missing, the shell did not reload after install, or another tool manager changed `PATH`.

Fix:

- Install or activate Node.js, reopen the shell, then rerun the check before trying npm or `offckb`.

Verification command:

```bash
node --version
```

Expected output:

- a version string such as `v20.x.x`, `v22.x.x`, or another installed Node.js version

PASS:

- the command returns a Node.js version

FAIL:

- stay in environment setup; do not continue to local CKB steps yet

Related section:

- [Path B. Local Node](branching-paths.md#path-b-local-node)

## npm global install fails

Symptom:

- `npm install -g @offckb/cli` fails, hangs, or exits with a permission/package error.

Likely cause:

- npm is missing, global install permissions are blocked, the npm registry is unreachable, or the shell uses a different Node.js installation than expected.

Fix:

- Confirm npm works first, then rerun the install in the same shell. If the error is permission-related, fix the local npm setup before retrying CKB-specific commands.

Verification command:

```bash
npm --version
```

Expected output:

- an npm version string

PASS:

- npm returns a version and the `@offckb/cli` install completes

FAIL:

- record the npm error and treat it as a local tooling issue, not a CKB node issue

Related section:

- [CKB Node Setup](reference/ckb-node-setup.md)

## curl missing

Symptom:

- `curl --version` fails.

Likely cause:

- `curl` is not installed or not visible in the current shell.

Fix:

- Make `curl` available before retrying HTTPS or RPC steps.

Verification command:

```bash
curl --version
```

Expected output:

- curl version information and supported protocol/features

PASS:

- `curl` returns version information

FAIL:

- stop before Quick Start; the public RPC path depends on curl

Related section:

- [Quick Start](quick-start.md)

## Network or DNS failure

Symptom:

- hostname resolution fails, HTTPS cannot connect, or a request times out.

Likely cause:

- DNS issue, VPN/proxy issue, firewall restriction, local network problem, or a mistyped hostname.

Fix:

- Verify general HTTPS access first. Only debug the CKB endpoint after a known HTTPS target works.

Verification command:

```bash
curl --head https://google.com
```

Expected output:

- HTTP headers such as `HTTP/2 301`, `HTTP/2 200`, or another valid HTTP response

PASS:

- HTTPS works; retry the documented CKB RPC command exactly

FAIL:

- record the exact curl error, such as `curl: (6) Could not resolve host`, before changing CKB commands

Related section:

- [How to Verify](how-to-verify.md#step-1-verify-your-environment)

## offckb command missing

Symptom:

- `offckb --help` fails after installation.

Likely cause:

- the global npm bin path is not active in the current shell or the install did not finish cleanly.

Fix:

- Rerun the install, reopen the shell, and verify that the global npm binary directory is visible.

Verification command:

```bash
offckb --help
```

Expected output:

- help output that includes available commands, including `node`

PASS:

- `offckb --help` works

FAIL:

- fix npm/global-path setup before running `offckb node`

Related section:

- [Path B. Local Node](branching-paths.md#path-b-local-node)

## First-run binary download confusion

Symptom:

- the first `offckb node` run prints a missing-binary or error-looking message.

Likely cause:

- on the validation machine, the first run recovered by downloading the required CKB binary before startup completed.

Fix:

- Keep reading the output until the process either reaches a startup signal or exits. Do not treat the first alarming line as the final result.

Verification command:

```bash
offckb node
```

Expected output:

- the process keeps running and eventually prints `CKB devnet RPC Proxy server running on http://127.0.0.1:28114`

PASS:

- the node reaches the startup signal and stays active

FAIL:

- the process exits without the startup signal; record the final error block

Related section:

- [CKB Node Setup](reference/ckb-node-setup.md#early-missing-binary-message)

## Warning-looking startup output

Symptom:

- startup output includes a warning-style line and the beginner assumes the node failed.

Likely cause:

- not every warning-style line is fatal; validation recorded warning-like output before successful startup.

Fix:

- Check whether the process continues running and reaches the expected startup signal.

Verification command:

```bash
offckb node
```

Expected output:

- a running process plus the startup signal for the devnet RPC proxy

PASS:

- the process stays alive and local RPC can be queried from another terminal

FAIL:

- the process exits or never reaches a startup signal

Related section:

- [Common Errors And Remediation](reference/common-errors-and-remediation.md#4-warning-looking-startup-output)

## Local node process stopped

Symptom:

- the local RPC request fails with connection refused, empty response, or timeout.

Likely cause:

- `offckb node` is not running, was interrupted, or is running in a different local state than expected.

Fix:

- Keep `offckb node` running in one terminal and run the RPC request in another terminal.

Verification command:

```bash
echo '{"id":2,"jsonrpc":"2.0","method":"get_tip_block_number","params":[]}' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

Expected output:

- JSON output including `"jsonrpc":"2.0"` and `"result"`

PASS:

- local RPC returns valid JSON-RPC

FAIL:

- restart the node and capture both terminal outputs

Related section:

- [Path B. Local Node](branching-paths.md#path-b-local-node)

## RPC endpoint opened in a browser

Symptom:

- opening the endpoint in a browser returns `Used HTTP Method is not allowed. POST or OPTIONS is required`.

Likely cause:

- the endpoint was tested with a browser GET request instead of a JSON-RPC POST request.

Fix:

- Use the documented curl POST command.

Verification command:

```bash
echo '{"id":2,"jsonrpc":"2.0","method":"get_tip_block_number","params":[]}' \
| curl -H 'content-type: application/json' -d @- \
https://testnet.ckb.dev/rpc
```

Expected output:

- JSON output including `"jsonrpc":"2.0"` and `"result"`

PASS:

- the POST request works

FAIL:

- continue with [Network or DNS failure](#network-or-dns-failure) or [Invalid JSON-RPC response](#invalid-json-rpc-response)

Related section:

- [FAQ](faq.md#why-did-the-rpc-endpoint-say-post-or-options-is-required)

## Invalid JSON-RPC response

Symptom:

- you receive HTML, empty output, a method error, or a body without `jsonrpc` and `result`.

Likely cause:

- wrong HTTP method, malformed JSON, wrong endpoint, or an endpoint that is not the expected CKB RPC service.

Fix:

- Copy the documented POST request exactly and retry it before changing ports or fields.

Verification command:

```bash
echo '{"id":2,"jsonrpc":"2.0","method":"get_tip_block_number","params":[]}' \
| curl -H 'content-type: application/json' -d @- \
https://testnet.ckb.dev/rpc
```

Expected output:

- JSON output including `"jsonrpc":"2.0"` and `"result"`

PASS:

- the response matches the expected JSON-RPC shape

FAIL:

- record the full response body and endpoint

Related section:

- [Quick Start](quick-start.md#step-2-call-public-ckb-rpc)

## Low block number misread as failure

Symptom:

- the response includes a low value such as `"result":"0x0"` and the beginner assumes the step failed.

Likely cause:

- the beginner is reading the block number as the success signal instead of the JSON-RPC response shape.

Fix:

- Check the structure first. For this guide, valid JSON-RPC output with a `result` field is the success signal.

Verification command:

```bash
echo '{"id":2,"jsonrpc":"2.0","method":"get_tip_block_number","params":[]}' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

Expected output:

- JSON output including `"jsonrpc":"2.0"` and `"result"`, even if the result value is low

PASS:

- the JSON-RPC shape is valid

FAIL:

- use [Invalid JSON-RPC response](#invalid-json-rpc-response)

Related section:

- [FAQ](faq.md#does-a-low-block-number-such-as-0x0-mean-the-step-failed)

## Wrong network or wrong endpoint

Symptom:

- the command succeeds, but you cannot tell whether it hit public testnet, local RPC, or the proxy port mentioned in startup logs.

Likely cause:

- path switching happened before one path was finished.

Fix:

- Record the endpoint, finish the current path, and only then compare another endpoint.

Verification command:

```bash
echo '{"id":2,"jsonrpc":"2.0","method":"get_tip_block_number","params":[]}' \
| curl -H 'content-type: application/json' -d @- \
https://testnet.ckb.dev/rpc
```

Expected output:

- JSON-RPC response from the exact endpoint shown in the command

PASS:

- you can name the endpoint that produced the response

FAIL:

- restart from [Branching Paths](branching-paths.md) and choose one path only

Related section:

- [Branching Paths](branching-paths.md)

## Indexer health check fails

Symptom:

- `get_indexer_tip` does not return a `result` object with `block_hash` and `block_number`.

Likely cause:

- local node path is not running, wrong endpoint was used, or indexer-backed service is not ready.

Fix:

- Confirm Path B passes first, keep `offckb node` running, then rerun the indexer health check.

Verification command:

```bash
echo '{"id":2,"jsonrpc":"2.0","method":"get_indexer_tip"}' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

Expected output:

- JSON output with `result.block_hash` and `result.block_number`

PASS:

- local indexer health check returns the expected result object

FAIL:

- record the endpoint and full response, then return to [Path C. Full Local Check](branching-paths.md#path-c-full-local-check)

Related section:

- [Indexer Setup](reference/indexer-setup.md)
