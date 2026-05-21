# Validation Log

## Metadata

- Date: 2026-04-14
- Tester: Milan Matejic
- Section being validated: Initial CKB node setup attempt and basic RPC interaction attempt
- Source used: Official CKB documentation and official OffCKB flow
- Operating system: macOS (Darwin 25.4.0, arm64)

## Command Executed

```bash
npm install -g @offckb/cli
```

## Observed Output

```text
added 194 packages in 21s

33 packages are looking for funding
  run `npm fund` for details
```

## Failure Cases

- None

## Confusion Points

- A beginner may not know whether the funding message is important or can be ignored.

## Possible Root Cause (Optional)

- N/A

## Notes

- Global installation succeeded.
- This confirms the package was reachable and installable in this environment.

---

## Command Executed

```bash
offckb node
```

## Observed Output

```text
/bin/sh: $HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/ckb: No such file or directory
CKB Binary not found, download and install the new version 0.205.0..
downloading https://github.com/nervosnetwork/ckb/releases/download/v0.205.0/ckb_v0.205.0_aarch64-apple-darwin.zip ..
CKB 0.205.0 installed successfully.
Launching CKB devnet Node...
CKB:
2026-04-14 08:22:06.220 +00:00 main WARN ckb_network::network  Customized supported protocols: [Ping, Discovery, Identify, Feeler, DisconnectMessage, Sync, Relay, Time, Alert, LightClient, Filter]

CKB devnet RPC Proxy server running on http://127.0.0.1:28114
```

## Failure Cases

- The command initially reported that the CKB binary was missing.
- The command recovered automatically by downloading and installing the binary.
- No final hard failure occurred in this attempt.

## Confusion Points

- A beginner may interpret `No such file or directory` as a fatal error and stop too early.
- A beginner may not know whether the warning log from `ckb_network::network` is normal or problematic.
- A beginner may not understand the difference between the CKB devnet RPC proxy at `127.0.0.1:28114` and other possible local RPC ports.

## Possible Root Cause (Optional)

- First-run state where the required CKB binary had not been downloaded yet.

## Notes

- This is a valuable onboarding friction point: the command looks like it fails before it self-heals.
- The documentation should explicitly say that the first run may download the binary automatically.
- The documentation should also clarify which endpoint should be used next after the node is launched.

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

- None

## Confusion Points

- A beginner may not know exactly what data was removed.
- A beginner may not know whether the node must be stopped before running this command.

## Possible Root Cause (Optional)

- N/A

## Notes

- The command is simple and produced a clear success message.
- Later docs should explain its effect before recommending its use.

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
{"jsonrpc":"2.0","result":"0x0","id":2}%
```

## Failure Cases

- None for the POST request itself.
- The RPC interaction succeeded and returned a valid JSON-RPC response.

## Confusion Points

- A beginner may not know whether `0x0` is a successful result or a sign that the node has not progressed.
- A beginner may not know why this request uses `http://localhost:8114` while the earlier `offckb node` output mentioned `http://127.0.0.1:28114`.
- The trailing `%` in the shell output may be confusing if the user does not realize it is shell prompt formatting rather than part of the JSON response.

## Possible Root Cause (Optional)

- N/A

## Notes

- This satisfies the project's definition of a first successful RPC interaction.
- Later docs should explain what success looks like in plain language.

---

## Additional Observation

## Observed Output

```text
Used HTTP Method is not allowed. POST or OPTIONS is required
```

## Failure Cases

- A direct browser visit or GET request to the RPC endpoint does not work for this RPC path.

## Confusion Points

- A beginner may try opening the RPC URL in a browser and assume the endpoint is broken.
- A beginner may not understand that the endpoint expects a POST request with a JSON-RPC payload.

## Possible Root Cause (Optional)

- HTTP method mismatch

## Notes

- This should become an explicit onboarding warning in later docs.

---

## Repeatability Check

## Command Executed

```bash
offckb clean
```

## Observed Output

```text
Chain data cleaned.
```

## Failure Cases

- None

## Confusion Points

- A beginner may still not know whether this removes only chain data or also affects installed binaries and configuration.

## Possible Root Cause (Optional)

- N/A

## Notes

- Confirms the cleanup command remains stable on repeat use.

---

## Command Executed

```bash
offckb node
```

## Observed Output

```text
Launching CKB devnet Node...
CKB:
2026-04-14 08:26:41.483 +00:00 main WARN ckb_network::network  Customized supported protocols: [Ping, Discovery, Identify, Feeler, DisconnectMessage, Sync, Relay, Time, Alert, LightClient, Filter]

CKB devnet RPC Proxy server running on http://127.0.0.1:28114
```

## Failure Cases

- None

## Confusion Points

- The warning log still looks error-like and may make a beginner unsure whether startup actually succeeded.

## Possible Root Cause (Optional)

- N/A

## Notes

- This repeat run did not trigger the earlier missing-binary message.
- That suggests the first-run binary download is a one-time onboarding event, while subsequent runs are cleaner.
- This is useful for Week 1 validation because it confirms the local node startup flow is reproducible after initial setup.
