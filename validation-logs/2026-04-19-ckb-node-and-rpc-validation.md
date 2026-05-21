# Validation Log

## Metadata

- Date: 2026-04-19
- Tester: Milan Matejic
- Section being validated: Milestone 1 node and RPC rerun
- Source used: Local Milestone 1 verification commands
- Operating system: macOS (shell prompt indicates local macOS workstation)

## Command Executed

```bash
offckb --help
```

## Observed Output

```text
Usage: offckb [options] [command]

ckb development network for your first try

Options:
  -V, --version                                 output the version number
  -h, --help                                    display help for command

Commands:
  node [options] [CKB-Version]                  Use the CKB to start devnet
  create [options] [project-name]               Create a new CKB Smart Contract project in JavaScript.
  deploy [options]                              Deploy contracts to different networks, only supports devnet and testnet
  debug [options]                               Quickly debug transaction with tx-hash
  system-scripts [options]                      Print/Output system scripts of the CKB blockchain
  clean [options]                               Clean the devnet data, need to stop running the chain first
  accounts                                      Print account list info
  deposit [options] [toAddress] [amountInCKB]   Deposit CKB tokens to address, only devnet and testnet
  transfer [options] [toAddress] [amountInCKB]  Transfer CKB tokens to address, only devnet and testnet
  transfer-all [options] [toAddress]            Transfer All CKB tokens to address, only devnet and testnet
  balance [options] [toAddress]                 Check account balance, only devnet and testnet
  debugger                                      Port of the raw CKB Standalone Debugger
  config <action> [item] [value]                do a configuration action
  devnet                                        Devnet utility commands
  help [command]                                display help for command
```

## Failure Cases

- None

## Confusion Points

- A beginner may not know which commands matter for the first successful onboarding pass.

## Possible Root Cause (Optional)

- N/A

## Notes

- Confirms the CLI is installed and visible in the current shell.

---

## Command Executed

```bash
offckb node --help
```

## Observed Output

```text
Usage: offckb node [options] [CKB-Version]

Use the CKB to start devnet

Options:
  --network <network>             Specify the network to deploy to (default: "devnet")
  -b, --binary-path <binaryPath>  Specify the CKB binary path to use, only for devnet, when set, will ignore version and network
  -h, --help                      display help for command
```

## Failure Cases

- None

## Confusion Points

- A beginner may not know when to use `--binary-path` versus the default flow.

## Possible Root Cause (Optional)

- N/A

## Notes

- Re-confirms the validated default network shown by the local help output is `devnet`.

---

## Command Executed

```bash
offckb clean --help
```

## Observed Output

```text
Usage: offckb clean [options]

Clean the devnet data, need to stop running the chain first

Options:
  -d, --data  Only remove chain data, keep devnet config files
  -h, --help  display help for command
```

## Failure Cases

- None

## Confusion Points

- A beginner may still be unsure what counts as "chain data" versus configuration files.

## Possible Root Cause (Optional)

- N/A

## Notes

- Re-confirms the local help text tells the user to stop the running chain before cleanup.

---

## Command Executed

```bash
offckb devnet --help
```

## Observed Output

```text
Usage: offckb devnet [options] [command]

Devnet utility commands

Options:
  -h, --help        display help for command

Commands:
  config [options]  Open a full-screen editor to tweak devnet config files
  help [command]    display help for command
```

## Failure Cases

- None

## Confusion Points

- A beginner may assume this means config editing is required for first success even though Milestone 1 does not require that.

## Possible Root Cause (Optional)

- N/A

## Notes

- Re-confirms the presence of the devnet config surface without requiring file-level editing.

---

## Command Executed

```bash
npm install -g @offckb/cli
```

## Observed Output

```text
changed 194 packages in 24s

33 packages are looking for funding
  run `npm fund` for details
```

## Failure Cases

- None

## Confusion Points

- A beginner may not know whether the funding message matters.
- A beginner may not know whether `changed 194 packages` means install succeeded or replaced an existing copy.

## Possible Root Cause (Optional)

- Existing global installation was updated or refreshed rather than installed for the first time.

## Notes

- Confirms the package remained reachable and installable during this rerun.

---

## Command Executed

```bash
offckb node
```

## Observed Output

```text
Launching CKB devnet Node...
CKB:
2026-04-19 17:48:15.174 +00:00 main WARN ckb_network::network  Customized supported protocols: [Ping, Discovery, Identify, Feeler, DisconnectMessage, Sync, Relay, Time, Alert, LightClient, Filter]

CKB devnet RPC Proxy server running on http://127.0.0.1:28114
```

## Failure Cases

- None

## Confusion Points

- The warning-style log can still look like a failure to a beginner.
- A beginner may still not know how the proxy endpoint relates to the later RPC request endpoint.

## Possible Root Cause (Optional)

- N/A

## Notes

- This rerun was cleaner than the first validated run because it did not include the earlier missing-binary recovery flow.
- Confirms the startup path remains reproducible after the initial setup has already happened.

---

## Command Executed

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "get_tip_block_number",
    "params": []
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

## Observed Output

```text
{"jsonrpc":"2.0","result":"0x2e","id":2}%
```

## Failure Cases

- None

## Confusion Points

- A beginner may not know whether `0x2e` is better than `0x0` or simply a later chain height.
- A beginner may still be confused by the trailing `%` shell prompt marker.

## Possible Root Cause (Optional)

- The local chain had progressed further than in the earlier validation pass before the RPC request was sent.

## Notes

- Confirms the first validated RPC interaction still succeeds on rerun.
- This time the tip block number was nonzero, which supports the documentation note that a successful response is not limited to `0x0`.

---

## Additional Observation

## Observed Output

```text
Used HTTP Method is not allowed. POST or OPTIONS is required
```

## Failure Cases

- Direct browser or GET-style access still does not count as valid RPC verification.

## Confusion Points

- A beginner may still interpret this browser message as proof that the node is broken.

## Possible Root Cause (Optional)

- HTTP method mismatch

## Notes

- The attached screenshot re-confirms the same false-negative pattern seen in the earlier validation pass.

---

## Command Executed

```bash
offckb clean
```

## Observed Output

```text
Chain data cleaned.
```

## Failure Cases

- None in the observed output

## Confusion Points

- The shared transcript does not state explicitly whether the node had already been stopped before cleanup.
- A beginner may incorrectly assume cleanup is part of the required first success path.

## Possible Root Cause (Optional)

- N/A

## Notes

- The local help text still says the running chain should be stopped first, so that guidance should remain in the documentation.
- The successful output confirms cleanup still works in this environment.
