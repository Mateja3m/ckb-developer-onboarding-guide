# 04. CKB Node Setup

## Goal

Install the validated onboarding CLI, start a local CKB devnet node, and recognize the difference between expected startup noise and an actual blocker.

## Requirements

Before following this page, complete:

- [01. Prerequisites](01-prerequisites.md)
- [02. Environment Setup](02-environment-setup.md)

For Milestone 1, this page is intentionally limited to the validated local devnet path captured in this repository.

- Required: npm must work in your current shell
- Required: your machine must be able to download packages and, on first run, any missing CKB binary needed by `offckb node`
- Validated: `npm install -g @offckb/cli`, `offckb node`, and `offckb clean`
- Validated: `offckb node -b <actual-binary-path>` with the discovered local CKB binary path
- Not yet validated: manual CKB binary installation, non-devnet setups, or platform-specific background-service setups

## Validated Facts From This Repository

The Week 1 validation materials confirmed the following:

- `npm install -g @offckb/cli` succeeded
- `offckb node` auto-downloaded CKB `0.205.0` when the binary was missing on first run
- the validated startup signal included `CKB devnet RPC Proxy server running on http://127.0.0.1:28114`
- `offckb clean` succeeded with `Chain data cleaned.`
- `offckb node --help` confirms the following local options exist:
  - `--network <network>`
  - `--binary-path <binaryPath>`
- running `offckb node -b "$ACTUAL_CKB_BIN"` with the discovered local binary path succeeded and showed the same startup signal

These are validated observations from this repository, not a promise that every machine will display identical version numbers or startup timing.

## Steps

1. Install the OffCKB CLI.

   Run:

   ```bash
   npm install -g @offckb/cli
   ```

   Why this matters:

   - This command provides the `offckb` entry point used by the validated onboarding flow.

   How to verify:

   - npm exits successfully.
   - You do not see package-resolution, permission, or network errors.

2. Confirm the CLI is available in your shell.

   Run:

   ```bash
   offckb --help
   ```

   Why this matters:

   - This confirms the installation completed in a way your current terminal session can actually use.

   How to verify:

   - You see usage information for `offckb`.
   - The command list includes `node` and `clean`.

3. Start the local devnet node.

   Run:

   ```bash
   offckb node
   ```

   Why this matters:

   - This is the validated first-run path in the repository.
   - Milestone 1 is focused on reaching a working local node and first RPC success, not on custom node management.

   Expected pattern on first run:

   - The tool may first print a missing-binary line.
   - It may then download and install the CKB binary automatically.
   - It may print a warning-style log before the final startup signal.

   The exact first-run validation output included all of the following patterns:

   - a missing-binary message
   - a download of CKB `0.205.0`
   - a warning log from `ckb_network::network`
   - `CKB devnet RPC Proxy server running on http://127.0.0.1:28114`

   How to verify:

   - The command continues running after startup instead of returning immediately.
   - You eventually see the local devnet RPC proxy message.
   - You do not stop at the first warning-like line if the process continues and reaches the startup signal.

4. Keep the node terminal open.

   Why this matters:

   - The later RPC step depends on the node process still running.

   How to verify:

   - Your terminal still shows the running process.
   - You can open a second terminal without stopping the first one.

5. Use cleanup only when you intentionally want a fresh devnet chain state.

   Run:

   ```bash
   offckb clean
   ```

   The local help text says this command cleans the devnet data and that you need to stop the running chain first.

   Why this matters:

   - Cleanup can be useful for repeatable validation passes.
   - It is not required for a normal first success path.

   How to verify:

   - The command returns `Chain data cleaned.`

## Verification

You are ready to continue to RPC setup if:

- `offckb --help` works in your shell
- `offckb node` reaches a stable running state
- you can identify the startup signal instead of relying on guesswork
- you understand that `offckb clean` is optional and should be used deliberately

## Expected Output

At the end of this page, you should have:

- a working `offckb` CLI in your shell
- a running local devnet node started through the validated onboarding flow
- a clear record of the startup messages that appeared on your machine

If your output differs, record the exact command and output in a validation log before changing anything from memory.

## Common Issues

### Early Missing-Binary Message

The validation pass showed that `offckb node` can begin with what looks like a fatal missing-file error and then recover automatically by downloading the required CKB binary.

### Warning-Looking Startup Logs

The validated startup output included a warning log before the node reported the local RPC proxy. Do not treat every warning-style line as a hard failure without checking whether the process continued to a startup signal.

### Assuming The Startup Port Explains Every Later RPC Step

The node startup log reported `127.0.0.1:28114`, while the first validated RPC request used `localhost:8114`. This repository does not yet document the full internal routing relationship between those endpoints, so follow the validated request flow exactly instead of guessing.
