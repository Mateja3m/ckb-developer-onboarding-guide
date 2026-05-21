# Third-Party Reproducibility Checklist

This checklist is for reviewers or contributors who did not write the guide.
It turns the onboarding claim into a low-cost independent test.

## Reviewer Profile

Use this checklist with a reviewer who has:

- no prior contribution to this repository
- access to a terminal
- permission to install npm packages if testing the local node path
- enough network access to reach HTTPS and npm

## Required Result Format

For each step, record:

- date
- operating system
- command run
- endpoint used
- exact output or error
- PASS or FAIL
- link to the troubleshooting entry used after a failure

## Path A. Public RPC Reproduction

Run:

```bash
curl --version
curl --head https://google.com
```

Expected output:

- `curl --version` returns version information
- `curl --head https://google.com` returns HTTP headers

Run:

```bash
echo '{"id":2,"jsonrpc":"2.0","method":"get_tip_block_number","params":[]}' \
| curl -H 'content-type: application/json' -d @- \
https://testnet.ckb.dev/rpc
```

Expected output:

- JSON output
- `"jsonrpc":"2.0"`
- `"result"`

## Path B. Local Node Reproduction

Run:

```bash
node --version
npm --version
git --version
npm install -g @offckb/cli
offckb --help
offckb node
```

Expected output:

- tool version commands return version information
- `offckb --help` returns help output
- `offckb node` keeps running
- startup output includes `CKB devnet RPC Proxy server running on http://127.0.0.1:28114`

In another terminal, run:

```bash
echo '{"id":2,"jsonrpc":"2.0","method":"get_tip_block_number","params":[]}' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

Expected output:

- JSON output
- `"jsonrpc":"2.0"`
- `"result"`

## Path C. Indexer Health Check

Run this only after Path B passes.

```bash
echo '{"id":2,"jsonrpc":"2.0","method":"get_indexer_tip"}' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

Expected output:

- JSON output
- `result` object
- `block_hash`
- `block_number`

## Reviewer Decision

The guide passes independent reproduction when:

- Path A passes on at least one reviewer machine
- Path B passes on at least one reviewer machine if local-node scope is being reviewed
- Path C passes on at least one reviewer machine if indexer scope is being reviewed
- any failure can be mapped to [Troubleshooting Matrix](troubleshooting-matrix.md)

If a reviewer cannot complete a path, open an issue with the recorded output instead of changing commands silently.
