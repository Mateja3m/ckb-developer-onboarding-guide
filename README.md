# CKB Developer Onboarding Guide

Begin here if you want the shortest reproducible path to first CKB success: one valid JSON-RPC response.

## Main Path

1. [Quick Start](docs/quick-start.md)
2. [Branching Paths](docs/branching-paths.md)
3. [Troubleshooting Matrix](docs/troubleshooting-matrix.md)
4. [FAQ](docs/faq.md)
5. [How to Verify](docs/how-to-verify.md)

## Success Signals

- Public RPC path: the response includes `"jsonrpc":"2.0"` and `"result"`.
- Local node path: `offckb node` keeps running and local RPC returns valid JSON-RPC.
- Full local path: local RPC and local indexer checks both return valid JSON-RPC.

If a command fails, use the [Troubleshooting Matrix](docs/troubleshooting-matrix.md) before changing endpoints or commands.
