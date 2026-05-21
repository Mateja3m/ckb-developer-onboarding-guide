# Proposal Coverage Map

This page maps the proposal baseline to public repository files.
It exists so reviewers can verify what is in scope without using old progress reports as the reader-facing guide.

## Reader-Facing Beginner Path

| Proposal item | Public location | Status |
| --- | --- | --- |
| Step-by-step onboarding process | [Quick Start](quick-start.md), [Branching Paths](branching-paths.md) | Published |
| Environment configuration guidance | [Quick Start](quick-start.md), [How to Verify](how-to-verify.md), [Environment Setup](reference/environment-setup.md) | Published |
| CKB node setup | [Path B. Local Node](branching-paths.md#path-b-local-node), [CKB Node Setup](reference/ckb-node-setup.md) | Published |
| RPC setup and first successful interaction | [Quick Start](quick-start.md), [RPC Basics](reference/rpc-setup.md) | Published |
| Indexer configuration and health check | [Path C. Full Local Check](branching-paths.md#path-c-full-local-check), [Indexer Setup](reference/indexer-setup.md) | Published |
| Troubleshooting and fix matrix | [Troubleshooting Matrix](troubleshooting-matrix.md), [Common Errors And Remediation](reference/common-errors-and-remediation.md) | Published |
| First runnable developer workflow | [First Developer Workflow](reference/first-developer-workflow.md) | Published |
| AI-assisted debugging guidance | [AI-Assisted Debugging](reference/ai-assisted-debugging.md) | Published |
| CKB mental model | [CKB Mental Model](reference/ckb-mental-model.md) | Published |
| Common misconceptions | [Common Misconceptions](reference/common-misconceptions.md) | Published |
| Bilingual English and Chinese guide | [Chinese Guide](zh-cn/README.md) | Published |
| Verification and evidence | [How to Verify](how-to-verify.md), [Validation Findings](validation/), [Validation Logs](../validation-logs/) | Published |

## Review Boundary

The main path is intentionally short:

1. [Quick Start](quick-start.md)
2. [Branching Paths](branching-paths.md)
3. [Troubleshooting Matrix](troubleshooting-matrix.md)
4. [FAQ](faq.md)
5. [How to Verify](how-to-verify.md)

The longer pages under [reference](reference/README.md) are public, but optional.
They support proposal auditability without forcing new users to read every background section before their first RPC success.

## What This Guide Proves

The guide proves that a beginner can follow a documented path to:

- check local terminal and HTTPS readiness
- call a public CKB testnet RPC endpoint
- start the repository-validated local node path
- receive a valid local JSON-RPC response
- run a basic local indexer health check
- classify common beginner failures before guessing fixes

## What This Guide Does Not Prove

The guide does not prove:

- contract development readiness
- CCC SDK integration readiness
- production deployment readiness
- every operating system variant
- every hosted RPC or indexer provider variant

Those areas are deliberately outside the current onboarding scope.
