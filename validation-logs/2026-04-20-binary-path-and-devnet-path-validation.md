# Validation Log

## Metadata

- Date: 2026-04-20
- Tester: repository maintainer
- Section being validated: Custom binary-path startup and initialized devnet path presence
- Source used: Milestone 1 follow-up validation commands
- Operating system: macOS (shell prompt indicates local macOS workstation)

## Command Executed

```bash
ACTUAL_CKB_BIN="$(find "$HOME/Library/Application Support/offckb-nodejs" -type f -name ckb 2>/dev/null | head -n 1)"
printf '%s\n' "$ACTUAL_CKB_BIN"
```

## Observed Output

```text
$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/ckb
```

## Failure Cases

- None

## Confusion Points

- A beginner may not know whether this discovered path is machine-specific or expected across installations.

## Possible Root Cause (Optional)

- N/A

## Notes

- Re-confirms the discovered local binary path used for the custom startup test.

---

## Command Executed

```bash
offckb node -b "$ACTUAL_CKB_BIN"
```

## Observed Output

```text
Using custom CKB binary path: "$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/ckb"
Launching CKB devnet Node...
CKB:
2026-04-20 06:55:31.141 +00:00 main WARN ckb_network::network  Customized supported protocols: [Ping, Discovery, Identify, Feeler, DisconnectMessage, Sync, Relay, Time, Alert, LightClient, Filter]

CKB devnet RPC Proxy server running on http://127.0.0.1:28114
```

## Failure Cases

- None

## Confusion Points

- A beginner may not know whether using `--binary-path` changes the rest of the devnet behavior or only selects a binary location.

## Possible Root Cause (Optional)

- N/A

## Notes

- Confirms the custom `--binary-path` startup flow works with the discovered local binary path on the validation machine.

---

## Command Executed

```bash
find "$HOME/Library/Application Support/offckb-nodejs" -maxdepth 3 -mindepth 1 | sort
```

## Observed Output

```text
$HOME/Library/Application Support/offckb-nodejs/bins
$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0
$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/CHANGELOG.md
$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/COPYING
$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/README.md
$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/ckb
$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/ckb-cli
$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/docs
$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/init
$HOME/Library/Application Support/offckb-nodejs/devnet
$HOME/Library/Application Support/offckb-nodejs/devnet/check-ckb-started-successfully.sh
$HOME/Library/Application Support/offckb-nodejs/devnet/ckb-miner.toml
$HOME/Library/Application Support/offckb-nodejs/devnet/ckb.toml
$HOME/Library/Application Support/offckb-nodejs/devnet/data
$HOME/Library/Application Support/offckb-nodejs/devnet/data/ancient
$HOME/Library/Application Support/offckb-nodejs/devnet/data/db
$HOME/Library/Application Support/offckb-nodejs/devnet/data/indexer
$HOME/Library/Application Support/offckb-nodejs/devnet/data/logs
$HOME/Library/Application Support/offckb-nodejs/devnet/data/network
$HOME/Library/Application Support/offckb-nodejs/devnet/data/tmp
$HOME/Library/Application Support/offckb-nodejs/devnet/data/tx_pool
$HOME/Library/Application Support/offckb-nodejs/devnet/default.db-options
$HOME/Library/Application Support/offckb-nodejs/devnet/specs
$HOME/Library/Application Support/offckb-nodejs/devnet/specs/always_success
$HOME/Library/Application Support/offckb-nodejs/devnet/specs/anyone_can_pay
$HOME/Library/Application Support/offckb-nodejs/devnet/specs/ckb_js_vm
$HOME/Library/Application Support/offckb-nodejs/devnet/specs/dev.toml
$HOME/Library/Application Support/offckb-nodejs/devnet/specs/nostr_lock
$HOME/Library/Application Support/offckb-nodejs/devnet/specs/omnilock
$HOME/Library/Application Support/offckb-nodejs/devnet/specs/pw-lock
$HOME/Library/Application Support/offckb-nodejs/devnet/specs/secp256k1_blake160_multisig_all_v2
$HOME/Library/Application Support/offckb-nodejs/devnet/specs/spore
$HOME/Library/Application Support/offckb-nodejs/devnet/specs/sudt
$HOME/Library/Application Support/offckb-nodejs/devnet/specs/xudt
```

## Failure Cases

- None

## Confusion Points

- A beginner may not know which of these files are safe to inspect versus edit.
- A beginner may assume the presence of `data/indexer` means full indexer setup is already documented, which is not the case in Milestone 1.

## Possible Root Cause (Optional)

- N/A

## Notes

- Confirms the devnet path exists after initialization on the validation machine.
- Confirms the path contains configuration files and data directories that can be referenced cautiously in documentation without claiming cross-machine stability.
