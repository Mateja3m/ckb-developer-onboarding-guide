# 分支路径

完成 [快速开始](quick-start.md) 后选择一个路径。

## Path A. Public RPC Only

当你想走最低成本路径时使用。

前置条件：

- Quick Start 的前置检查通过

命令：

```bash
echo '{"id":2,"jsonrpc":"2.0","method":"get_tip_block_number","params":[]}' \
| curl -H 'content-type: application/json' -d @- \
https://testnet.ckb.dev/rpc
```

PASS：

- 响应包含 `"jsonrpc":"2.0"` 和 `"result"`

FAIL：

- 查看 [Network or DNS failure](troubleshooting-matrix.md#network-or-dns-failure)
- 查看 [Invalid JSON-RPC response](troubleshooting-matrix.md#invalid-json-rpc-response)

证据：

- 在 [如何验证](how-to-verify.md) 中记录命令、端点和响应

## Path B. Local Node

当你需要本地日志、本地控制或 devnet 路径时使用。
更长说明请看英文参考页：[CKB Node Setup](../reference/ckb-node-setup.md) 和 [RPC Basics](../reference/rpc-setup.md)。

前置条件：

- Path A 通过
- npm 可以安装全局包

命令：

```bash
npm install -g @offckb/cli
offckb --help
offckb node
```

保持 `offckb node` 运行。
在另一个终端运行：

```bash
echo '{"id":2,"jsonrpc":"2.0","method":"get_tip_block_number","params":[]}' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

PASS：

- `offckb --help` 可用
- `offckb node` 输出 `CKB devnet RPC Proxy server running on http://127.0.0.1:28114`
- 本地 RPC 返回 `"jsonrpc":"2.0"` 和 `"result"`

FAIL：

- `offckb` 失败：查看 [offckb command missing](troubleshooting-matrix.md#offckb-command-missing)
- 本地 RPC 失败：查看 [Local node process stopped](troubleshooting-matrix.md#local-node-process-stopped)
- 响应不清楚：查看 [Invalid JSON-RPC response](troubleshooting-matrix.md#invalid-json-rpc-response)

证据：

- 在 [如何验证](how-to-verify.md) 中记录启动行和本地 RPC 响应

## Path C. Full Local Check

当 Path B 通过，并且你还需要本地 indexer 健康检查时使用。
更长说明请看英文参考页：[Indexer Setup](../reference/indexer-setup.md)。

前置条件：

- Path B 通过
- `offckb node` 仍在运行

命令：

```bash
echo '{"id":2,"jsonrpc":"2.0","method":"get_indexer_tip"}' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

PASS：

- 响应包含 `result` 对象
- `result` 包含 `block_hash`
- `result` 包含 `block_number`

FAIL：

- 本地服务不可用：查看 [Local node process stopped](troubleshooting-matrix.md#local-node-process-stopped)
- 响应格式不对：查看 [Invalid JSON-RPC response](troubleshooting-matrix.md#invalid-json-rpc-response)
- 端点混淆：查看 [Wrong network or wrong endpoint](troubleshooting-matrix.md#wrong-network-or-wrong-endpoint)

证据：

- 在 [如何验证](how-to-verify.md) 中记录端点和完整 indexer 响应
