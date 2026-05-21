# Configuration Setup

## Goal

Explain the minimum configuration awareness a beginner needs for Milestone 1 without inventing file paths, default values, or custom settings that have not been validated in this repository.

## Requirements

Before using this page:

- complete [CKB Node Setup](ckb-node-setup.md)
- complete [RPC Basics](rpc-setup.md)

This page is intentionally conservative.

- Required: understand which local network and endpoint you actually used
- Optional: inspect the CLI help for available configuration-related commands
- Validated: `offckb node --help`, `offckb clean --help`, and `offckb devnet --help`
- Validated: local binary-path discovery and `offckb node -b <actual-binary-path>` on the validation machine
- Not yet validated: direct editing of OffCKB or CKB config files, stable config file locations across environments, or custom port assignments

## What Is Actually Validated

The following configuration-related facts were verified locally in this repository:

- `offckb node --help` shows `--network <network>` with default `"devnet"`
- `offckb node --help` shows `--binary-path <binaryPath>`
- `offckb clean --help` says it cleans devnet data and that the running chain should be stopped first
- `offckb devnet --help` shows a `config` subcommand
- `offckb devnet config` is described by the local CLI help as opening a full-screen editor to tweak devnet config files
- running `offckb devnet config` before the devnet config path exists returns:
  - `Devnet config path does not exist: .../offckb-nodejs/devnet`
  - `Tip: run offckb node once to initialize devnet config files first.`
- the installed local CKB binary can be discovered instead of guessed with a `find` command
- on the validation machine, the discovered path was under `$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/ckb`
- after initialization, the validation machine showed a real devnet path under `$HOME/Library/Application Support/offckb-nodejs/devnet`
- running `offckb node -b "$ACTUAL_CKB_BIN"` with the discovered binary path succeeded on the validation machine

That is enough for Milestone 1 to explain the shape of configuration work.
It is not enough to publish file-level editing instructions yet.

## Milestone 1 Guidance

For a first successful onboarding pass:

- Required: stay on the validated default devnet flow unless you have a specific reason not to
- Required: record the actual endpoint and messages from your own session
- Optional: inspect local help output before making any configuration change
- Not yet validated: changing ports, switching to a different network for the beginner flow, or editing config files directly

## Steps

1. Confirm which network the validated onboarding flow expects.

   Run:

   ```bash
   offckb node --help
   ```

   How to verify:

   - The help output shows `--network <network>`.
   - The default shown in the local help is `"devnet"`.

2. Confirm which configuration surfaces exist locally before you edit anything.

   Run:

   ```bash
   offckb devnet --help
   offckb clean --help
   ```

   Why this matters:

   - Beginners often edit configuration too early without first identifying which tool owns which setting.
   - For Milestone 1, knowing what commands exist is more important than changing values.

   How to verify:

   - `offckb devnet --help` lists the `config` subcommand.
   - `offckb clean --help` explains the cleanup behavior and the stop-the-chain requirement.

3. Discover the local CKB binary path instead of assuming it.

   Run:

   ```bash
   find "$HOME/Library/Application Support/offckb-nodejs" -type f -name ckb 2>/dev/null | sort
   ```

   Why this matters:

   - It is safer to inspect the actual installed path than to guess where the binary lives.
   - This keeps the guide aligned with the "validation-first" rule.

   How to verify:

   - The command returns one or more real paths on your machine.
   - On the validation machine, the result included a path under `.../offckb-nodejs/bins/0.205.0/ckb`.

4. Confirm whether the expected devnet path now exists after initialization.

   Run:

   ```bash
   find "$HOME/Library/Application Support/offckb-nodejs" -maxdepth 3 -mindepth 1 | sort
   ```

   How to verify:

   - You can see whether a real `.../offckb-nodejs/devnet` path now exists.
   - On the validation machine, that path contained files such as `ckb.toml`, `ckb-miner.toml`, and a `data` directory.

5. Record the values that actually appeared in your run instead of assuming defaults from memory.

   At minimum, write down:

   - the network you used
   - the endpoint that worked for your RPC request
   - any startup port or proxy message shown by the node
   - the CKB version shown if the first run downloaded a binary

   Why this matters:

   - The validation logs already show that the startup message and the first successful RPC request referenced different local addresses.
   - Recording real values is safer than guessing which port or file matters later.

   How to verify:

   - Your setup notes contain exact copied values from your terminal output.

6. Avoid direct configuration editing unless you are validating it deliberately.

   For the beginner onboarding scope, the guide does not instruct you to open or edit config files directly because cross-environment configuration editing belongs outside the first-success path.

   If you test the config surface before initialization, you may see:

   ```text
   Devnet config path does not exist: ...
   Tip: run `offckb node` once to initialize devnet config files first.
   ```

   How to verify:

   - You can reach first RPC success without editing config files manually.

## Verification

You are aligned with Milestone 1 configuration expectations if:

- you know the validated flow is using devnet by default
- you can name the exact endpoint that worked in your environment
- you know how to discover the actual local binary path instead of guessing it
- you understand which configuration areas are still intentionally undocumented
- you have not introduced speculative config edits just to get through first setup

## Expected Output

At the end of this page, you should have:

- a written record of the network and endpoints used during onboarding
- a clear understanding of which CLI configuration surfaces exist
- a clear boundary between validated setup guidance and later configuration work

## Common Issues

### Editing Config Too Early

If you start changing ports, networks, or file contents before you have one successful baseline RPC call, it becomes harder to tell whether the original setup path actually worked.

### Assuming Every Port Mentioned By The Tool Is The Same Thing

The repository's validation evidence shows multiple local endpoint values during startup and RPC testing. Until those relationships are validated more deeply, keep precise notes instead of merging them mentally into one value.

### Treating CLI Help As Full Configuration Documentation

The local help output is useful for identifying what knobs exist. It is not, by itself, a validated beginner-safe editing guide.
