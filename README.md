# CKB Developer Onboarding Guide

Begin here if you want the shortest reproducible path to first CKB success: one valid JSON-RPC response.

This repository keeps the beginner path short, while making the full proposal baseline publicly auditable through reference appendices, validation evidence, reproducibility checks, and Chinese translations.

## Main Path

1. [Quick Start](docs/quick-start.md)
2. [Branching Paths](docs/branching-paths.md)
3. [Troubleshooting Matrix](docs/troubleshooting-matrix.md)
4. [FAQ](docs/faq.md)
5. [How to Verify](docs/how-to-verify.md)

## Proposal Coverage

- [Proposal coverage map](docs/proposal-coverage.md)
- [Reference appendices](docs/reference/README.md)
- [Reviewer reproducibility checklist](docs/third-party-reproducibility.md)
- [Chinese guide](docs/zh-cn/README.md)
- [Validation logs](validation-logs/)

## Success Signals

- Public RPC path: the response includes `"jsonrpc":"2.0"` and `"result"`.
- Local node path: `offckb node` keeps running and local RPC returns valid JSON-RPC.
- Full local path: local RPC and local indexer checks both return valid JSON-RPC.

If a command fails, use the [Troubleshooting Matrix](docs/troubleshooting-matrix.md) before changing endpoints or commands.

## Scope Boundary

This guide proves early onboarding readiness: terminal access, public RPC access, local node startup, local RPC health check, and a basic indexer health check.

It does not claim to teach contract development, CCC SDK integration, production deployment, or full dApp delivery.
