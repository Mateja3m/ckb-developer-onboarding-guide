# CKB Node Setup

## Goal

Decide whether you need a local CKB node for early development, then follow the repository's validated local-node path without pretending unverified setup variants are already complete.

## Requirements

Before using this page, complete:

- [Prerequisites](prerequisites.md)
- [Environment Setup](environment-setup.md)
- [Quick Start](../quick-start.md)

This page stays conservative on purpose.

- It uses exact commands only where the repository already contains validation evidence.
- It does not claim that every CKB installation path has been tested here.
- It keeps official documentation as the source of truth for commands or options not already validated locally.

## When A Local Node Is Needed

A local node is usually the better choice when:

- you want a self-contained beginner environment
- you need to confirm that node startup and RPC behavior work together on your own machine
- you are validating a local devnet workflow instead of only reading remote chain data
- you want to reproduce onboarding steps without depending on a third-party endpoint

## When A Public Or Shared RPC Endpoint May Be Enough

A local node may not be necessary when:

- you only need to read chain data for a simple experiment
- the tutorial you are following clearly supports a remote RPC endpoint
- you are not yet testing local process management, local chain state, or devnet behavior

This guide does not yet document a fully validated public RPC path. If you choose that route, verify the exact endpoint and onboarding steps against official CKB documentation before treating it as part of this repository's validated flow.

## What Is Already Validated In This Repository

The local validation notes in this repository already confirmed:

- `npm install -g @offckb/cli` succeeded
- `offckb --help` exposed the expected CLI surface
- `offckb node` started a local devnet flow
- on first run, `offckb node` auto-downloaded a missing CKB binary on the validation machine
- the startup output reported `CKB devnet RPC Proxy server running on http://127.0.0.1:28114`
- `offckb clean` succeeded when used deliberately as cleanup

These are repository-validated observations, not a blanket claim about every operating system or every CKB setup path.

## High-Level Preparation

Before you run the local-node path, confirm that:

- Node.js and npm work in your shell
- package installation from npm is available on your machine
- you have enough network access for the first tool download path used by this repository
- you are ready to keep one terminal open for the running node process

Before finalizing or publishing broader installation guidance, verify the following against official CKB documentation:

- `TODO: verify against official CKB documentation before finalizing.` Recommended beginner installation path outside the specific OffCKB flow already validated here.
- `TODO: verify against official CKB documentation before finalizing.` Supported operating-system notes that should appear in a public-facing setup guide.
- `TODO: verify against official CKB documentation before finalizing.` Whether any newer recommended local setup flow should replace or supplement the current repository-validated path.

## Repository-Validated Local Path

1. Install the onboarding CLI already validated in this repository.

   Run:

   ```bash
   npm install -g @offckb/cli
   ```

   What success looks like:

   - npm exits successfully
   - the install completes without permission or package-resolution failure

2. Confirm the CLI is available in your current shell.

   Run:

   ```bash
   offckb --help
   ```

   What success looks like:

   - help output appears
   - the command list includes `node`

3. Start the local node path already recorded in the validation notes.

   Run:

   ```bash
   offckb node
   ```

   What success looks like:

   - the process keeps running instead of exiting immediately
   - the startup flow reaches a message containing `CKB devnet RPC Proxy server running on http://127.0.0.1:28114`

   Important beginner note:

   - the validation notes show that the first run can print an error-looking missing-binary message before recovering and downloading the required CKB binary

4. Keep that terminal open while you move to RPC checks.

   Why this matters:

   - the next page depends on the node process still being active

5. Use cleanup only when you intentionally want a fresh local state.

   Run:

   ```bash
   offckb clean
   ```

   Use this only after stopping the running local chain. The repository validation notes recorded `Chain data cleaned.` as the success signal for this command.

## Common Beginner Mistakes

- assuming a public RPC endpoint and a local node serve the same onboarding purpose
- stopping the node terminal before running the RPC check
- treating the first warning-style startup line as the final outcome
- changing ports or options before reaching one known-good baseline
- copying commands from memory instead of from the validated notes or official docs

## Verification Checklist

You are ready to continue if:

- you know whether you are choosing a local node path or an RPC-only path
- `npm install -g @offckb/cli` succeeded on your machine if you chose the validated local path
- `offckb --help` works in your shell
- `offckb node` reaches a stable running state
- you can identify the startup signal instead of guessing from partial logs

## Expected Output

At the end of this page, you should have:

- a clear reason for using a local node or not using one yet
- one working local-node startup path if you followed the validated repository flow
- a short written record of the startup message and any unusual first-run behavior

## Common Issues

### Early Missing-Binary Message

The validation notes show that the first local run can begin with a missing-file style message before recovering automatically. Do not assume the first alarming line is the final result.

### Port Confusion During Startup

The startup output recorded in this repository mentions `127.0.0.1:28114`. Later RPC checks in the repository also use `localhost:8114`. The next page explains how to interpret that carefully without assuming both values mean the same thing in every context.

### Treating This Page As Full Installation Documentation

This page documents the first repository-validated onboarding path. It does not yet replace official CKB installation references for broader setups, alternate networks, or production-oriented node operation.
