# 分支路径

完成 [快速开始](quick-start.md) 后选择一个路径。

仓库维护者提供的本地节点验证来自 macOS arm64。
如果你在其他操作系统上测试，请通过 `Cold Start Guide Test` issue 记录结果。
本页包含 Windows PowerShell 的 RPC 命令写法，但 Windows 仍需要 community reproduction 后才算已验证。

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

在 Windows PowerShell 中运行：

```powershell
$body = '{"id":2,"jsonrpc":"2.0","method":"get_tip_block_number","params":[]}'
$body | curl.exe `
  -H "content-type: application/json" `
  --data-binary "@-" `
  https://testnet.ckb.dev/rpc
```

PASS：

- 响应包含 `"jsonrpc":"2.0"` 和 `"result"`

成功输出示例：

```json
{"jsonrpc":"2.0","result":"0x123","id":2}
```

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

在 Windows PowerShell 中运行相同的安装和启动命令。
如果安装后 `offckb` 还不能识别，请重新打开 PowerShell，再运行 `offckb --help`。

保持 `offckb node` 运行。
如果启动输出很长或看起来像错误，请先参考英文页 [Read OffCKB Startup Output](../how-to/read-offckb-startup-output.md)。
OffCKB 启动日志会显示 proxy 地址 `127.0.0.1:28114`，但本仓库验证过的新手 RPC health check 仍然使用 `http://localhost:8114`。
关于这两个端口的关系，请看英文参考页 [Port Confusion During Startup](../reference/ckb-node-setup.md#port-confusion-during-startup)。
在另一个终端运行：

```bash
echo '{"id":2,"jsonrpc":"2.0","method":"get_tip_block_number","params":[]}' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

在 Windows PowerShell 中运行：

```powershell
$body = '{"id":2,"jsonrpc":"2.0","method":"get_tip_block_number","params":[]}'
$body | curl.exe `
  -H "content-type: application/json" `
  --data-binary "@-" `
  http://localhost:8114
```

PASS：

- `offckb --help` 可用
- `offckb node` 输出 `CKB devnet RPC Proxy server running on http://127.0.0.1:28114`
- 本地 RPC 返回 `"jsonrpc":"2.0"` 和 `"result"`

成功启动行示例：

```text
CKB devnet RPC Proxy server running on http://127.0.0.1:28114
```

本地 RPC 成功输出示例：

```json
{"jsonrpc":"2.0","result":"0x0","id":2}
```

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

在 Windows PowerShell 中运行：

```powershell
$body = '{"id":2,"jsonrpc":"2.0","method":"get_indexer_tip"}'
$body | curl.exe `
  -H "content-type: application/json" `
  --data-binary "@-" `
  http://localhost:8114
```

PASS：

- 响应包含 `result` 对象
- `result` 包含 `block_hash`
- `result` 包含 `block_number`

成功输出结构示例：

```json
{"jsonrpc":"2.0","result":{"block_hash":"0x...","block_number":"0x..."},"id":2}
```

FAIL：

- 本地服务不可用：查看 [Local node process stopped](troubleshooting-matrix.md#local-node-process-stopped)
- 响应格式不对：查看 [Invalid JSON-RPC response](troubleshooting-matrix.md#invalid-json-rpc-response)
- 端点混淆：查看 [Wrong network or wrong endpoint](troubleshooting-matrix.md#wrong-network-or-wrong-endpoint)

证据：

- 在 [如何验证](how-to-verify.md) 中记录端点和完整 indexer 响应
