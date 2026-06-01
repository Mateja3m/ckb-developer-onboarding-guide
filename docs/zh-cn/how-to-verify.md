# 如何验证

完成 [快速开始](quick-start.md) 或 [分支路径](branching-paths.md) 后使用本页。

先运行公共 RPC 检查。
只有当你选择 Path B 或 Path C 时，才运行本地节点或 indexer 检查。

仓库维护者提供的验证日志来自 macOS arm64。
其他操作系统的结果请通过英文页 [Test The Guide](../contributing/test-the-guide.md) 记录。
在 Windows PowerShell 中，请使用 [快速开始](quick-start.md) 和 [分支路径](branching-paths.md) 中的 `curl.exe` 命令写法。

## 证据保存位置

面向 reviewer 的证据保存在英文 `docs/validation/` 文件中。
`validation-logs/` 只用于已经去除个人路径和用户名的可公开复现日志。

已有证据：

- [environment-validation-findings.md](../validation/environment-validation-findings.md)
- [ckb-node-and-rpc-validation-findings.md](../validation/ckb-node-and-rpc-validation-findings.md)
- [community-reproduction-results.md](../validation/community-reproduction-results.md)

独立审核请使用：[Third-Party Reproducibility Checklist](../third-party-reproducibility.md)。

## Step 1. 验证环境

对于低成本公共 RPC 路径，先检查 `curl` 和 HTTPS。

运行：

```bash
curl --version
curl --head https://google.com
```

在 Windows PowerShell 中运行：

```powershell
curl.exe --version
curl.exe --head https://google.com
```

预期输出：

- `curl` 返回版本信息
- `curl --head https://google.com` 返回 HTTP headers
- `HTTP/2 301` 这样的重定向也算成功

PASS：

- 两个命令都返回预期输出

FAIL：

- `curl` 失败：查看 [curl missing](troubleshooting-matrix.md#curl-missing)
- HTTPS 失败：查看 [Network or DNS failure](troubleshooting-matrix.md#network-or-dns-failure)

需要记录的证据：

- 两个命令的输出

## Step 2. 验证公共 RPC 路径

运行 [快速开始](quick-start.md#step-2-调用公共-ckb-rpc) 中的公共 RPC 命令。
如果你在 Windows PowerShell 中测试，请使用该章节里的 PowerShell 写法。

预期输出：

- 响应是 JSON
- 响应包含 `"jsonrpc":"2.0"`
- 响应包含 `"result"`

PASS：

- 公共 RPC 返回有效 JSON-RPC 输出

FAIL：

- 无响应：查看 [Network or DNS failure](troubleshooting-matrix.md#network-or-dns-failure)
- 响应结构不对：查看 [Invalid JSON-RPC response](troubleshooting-matrix.md#invalid-json-rpc-response)
- 端点混淆：查看 [Wrong network or wrong endpoint](troubleshooting-matrix.md#wrong-network-or-wrong-endpoint)

需要记录的证据：

- 完整命令
- 使用的端点
- 完整响应

这是最低成本的复现路径。

## Step 3. 验证本地节点路径

如果你只选择 Path A，请跳过本步骤。

先确认 Path B 或 Path C 需要的本地工具：

```bash
node --version
npm --version
git --version
```

预期输出：

- 每个命令都返回版本信息

PASS：

- 三个命令都返回版本信息

FAIL：

- `node` 失败：查看 [Node.js missing or wrong version](troubleshooting-matrix.md#nodejs-missing-or-wrong-version)
- 其他工具失败：查看 [故障排查矩阵](troubleshooting-matrix.md)

运行 [Path B](branching-paths.md#path-b-local-node) 中的命令。
如果你在 Windows PowerShell 中测试，请使用该章节里的本地 RPC PowerShell 写法。
OffCKB 启动日志会显示 proxy 地址 `127.0.0.1:28114`，但本指南的新手 RPC health check 仍然使用 `http://localhost:8114`。
关于这两个端口的关系，请看英文参考页 [Port Confusion During Startup](../reference/ckb-node-setup.md#port-confusion-during-startup)。

预期输出：

- `offckb --help` 可用
- `offckb node` 持续运行
- 启动输出包含 `CKB devnet RPC Proxy server running on http://127.0.0.1:28114`
- 本地 RPC 返回 `"jsonrpc":"2.0"` 和 `"result"`

PASS：

- 本地节点保持运行，并且本地 RPC 返回有效 JSON-RPC

FAIL：

- `offckb` 失败：查看 [offckb command missing](troubleshooting-matrix.md#offckb-command-missing)
- 本地 RPC 失败：查看 [Local node process stopped](troubleshooting-matrix.md#local-node-process-stopped)
- 响应不清楚：查看 [Invalid JSON-RPC response](troubleshooting-matrix.md#invalid-json-rpc-response)

需要记录的证据：

- 本地工具版本
- `offckb --help` 结果
- 本地节点启动行
- 本地 RPC 命令和响应

## Step 4. 验证本地 Indexer 路径

只有当你选择 Path C 时才运行。

运行 [Path C](branching-paths.md#path-c-full-local-check) 中的命令。
如果你在 Windows PowerShell 中测试，请使用该章节里的 indexer PowerShell 写法。

预期输出：

- 响应包含 `result` 对象
- `result` 包含 `block_hash`
- `result` 包含 `block_number`

PASS：

- 本地 indexer 返回预期的 JSON-RPC result 对象

FAIL：

- 本地服务不可用：查看 [Local node process stopped](troubleshooting-matrix.md#local-node-process-stopped)
- 响应无效：查看 [Invalid JSON-RPC response](troubleshooting-matrix.md#invalid-json-rpc-response)
- 端点混淆：查看 [Wrong network or wrong endpoint](troubleshooting-matrix.md#wrong-network-or-wrong-endpoint)

需要记录的证据：

- indexer 命令
- 使用的端点
- 完整响应

## Review Checklist

提交审核前确认：

- `curl` 和 HTTPS 检查通过
- 公共 RPC 检查通过
- 如果使用 Path B 或 Path C，本地节点证据存在
- 如果使用 Path C，本地 indexer 证据存在
- 每条证据包含命令、端点、输出和日期
- 已记录操作系统
- 已记录终端 shell，尤其是 Windows 上的 PowerShell、PowerShell 7、Git Bash 或 WSL
- 个人 home path 和用户名已经替换为 `$HOME` 和 `<local-user>`
