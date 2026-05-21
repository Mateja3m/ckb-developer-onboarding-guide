# FAQ

## 最快证明指南有效的方法是什么？

运行 [快速开始](quick-start.md) 中的公共 RPC 请求。
当响应包含 `"jsonrpc":"2.0"` 和 `"result"` 字段时，就算成功。

## 第一次成功信号需要本地节点吗？

不需要。
如果你想先走最低成本路径，从 [Path A. Public RPC Only](branching-paths.md#path-a-public-rpc-only) 开始。

## 什么时候切换到本地节点？

当你需要本地控制、本地日志或可复现的 devnet 路径时再切换。
使用 [Path B. Local Node](branching-paths.md#path-b-local-node)。

## 为什么 RPC 端点返回 `POST or OPTIONS is required`？

这通常表示你用错误的 HTTP 方法打开了端点。
回到 [快速开始](quick-start.md#step-2-调用公共-ckb-rpc) 中的 POST 请求。

## `0x0` 这样的低 block number 是否表示失败？

不是。
如果响应是有效 JSON-RPC，步骤就通过。
先查看 [Low block number misread as failure](troubleshooting-matrix.md#low-block-number-misread-as-failure)，只有本地环境仍然不稳定时再查看 [Local node process stopped](troubleshooting-matrix.md#local-node-process-stopped)。

## 应该信任哪个本地端点：`localhost:8114` 还是 `127.0.0.1:28114`？

使用当前步骤文档中的端点，并记录在你机器上实际成功的端点。
如果不确定，先查看 [Wrong network or wrong endpoint](troubleshooting-matrix.md#wrong-network-or-wrong-endpoint)，不要马上切换端口。

## 什么时候需要 indexer 检查？

只有在 Path B 成功后才需要。
本地 indexer 检查属于 [Path C. Full Local Check](branching-paths.md#path-c-full-local-check)。

## 验证证据在哪里？

从 [如何验证](how-to-verify.md) 开始。
当前仓库证据在英文目录：[environment-validation-findings.md](../validation/environment-validation-findings.md) 和 [ckb-node-and-rpc-validation-findings.md](../validation/ckb-node-and-rpc-validation-findings.md)。
