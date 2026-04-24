# 03. Quick Start

## Goal

Reach a first successful CKB JSON-RPC interaction through the shortest validated local path in this repository.

## Requirements

Before following this page, complete:

- [01. Prerequisites](01-prerequisites.md)
- [02. Environment Setup](02-environment-setup.md)

This quick start is intentionally narrow.

- Required: a working terminal, npm, and `curl`
- Required: enough network access to install `@offckb/cli` and allow the first `offckb node` run to download the CKB binary if it is missing
- Validated: the flow below was recorded in this repository's Week 1 validation logs
- Not yet validated: alternative installation paths, custom node configuration, or non-devnet onboarding flows

If your environment still has unresolved DNS or connectivity problems, stop here and fix those first.

## Steps

1. Install the OffCKB CLI.

   Run:

   ```bash
   npm install -g @offckb/cli
   ```

   This is the exact command that succeeded during the recorded validation pass.

   How to verify:

   - The command exits successfully.
   - npm reports that packages were added.
   - You do not see a package-resolution or permission failure.

2. Start the local devnet node.

   Run:

   ```bash
   offckb node
   ```

   Keep this terminal open. On the first run, the tool may report that the CKB binary is missing, then download it automatically and continue.

   Expected pattern:

   - You may see an early `No such file or directory` line for the missing binary.
   - You may then see download and install messages for CKB.
   - The success signal recorded in validation was:
     - `CKB devnet RPC Proxy server running on http://127.0.0.1:28114`

   How to verify:

   - The command keeps running instead of returning immediately.
   - You eventually see the local devnet RPC proxy message.
   - You do not stop at the first alarming-looking line if later lines show recovery and startup.

3. Open a second terminal for the RPC check.

   Leave the node running in the first terminal.

   Why this matters:

   - The node process needs to stay active while you send the RPC request.
   - Using a second terminal avoids accidentally stopping the node while testing.

   How to verify:

   - The first terminal is still showing the running node process.
   - The second terminal opens in the shell normally.

4. Send the first validated JSON-RPC request.

   Run:

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

   This is the exact request captured in the Week 1 validation log.

   How to verify:

   - You receive a JSON-RPC response instead of a browser page or connection error.
   - The response contains `"jsonrpc":"2.0"` and a `"result"` field.
   - The validation logs already captured successful responses with `0x0` and `0x2e`. Treat those as confirmed success cases, not as the only possible successful block numbers.

5. Interpret the result correctly.

   For this onboarding guide, success means the request was accepted and a valid JSON-RPC response came back from the local CKB environment.

   Important notes:

   - A low block number such as `0x0` can still be a successful first response.
   - A later request may return a higher hex block number such as `0x2e` if the local chain has progressed further.
   - If your shell prints a trailing `%`, that may be shell prompt formatting rather than part of the JSON.
   - Do not test this RPC step by opening the endpoint in a browser. The validation pass recorded `Used HTTP Method is not allowed. POST or OPTIONS is required` when the endpoint was accessed the wrong way.

## Verification

You have completed this quick start if:

- `npm install -g @offckb/cli` succeeded
- `offckb node` stayed running and showed a local startup signal
- the JSON-RPC request returned a valid JSON response
- you understand that first success means "working request and response", not "fully synced development environment"

## Expected Output

At the end of this page, you should have:

- the OffCKB CLI installed locally
- a running local devnet node process
- one successful JSON-RPC request recorded against that local environment

For the detailed explanation of each step, continue with:

- [04. CKB Node Setup](04-ckb-node-setup.md)
- [05. RPC Setup](05-rpc-setup.md)
- [07. Configuration Setup](07-configuration-setup.md)

## Common Issues

### Treating The First Startup Message As A Final Failure

During validation, `offckb node` first reported a missing binary and then recovered by downloading the required CKB version automatically.

### Mixing Up Local Endpoints

The Week 1 validation materials show both `127.0.0.1:28114` and `localhost:8114`. This guide only treats the exact validated request flow as confirmed. Do not substitute ports or endpoints casually.

### Testing RPC In A Browser

The RPC check requires a POST request with a JSON-RPC payload. A browser visit or plain GET request is not a valid verification method for this step.
