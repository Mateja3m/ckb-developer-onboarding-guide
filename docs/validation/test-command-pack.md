# Test Command Pack

Use [How to Verify](../how-to-verify.md) for the current reader checklist.

This file is a support pack for people collecting new evidence.

## Environment Commands

```bash
pwd
echo "$SHELL"
uname -a
node --version
npm --version
git --version
curl --version
curl --head https://google.com
```

## Public RPC Command

```bash
echo '{"id":2,"jsonrpc":"2.0","method":"get_tip_block_number","params":[]}' \
| curl -H 'content-type: application/json' -d @- \
https://testnet.ckb.dev/rpc
```

## Local Node Commands

```bash
npm install -g @offckb/cli
offckb --help
offckb node
```

In a second terminal:

```bash
echo '{"id":2,"jsonrpc":"2.0","method":"get_tip_block_number","params":[]}' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

## Local Indexer Command

```bash
echo '{"id":2,"jsonrpc":"2.0","method":"get_indexer_tip"}' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```
