# 快速开始

## 目标

使用公共 RPC 获得一次有效的 CKB JSON-RPC 响应。
更详细的 RPC 说明请看英文参考页：[RPC Basics](../reference/rpc-setup.md)。

仓库维护者提供的验证日志来自 macOS arm64。
如果你在其他操作系统上测试，请通过 `Cold Start Guide Test` issue 记录结果。
在 Windows PowerShell 中，请使用 `curl.exe` 示例，避免 PowerShell 把 `curl` 当作 alias 处理。

## 适用场景

- 你刚开始接触 CKB
- 你想先走成本最低的路径
- 你暂时不想运行本地节点

目标时间：公共 RPC 路径 10 到 15 分钟。
如果你在测试本指南，请记录实际用时。

## 前置条件

公共 RPC 快速开始只需要：

- 一个终端
- `curl`
- 可用的 HTTPS 网络访问

运行：

```bash
curl --version
```

在 Windows PowerShell 中运行：

```powershell
curl.exe --version
```

PASS：

- `curl` 返回版本信息

成功输出示例：

```text
curl 8.x.x
```

FAIL：

- `curl` 失败：查看 [curl missing](troubleshooting-matrix.md#curl-missing)

注意：

- Path A 不需要 `node`、`npm` 或 `git`。
- 只有当你选择 [Path B](branching-paths.md#path-b-local-node) 或 [Path C](branching-paths.md#path-c-full-local-check) 时，才需要检查 `node`、`npm` 和 `git`。

## Step 1. 检查网络访问

运行：

```bash
curl --head https://google.com
```

在 Windows PowerShell 中运行：

```powershell
curl.exe --head https://google.com
```

PASS：

- 返回 HTTP headers
- `HTTP/2 301` 或其他重定向也算成功

成功输出示例：

```text
HTTP/2 301
```

FAIL：

- 查看 [Network or DNS failure](troubleshooting-matrix.md#network-or-dns-failure)

## Step 2. 调用公共 CKB RPC

运行：

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

在 Windows PowerShell 中运行：

```powershell
$body = '{"id":2,"jsonrpc":"2.0","method":"get_tip_block_number","params":[]}'
$body | curl.exe `
  -H "content-type: application/json" `
  --data-binary "@-" `
  https://testnet.ckb.dev/rpc
```

PASS：

- 响应是 JSON
- 响应包含 `"jsonrpc":"2.0"`
- 响应包含 `"result"`

成功输出示例：

```json
{"jsonrpc":"2.0","result":"0x123","id":2}
```

实际的 `result` 值可以不同。
成功信号是 JSON-RPC 结构，而不是某个固定 block number。

FAIL：

- 无连接：查看 [Network or DNS failure](troubleshooting-matrix.md#network-or-dns-failure)
- 响应格式不对：查看 [Invalid JSON-RPC response](troubleshooting-matrix.md#invalid-json-rpc-response)
- 网络或端点不清楚：查看 [Wrong network or wrong endpoint](troubleshooting-matrix.md#wrong-network-or-wrong-endpoint)

## Step 3. 记录证据

记录：

- 命令
- 端点
- 完整响应
- 如果你在测试本指南，记录实际用时

最终检查请使用 [如何验证](how-to-verify.md)。

## 下一步

- 继续使用远程 RPC：[Path A](branching-paths.md#path-a-public-rpc-only)
- 运行本地节点：[Path B](branching-paths.md#path-b-local-node)
- 增加本地 indexer 检查：[Path C](branching-paths.md#path-c-full-local-check)
