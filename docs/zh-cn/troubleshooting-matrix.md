# 故障排查矩阵

## 目标

把新手常见失败映射到一个下一步动作。
在匹配症状并运行验证命令之前，不要更改端点、端口或工具。

## 快速查找

| 症状 | 从这里开始 | 验证命令 |
| --- | --- | --- |
| `node` 失败 | [Node.js missing or wrong version](#nodejs-missing-or-wrong-version) | `node --version` |
| `npm install -g @offckb/cli` 失败 | [npm global install fails](#npm-global-install-fails) | `npm --version` |
| `curl` 失败 | [curl missing](#curl-missing) | `curl --version` |
| PowerShell 中 `curl` 表现不同 | [Windows PowerShell curl alias or quoting issue](#windows-powershell-curl-alias-or-quoting-issue) | `curl.exe --version` |
| hostname 或 HTTPS 失败 | [Network or DNS failure](#network-or-dns-failure) | `curl --head https://google.com` |
| `offckb` 不可用 | [offckb command missing](#offckb-command-missing) | `offckb --help` |
| 第一次 `offckb node` 输出看起来像错误 | [First-run binary download confusion](#first-run-binary-download-confusion) | 观察 `offckb node` 直到最终启动或退出 |
| 启动输出包含 warning | [Warning-looking startup output](#warning-looking-startup-output) | 检查节点是否继续运行 |
| 本地 RPC 连接被拒绝 | [Local node process stopped](#local-node-process-stopped) | 在 `offckb node` 运行时重试本地 RPC |
| 浏览器显示 `POST or OPTIONS` | [RPC endpoint opened in a browser](#rpc-endpoint-opened-in-a-browser) | 重跑 JSON-RPC POST 请求 |
| 响应不是有效 JSON-RPC | [Invalid JSON-RPC response](#invalid-json-rpc-response) | 重跑文档中的公共 RPC 请求 |
| 本地 block number 很低 | [Low block number misread as failure](#low-block-number-misread-as-failure) | 检查 JSON-RPC 结构 |
| 网络或端点不清楚 | [Wrong network or wrong endpoint](#wrong-network-or-wrong-endpoint) | 记录并只重试一个端点 |
| indexer 响应缺少字段 | [Indexer health check fails](#indexer-health-check-fails) | 重跑 `get_indexer_tip` |

## Node.js missing or wrong version

症状：

- `node --version` 失败，或返回意外的版本/二进制。

可能原因：

- Node.js 未安装、安装后 shell 未刷新，或工具管理器改变了 `PATH`。

修复：

- 安装或激活 Node.js，重新打开 shell，然后再运行 npm 或 `offckb`。

验证命令：

```bash
node --version
```

预期输出：

- 类似 `v20.x.x`、`v22.x.x` 的 Node.js 版本字符串

PASS：

- 命令返回 Node.js 版本

FAIL：

- 停留在环境设置阶段，不要继续 CKB 本地步骤

## npm global install fails

症状：

- `npm install -g @offckb/cli` 失败、卡住，或因权限/包解析错误退出。

可能原因：

- npm 缺失、全局安装权限受阻、npm registry 不可达，或当前 shell 使用了意外的 Node.js 安装。

修复：

- 先确认 npm 可用，再在同一个 shell 中重跑安装。如果是权限错误，先修复本地 npm 设置。

验证命令：

```bash
npm --version
```

预期输出：

- npm 版本字符串

PASS：

- npm 返回版本，并且 `@offckb/cli` 安装完成

FAIL：

- 记录 npm 错误，把它视为本地工具问题，而不是 CKB 节点问题

## curl missing

症状：

- `curl --version` 失败。
- 在 Windows PowerShell 中，`curl` 的行为和文档中的 curl 命令不同。

可能原因：

- `curl` 未安装或当前 shell 不可见。
- 在 Windows PowerShell 中，`curl` 可能是 PowerShell alias，而不是 `curl.exe`。

修复：

- 先让 `curl` 可用，再重试 HTTPS 或 RPC。
- 在 Windows PowerShell 中，使用本指南里的 `curl.exe` 示例。

验证命令：

```bash
curl --version
```

Windows PowerShell：

```powershell
curl.exe --version
```

预期输出：

- curl 版本信息和支持的协议/功能

PASS：

- `curl` 返回版本信息

FAIL：

- 暂停 Quick Start；公共 RPC 路径依赖 curl

## Windows PowerShell curl alias or quoting issue

症状：

- 同一个 RPC 命令在 Bash 或 Git Bash 中可用，但在 Windows PowerShell 中失败
- `curl` 输出看起来像 PowerShell web request 输出，而不是 curl 输出
- 把 Bash pipeline 复制到 PowerShell 后，JSON body 被拒绝
- PowerShell 发送的 JSON 格式不正确，RPC server 返回 parse error，例如 `"code":-32700`

可能原因：

- Windows PowerShell 可能把 `curl` 作为 alias 处理，而不是调用 curl executable。
- Bash 的换行和 pipe 写法不一定能直接复制到 PowerShell。

修复：

- 使用 `curl.exe`，不要使用 `curl`。
- 使用 [快速开始](quick-start.md) 或 [分支路径](branching-paths.md) 中的 PowerShell 命令写法。
- 把 JSON body pipe 给 `curl.exe`，并使用 `--data-binary "@-"` 发送。

验证命令：

```powershell
$body = '{"id":2,"jsonrpc":"2.0","method":"get_tip_block_number","params":[]}'
$body | curl.exe `
  -H "content-type: application/json" `
  --data-binary "@-" `
  https://testnet.ckb.dev/rpc
```

预期输出：

- JSON 输出包含 `"jsonrpc":"2.0"` 和 `"result"`

PASS：

- PowerShell 命令返回有效 JSON-RPC 输出

FAIL：

- 先记录完整 PowerShell 错误和 shell 版本，不要马上更换端点

## Network or DNS failure

症状：

- hostname 解析失败、HTTPS 无法连接，或请求超时。

可能原因：

- DNS、VPN/proxy、防火墙、本地网络或 hostname 拼写问题。

修复：

- 先验证通用 HTTPS 访问，再调试 CKB 端点。

验证命令：

```bash
curl --head https://google.com
```

Windows PowerShell：

```powershell
curl.exe --head https://google.com
```

预期输出：

- HTTP headers，例如 `HTTP/2 301`、`HTTP/2 200` 或其他有效 HTTP 响应

PASS：

- HTTPS 可用；严格重试文档中的 CKB RPC 命令

FAIL：

- 记录完整 curl 错误，例如 `curl: (6) Could not resolve host`

## offckb command missing

症状：

- 安装后 `offckb --help` 失败。

可能原因：

- 全局 npm bin 路径不在当前 shell 中，或安装未完成。

修复：

- 重跑安装，重新打开 shell，并确认全局 npm binary 目录可见。

验证命令：

```bash
offckb --help
```

预期输出：

- help 输出，包含可用命令，包括 `node`

PASS：

- `offckb --help` 可用

FAIL：

- 在运行 `offckb node` 前修复 npm/global-path 设置

## First-run binary download confusion

症状：

- 第一次 `offckb node` 输出 missing-binary 或类似错误的信息。

可能原因：

- 在验证机器上，第一次运行会下载所需 CKB binary，然后继续启动。

修复：

- 继续阅读输出，直到进程到达启动信号或退出。不要把第一行看起来吓人的输出当作最终结果。

验证命令：

```bash
offckb node
```

预期输出：

- 进程持续运行，并最终输出 `CKB devnet RPC Proxy server running on http://127.0.0.1:28114`

PASS：

- 节点到达启动信号并保持运行

FAIL：

- 进程没有启动信号就退出；记录最后的错误块

## Warning-looking startup output

症状：

- 启动输出有 warning 风格的内容，新手以为节点失败。

可能原因：

- 不是所有 warning 风格的行都是致命错误；验证日志中也记录过 warning 后成功启动的情况。

修复：

- 检查进程是否继续运行并到达预期启动信号。

验证命令：

```bash
offckb node
```

预期输出：

- 运行中的进程和 devnet RPC proxy 启动信号

PASS：

- 进程保持运行，并且另一个终端可以查询本地 RPC

FAIL：

- 进程退出，或从未到达启动信号

## Local node process stopped

症状：

- 本地 RPC 请求 connection refused、空响应或超时。

可能原因：

- `offckb node` 未运行、被中断，或运行状态与预期不一致。

修复：

- 一个终端保持 `offckb node` 运行，另一个终端运行 RPC 请求。

验证命令：

```bash
echo '{"id":2,"jsonrpc":"2.0","method":"get_tip_block_number","params":[]}' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

预期输出：

- JSON 输出包含 `"jsonrpc":"2.0"` 和 `"result"`

PASS：

- 本地 RPC 返回有效 JSON-RPC

FAIL：

- 重启节点并记录两个终端的输出

## RPC endpoint opened in a browser

症状：

- 浏览器打开端点后返回 `Used HTTP Method is not allowed. POST or OPTIONS is required`。

可能原因：

- 使用了浏览器 GET 请求，而不是 JSON-RPC POST 请求。

修复：

- 使用文档中的 curl POST 命令。

验证命令：

```bash
echo '{"id":2,"jsonrpc":"2.0","method":"get_tip_block_number","params":[]}' \
| curl -H 'content-type: application/json' -d @- \
https://testnet.ckb.dev/rpc
```

预期输出：

- JSON 输出包含 `"jsonrpc":"2.0"` 和 `"result"`

PASS：

- POST 请求成功

FAIL：

- 继续查看 Network/DNS 或 Invalid JSON-RPC response

## Invalid JSON-RPC response

症状：

- 收到 HTML、空输出、method error，或没有 `jsonrpc` 和 `result` 的 body。

可能原因：

- HTTP 方法错误、JSON malformed、端点错误，或端点不是预期的 CKB RPC 服务。

修复：

- 完整复制文档中的 POST 请求并重试，不要先改端口或字段。

验证命令：

```bash
echo '{"id":2,"jsonrpc":"2.0","method":"get_tip_block_number","params":[]}' \
| curl -H 'content-type: application/json' -d @- \
https://testnet.ckb.dev/rpc
```

预期输出：

- JSON 输出包含 `"jsonrpc":"2.0"` 和 `"result"`

PASS：

- 响应符合 JSON-RPC 结构

FAIL：

- 记录完整响应 body 和端点

## Low block number misread as failure

症状：

- 响应包含低值，例如 `"result":"0x0"`，新手以为失败。

可能原因：

- 把 block number 当成成功信号，而不是检查 JSON-RPC 响应结构。

修复：

- 先检查结构。对本指南来说，有效 JSON-RPC 和 `result` 字段就是成功信号。

验证命令：

```bash
echo '{"id":2,"jsonrpc":"2.0","method":"get_tip_block_number","params":[]}' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

预期输出：

- JSON 输出包含 `"jsonrpc":"2.0"` 和 `"result"`，即使 result 值较低

PASS：

- JSON-RPC 结构有效

FAIL：

- 查看 Invalid JSON-RPC response

## Wrong network or wrong endpoint

症状：

- 命令成功，但你不知道请求打到了 public testnet、本地 RPC，还是启动日志里的 proxy port。

可能原因：

- 在完成一个路径前切换了路径或端点。

修复：

- 记录端点，完成当前路径，然后再比较其他端点。

验证命令：

```bash
echo '{"id":2,"jsonrpc":"2.0","method":"get_tip_block_number","params":[]}' \
| curl -H 'content-type: application/json' -d @- \
https://testnet.ckb.dev/rpc
```

预期输出：

- 来自命令中所示端点的 JSON-RPC 响应

PASS：

- 你能说出产生响应的具体端点

FAIL：

- 回到 [分支路径](branching-paths.md)，一次只选择一个路径

## Indexer health check fails

症状：

- `get_indexer_tip` 没有返回包含 `block_hash` 和 `block_number` 的 `result` 对象。

可能原因：

- 本地节点路径未运行、端点错误，或 indexer-backed service 尚未就绪。

修复：

- 先确认 Path B 通过，保持 `offckb node` 运行，再重跑 indexer health check。

验证命令：

```bash
echo '{"id":2,"jsonrpc":"2.0","method":"get_indexer_tip"}' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

预期输出：

- JSON 输出包含 `result.block_hash` 和 `result.block_number`

PASS：

- 本地 indexer health check 返回预期 result 对象

FAIL：

- 记录端点和完整响应，然后回到 [Path C. Full Local Check](branching-paths.md#path-c-full-local-check)
