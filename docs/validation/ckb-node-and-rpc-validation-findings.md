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
- A browser-style or GET-style access pattern produced:
  - `Used HTTP Method is not allowed. POST or OPTIONS is required`

## Interpretation

- The onboarding path is viable on this machine.
- The first node startup experience contains a misleading early error-looking message before recovery.
- The node startup flow appears reproducible after the first-run binary installation has completed.
- The difference between `127.0.0.1:28114` and `localhost:8114` is likely to confuse beginners and should be explained explicitly.
- The first RPC success condition is real, but the meaning of `0x0` needs clarification for new developers.
- The RPC endpoint behavior is easy to misinterpret if a beginner tests it in a browser instead of with a POST request.

## Documentation Implications

- Add a note that `offckb node` may auto-download the required CKB binary on first run.
- Add a note that early output may look like a failure before the tool recovers.
- Add a note that subsequent node launches may look simpler than the first-run experience.
- Explain clearly which local endpoint should be used in each step and why different ports may appear.
- Explain that RPC endpoints are not validated by opening them in a browser.
- Explain that a valid JSON-RPC response can still contain a low block number during early startup or after a clean chain state.

## Candidate Future Troubleshooting Entries

- Symptom: `No such file or directory` appears when running `offckb node`
- Symptom: node output shows a warning log during startup
- Symptom: RPC works on one local port while another tool mentions a different local port
- Symptom: browser says `Used HTTP Method is not allowed. POST or OPTIONS is required`
- Symptom: `get_tip_block_number` returns `0x0`
