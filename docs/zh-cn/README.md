# CKB 开发者入门指南

如果你想用最短、可复现的方式完成第一次 CKB 成功交互，请从这里开始：获得一次有效的 JSON-RPC 响应。

本中文版本对应英文主路径。更长的参考材料、验证日志和周报仍保留在英文目录中，以便审核 proposal baseline。

## 主路径

1. [快速开始](quick-start.md)
2. [分支路径](branching-paths.md)
3. [故障排查矩阵](troubleshooting-matrix.md)
4. [FAQ](faq.md)
5. [如何验证](how-to-verify.md)

## 验证范围

仓库维护者提供的验证日志来自 macOS arm64。
其他操作系统需要通过 community cold-start test 来补充验证。
本指南已经加入 Windows PowerShell 的 RPC 命令写法，但 Windows 仍需要 cold-start 结果后才算已验证。

## Proposal 覆盖范围

- [Proposal 覆盖地图](proposal-coverage.md)
- [英文参考附录](../reference/README.md)
- [第三方复现检查表](../third-party-reproducibility.md)
- [Community testing guide](../contributing/test-the-guide.md)
- [英文验证证据](../validation/)
- [验证日志](../../validation-logs/)

## Community Testing

如果你是 CKB 新用户并尝试本指南，欢迎打开 `Cold Start Guide Test` issue，记录你的操作系统、尝试的路径、第一次卡住的位置以及看到的完整输出。

## 成功信号

- 公共 RPC 路径：响应包含 `"jsonrpc":"2.0"` 和 `"result"`。
- 本地节点路径：`offckb node` 持续运行，并且本地 RPC 返回有效 JSON-RPC。
- 完整本地路径：本地 RPC 和本地 indexer 检查都返回有效 JSON-RPC。

如果命令失败，请先查看 [故障排查矩阵](troubleshooting-matrix.md)，不要马上更换端点或命令。

## 范围边界

本指南验证的是早期入门能力：终端可用性、公共 RPC 访问、本地节点启动、本地 RPC 健康检查，以及基础 indexer 健康检查。

本指南不声称覆盖合约开发、CCC SDK 集成、生产部署或完整 dApp 开发。
