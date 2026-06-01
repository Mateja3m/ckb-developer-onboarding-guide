# How to Verify

Use this page after [Quick Start](quick-start.md) or one of the [Branching Paths](branching-paths.md).

Start with the public RPC check.
Only run the local node or indexer checks if you chose Path B or Path C.

Current repository-maintained validation was performed on macOS arm64.
For other operating systems, record the result through [Test The Guide](contributing/test-the-guide.md).
On Windows PowerShell, use the `curl.exe` command variants from [Quick Start](quick-start.md) and [Branching Paths](branching-paths.md).

## Where To Save Evidence

Keep reviewer-facing evidence in the tracked `docs/validation/` files below.
Use `validation-logs/` only for sanitized, publishable reproduction logs.
Do not commit personal home paths or usernames.

Existing evidence is stored in:

- [environment-validation-findings.md](validation/environment-validation-findings.md)
- [ckb-node-and-rpc-validation-findings.md](validation/ckb-node-and-rpc-validation-findings.md)
- [community-reproduction-results.md](validation/community-reproduction-results.md)

For independent review, use [Third-Party Reproducibility Checklist](third-party-reproducibility.md).

## Step 1. Verify Your Environment

For the low-cost public RPC path, start with `curl` and HTTPS access.

Run:

```bash
curl --version
curl --head https://google.com
```

On Windows PowerShell, run:

```powershell
curl.exe --version
curl.exe --head https://google.com
```

Expected output:

- `curl` returns version information
- `curl --head https://google.com` returns HTTP headers
- a redirect such as `HTTP/2 301` still counts as success

Example successful output:

```text
curl 8.x.x
HTTP/2 301
```

PASS:

- both commands return the expected output

FAIL:

- `curl` fails: [curl missing](troubleshooting-matrix.md#curl-missing)
- HTTPS fails: [Network or DNS failure](troubleshooting-matrix.md#network-or-dns-failure)

Evidence to record:

- command outputs for both checks

## Step 2. Verify The Low-Cost Public RPC Path

Run the public RPC command from [Quick Start](quick-start.md#step-2-call-public-ckb-rpc).
Use the PowerShell variant from that section if you are testing on Windows PowerShell.

Expected output:

- the response is JSON
- the response includes `"jsonrpc":"2.0"`
- the response includes `"result"`

Example successful output:

```json
{"jsonrpc":"2.0","result":"0x123","id":2}
```

PASS:

- public RPC returns valid JSON-RPC output

FAIL:

- no response: [Network or DNS failure](troubleshooting-matrix.md#network-or-dns-failure)
- wrong response shape: [Invalid JSON-RPC response](troubleshooting-matrix.md#invalid-json-rpc-response)
- endpoint confusion: [Wrong network or wrong endpoint](troubleshooting-matrix.md#wrong-network-or-wrong-endpoint)

Evidence to record:

- exact command
- endpoint used
- full response

This is the minimum low-cost reproduction path.

## Step 3. Verify The Local Node Path

Skip this step if you only chose Path A.

First confirm the local tools needed for Path B or Path C:

```bash
node --version
npm --version
git --version
```

Expected output:

- each command returns version information

Example successful output:

```text
v22.x.x
10.x.x
git version 2.x.x
```

PASS:

- all three commands return version information

FAIL:

- `node` fails: [Node.js missing or wrong version](troubleshooting-matrix.md#nodejs-missing-or-wrong-version)
- another tool fails: [Troubleshooting Matrix](troubleshooting-matrix.md)

Run the Path B commands from [Branching Paths](branching-paths.md#path-b-local-node).
Use the PowerShell local RPC variant from that section if you are testing on Windows PowerShell.
The OffCKB startup log advertises its proxy on `127.0.0.1:28114`, but this guide's beginner RPC health check still targets `http://localhost:8114`.
For the port relationship, see [Port Confusion During Startup](reference/ckb-node-setup.md#port-confusion-during-startup).

Expected output:

- `offckb --help` works
- `offckb node` keeps running
- startup output includes `CKB devnet RPC Proxy server running on http://127.0.0.1:28114`
- local RPC returns `"jsonrpc":"2.0"` and `"result"`

Example successful local RPC output:

```json
{"jsonrpc":"2.0","result":"0x0","id":2}
```

PASS:

- the local node stays running and local RPC returns valid JSON-RPC output

FAIL:

- `offckb` fails: [offckb command missing](troubleshooting-matrix.md#offckb-command-missing)
- local RPC fails: [Local node process stopped](troubleshooting-matrix.md#local-node-process-stopped)
- response is unclear: [Invalid JSON-RPC response](troubleshooting-matrix.md#invalid-json-rpc-response)

Evidence to record:

- local tool versions
- `offckb --help` result
- local node startup line
- local RPC command and response

## Step 4. Verify The Local Indexer Path

Skip this step unless you chose Path C.

Run the Path C command from [Branching Paths](branching-paths.md#path-c-full-local-check).
Use the PowerShell indexer variant from that section if you are testing on Windows PowerShell.

Expected output:

- the response includes a `result` object
- `result` includes `block_hash`
- `result` includes `block_number`

Example successful output shape:

```json
{"jsonrpc":"2.0","result":{"block_hash":"0x...","block_number":"0x..."},"id":2}
```

PASS:

- local indexer returns the expected JSON-RPC result object

FAIL:

- local service unavailable: [Local node process stopped](troubleshooting-matrix.md#local-node-process-stopped)
- invalid response: [Invalid JSON-RPC response](troubleshooting-matrix.md#invalid-json-rpc-response)
- endpoint confusion: [Wrong network or wrong endpoint](troubleshooting-matrix.md#wrong-network-or-wrong-endpoint)

Evidence to record:

- indexer command
- endpoint used
- full response

## Review Checklist

Before requesting review, confirm:

- `curl` and HTTPS checks passed
- public RPC check passed
- local node evidence exists if you used Path B or Path C
- local indexer evidence exists if you used Path C
- each evidence note includes command, endpoint, output, and date
- operating system is recorded
- terminal shell is recorded, especially PowerShell, PowerShell 7, Git Bash, or WSL on Windows
- personal home paths and usernames are replaced with `$HOME` and `<local-user>`
