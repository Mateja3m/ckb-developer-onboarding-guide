# CKB Node And RPC Validation Findings

## Goal

Summarize the first real validation pass for initial CKB node setup and basic RPC interaction.

## Findings

- `npm install -g @offckb/cli` succeeded.
- `offckb node` initially reported a missing CKB binary, then automatically downloaded CKB `0.205.0`, installed it, and launched the devnet node.
- The node startup output included a warning log and then reported:
  - `CKB devnet RPC Proxy server running on http://127.0.0.1:28114`
- `offckb clean` succeeded and returned:
  - `Chain data cleaned.`
- A repeat pass of `offckb clean` followed by `offckb node` also succeeded.
- On the repeat pass, the earlier missing-binary message did not appear again.
- The RPC request using `get_tip_block_number` returned:
  - `{"jsonrpc":"2.0","result":"0x0","id":2}`
- A later rerun on April 19, 2026 again showed a clean `offckb node` startup with:
  - `CKB devnet RPC Proxy server running on http://127.0.0.1:28114`
- The April 19, 2026 rerun of the same RPC request returned:
  - `{"jsonrpc":"2.0","result":"0x2e","id":2}`
- On April 20, 2026, the installed CKB binary was discovered at:
  - `/Users/milanmatejic/Library/Application Support/offckb-nodejs/bins/0.205.0/ckb`
- Running that binary with `--version` returned:
  - `ckb 0.205.0 (b75a785 2026-03-17)`
- Running `offckb devnet config` before the devnet config path existed returned:
  - `Devnet config path does not exist: /Users/milanmatejic/Library/Application Support/offckb-nodejs/devnet`
  - `Tip: run offckb node once to initialize devnet config files first.`
- A browser-style or GET-style access pattern produced:
  - `Used HTTP Method is not allowed. POST or OPTIONS is required`
- On April 20, 2026, plain `curl` requests to both `http://localhost:8114` and `http://127.0.0.1:28114` produced the same method error:
  - `Used HTTP Method is not allowed. POST or OPTIONS is required`
- On April 20, 2026, after restarting the node, the JSON-RPC POST request to `http://localhost:8114` returned:
  - `{"jsonrpc":"2.0","result":"0x0","id":2}`
- On April 20, 2026, the same JSON-RPC POST request to `http://127.0.0.1:28114` returned:
  - `{"jsonrpc":"2.0","result":"0xa","id":2}`
- On April 20, 2026, `curl -i` checks showed both `http://localhost:8114` and `http://127.0.0.1:28114` returning:
  - `HTTP/1.1 200 OK`
  - `content-type: application/json`
  - valid JSON-RPC bodies for `get_tip_block_number`
- On April 20, 2026, `lsof -nP -iTCP:8114 -sTCP:LISTEN` showed:
  - `ckb` listening on `*:8114`
- On April 20, 2026, `lsof -nP -iTCP:28114 -sTCP:LISTEN` showed:
  - `node` listening on `*:28114`
- On April 20, 2026, running `offckb node -b "/Users/milanmatejic/Library/Application Support/offckb-nodejs/bins/0.205.0/ckb"` returned:
  - `Using custom CKB binary path: "/Users/milanmatejic/Library/Application Support/offckb-nodejs/bins/0.205.0/ckb"`
  - `CKB devnet RPC Proxy server running on http://127.0.0.1:28114`
- On April 20, 2026, a filesystem check showed the devnet path now existed at:
  - `/Users/milanmatejic/Library/Application Support/offckb-nodejs/devnet`
  - including `ckb.toml`, `ckb-miner.toml`, and the `data` directory

## Interpretation

- The onboarding path is viable on this machine.
- The first node startup experience contains a misleading early error-looking message before recovery.
- The node startup flow appears reproducible after the first-run binary installation has completed.
- The difference between `127.0.0.1:28114` and `localhost:8114` is likely to confuse beginners and should be explained explicitly.
- The first RPC success condition is real, and successful responses can include different tip heights such as `0x0` or `0x2e` depending on chain state and timing.
- Both `localhost:8114` and `127.0.0.1:28114` accepted the same JSON-RPC POST request in local validation.
- Both endpoints also returned normal HTTP `200 OK` responses with JSON content during header-level validation.
- A `ckb` process was directly observed listening on port `8114`.
- A `node` process was directly observed listening on port `28114`.
- Taken together, the local evidence strongly suggests that `28114` is a Node.js-facing proxy layer in front of the `ckb` listener on `8114`.
- The custom `--binary-path` startup flow works on the validation machine when pointed at the discovered local binary.
- The devnet config/data path can exist after initialization and is not only a hypothetical location from help text.
- The installed CKB binary location can be discovered locally instead of being guessed.
- The `offckb devnet config` surface exists, but it may require prior initialization before it can open a config editor successfully.
- The RPC endpoint behavior is easy to misinterpret if a beginner tests it in a browser instead of with a POST request.

## Documentation Implications

- Add a note that `offckb node` may auto-download the required CKB binary on first run.
- Add a note that early output may look like a failure before the tool recovers.
- Add a note that subsequent node launches may look simpler than the first-run experience.
- Explain clearly which local endpoint should be used in each step and why different ports may appear.
- Add a note that both recorded local endpoints accepted the same JSON-RPC POST request in local validation, while the deeper relationship between them still needs explanation.
- Add a note that both endpoints returned HTTP `200 OK` with JSON-RPC payloads during validation.
- Add a note that local process inspection showed `ckb` on `8114` and `node` on `28114`, which is a useful beginner-facing explanation for why both ports can work.
- Add a note that the `--binary-path` startup option has now been validated with the discovered local binary path.
- Add a note that the devnet config/data path can appear after initialization and can be inspected without editing files.
- Add a note that the installed binary path can be inspected locally if needed instead of being assumed.
- Add a note that `offckb devnet config` may fail with a missing-path message until the relevant devnet files exist.
- Explain that RPC endpoints are not validated by opening them in a browser.
- Explain that a valid JSON-RPC response can still contain a low or nonzero block number depending on when the request is sent.

## Candidate Future Troubleshooting Entries

- Symptom: `No such file or directory` appears when running `offckb node`
- Symptom: node output shows a warning log during startup
- Symptom: RPC works on one local port while another tool mentions a different local port
- Symptom: browser says `Used HTTP Method is not allowed. POST or OPTIONS is required`
- Symptom: `get_tip_block_number` returns `0x0`
