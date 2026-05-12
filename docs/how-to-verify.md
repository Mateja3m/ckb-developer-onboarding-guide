# How to Verify

Use this page after [Quick Start](quick-start.md) or one of the [Branching Paths](branching-paths.md).

Start with the public RPC check.
Only run the local node or indexer checks if you chose Path B or Path C.

## Where To Save Evidence

Save new evidence in `validation-logs/` or in a dated setup note.

Existing evidence is stored in:

- [environment-validation-findings.md](validation/environment-validation-findings.md)
- [ckb-node-and-rpc-validation-findings.md](validation/ckb-node-and-rpc-validation-findings.md)

## Step 1. Verify Your Environment

For the low-cost public RPC path, start with `curl` and HTTPS access.

Run:

```bash
curl --version
curl --head https://google.com
```

Expected output:

- `curl` returns version information
- `curl --head https://google.com` returns HTTP headers
- a redirect such as `HTTP/2 301` still counts as success

PASS:

- both commands return the expected output

FAIL:

- `curl` fails: [curl missing](troubleshooting-matrix.md#curl-missing)
- HTTPS fails: [RPC endpoint unreachable](troubleshooting-matrix.md#rpc-endpoint-unreachable)

Evidence to record:

- command outputs for both checks

## Step 2. Verify The Low-Cost Public RPC Path

Run the public RPC command from [Quick Start](quick-start.md#step-2-call-public-ckb-rpc).

Expected output:

- the response is JSON
- the response includes `"jsonrpc":"2.0"`
- the response includes `"result"`

PASS:

- public RPC returns valid JSON-RPC output

FAIL:

- no response: [RPC endpoint unreachable](troubleshooting-matrix.md#rpc-endpoint-unreachable)
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

PASS:

- all three commands return version information

FAIL:

- `node` fails: [Node.js missing or wrong version](troubleshooting-matrix.md#nodejs-missing-or-wrong-version)
- another tool fails: [Troubleshooting Matrix](troubleshooting-matrix.md)

Run the Path B commands from [Branching Paths](branching-paths.md#path-b-local-node).

Expected output:

- `offckb --help` works
- `offckb node` keeps running
- startup output includes `CKB devnet RPC Proxy server running on http://127.0.0.1:28114`
- local RPC returns `"jsonrpc":"2.0"` and `"result"`

PASS:

- the local node stays running and local RPC returns valid JSON-RPC output

FAIL:

- `offckb` fails: [offckb command missing](troubleshooting-matrix.md#offckb-command-missing)
- local RPC fails: [RPC endpoint unreachable](troubleshooting-matrix.md#rpc-endpoint-unreachable)
- response is unclear: [Invalid JSON-RPC response](troubleshooting-matrix.md#invalid-json-rpc-response)

Evidence to record:

- local tool versions
- `offckb --help` result
- local node startup line
- local RPC command and response

## Step 4. Verify The Local Indexer Path

Skip this step unless you chose Path C.

Run the Path C command from [Branching Paths](branching-paths.md#path-c-full-local-check).

Expected output:

- the response includes a `result` object
- `result` includes `block_hash`
- `result` includes `block_number`

PASS:

- local indexer returns the expected JSON-RPC result object

FAIL:

- local service unavailable: [RPC endpoint unreachable](troubleshooting-matrix.md#rpc-endpoint-unreachable)
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
