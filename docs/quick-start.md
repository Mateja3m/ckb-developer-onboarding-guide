# Quick Start

## Goal

Get one valid CKB JSON-RPC response using public RPC.
For the longer RPC explanation, see [RPC Basics](reference/rpc-setup.md).

## Use This If

- you are new to CKB
- you want the lowest-cost path
- you do not want to run a local node yet

Time required: 10 to 15 minutes.

## Prerequisites

For the public RPC quick start, you only need:

- a terminal
- `curl`
- working HTTPS access

Run:

```bash
curl --version
```

PASS:

- `curl` returns version information

FAIL:

- `curl` fails: [curl missing](troubleshooting-matrix.md#curl-missing)

Note:

- `node`, `npm`, and `git` are not required for Path A.
- You will check `node`, `npm`, and `git` later only if you choose [Path B](branching-paths.md#path-b-local-node) or [Path C](branching-paths.md#path-c-full-local-check).

## Step 1. Check Network Access

Run:

```bash
curl --head https://google.com
```

PASS:

- HTTP headers are returned
- `HTTP/2 301` or another redirect still counts as success

FAIL:

- use [Network or DNS failure](troubleshooting-matrix.md#network-or-dns-failure)

## Step 2. Call Public CKB RPC

Run:

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "get_tip_block_number",
    "params": []
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
https://testnet.ckb.dev/rpc
```

PASS:

- the response is JSON
- the response includes `"jsonrpc":"2.0"`
- the response includes `"result"`

FAIL:

- no connection: [Network or DNS failure](troubleshooting-matrix.md#network-or-dns-failure)
- invalid response: [Invalid JSON-RPC response](troubleshooting-matrix.md#invalid-json-rpc-response)
- wrong network or endpoint: [Wrong network or wrong endpoint](troubleshooting-matrix.md#wrong-network-or-wrong-endpoint)

## Step 3. Record Evidence

Record:

- command
- endpoint
- full response

Use [How to Verify](how-to-verify.md) for the final checklist.

## Next Step

- stay remote: [Path A](branching-paths.md#path-a-public-rpc-only)
- run a local node: [Path B](branching-paths.md#path-b-local-node)
- add local indexer check: [Path C](branching-paths.md#path-c-full-local-check)
