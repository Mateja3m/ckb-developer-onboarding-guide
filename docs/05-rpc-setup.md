# 05. RPC Setup

## Goal

Reach a first successful CKB JSON-RPC response and understand what counts as success for Milestone 1.

## Requirements

Before following this page:

- complete [04. CKB Node Setup](04-ckb-node-setup.md)
- keep the local node process running in a separate terminal
- make sure `curl` works in the terminal where you will send the request

This page is limited to the first validated local RPC interaction recorded in this repository.

- Required: a running local node started through `offckb node`
- Validated: POST requests to `http://localhost:8114` and `http://127.0.0.1:28114` using `get_tip_block_number`
- Validated: a browser-style or GET-style check is not a valid RPC verification step
- Not yet validated: public RPC providers, additional local ports beyond the recorded flow, or additional RPC methods for onboarding

## Validated Facts From This Repository

The Week 1 validation materials confirmed the following:

- the first successful request used `http://localhost:8114`
- the request method was `get_tip_block_number`
- the validated response was `{"jsonrpc":"2.0","result":"0x0","id":2}`
- a later rerun of the same request returned `{"jsonrpc":"2.0","result":"0x2e","id":2}`
- a restart validation on April 20, 2026 showed the same request also succeeding on `http://127.0.0.1:28114` with `{"jsonrpc":"2.0","result":"0xa","id":2}`
- opening the endpoint with the wrong HTTP method produced `Used HTTP Method is not allowed. POST or OPTIONS is required`
- `lsof` validation on April 20, 2026 showed `ckb` listening on `*:8114`
- `lsof` validation on April 20, 2026 showed `node` listening on `*:28114`

The repository also recorded that `offckb node` reported `http://127.0.0.1:28114` during startup. Both that endpoint and `http://localhost:8114` have now returned valid JSON-RPC responses in local validation. On the validation machine, `lsof` also showed `ckb` listening on `8114` and `node` listening on `28114`, which strongly suggests a proxy relationship. The full implementation details are still not documented here, so keep recording the exact endpoint you used.

## Steps

1. Confirm the node is still running.

   Why this matters:

   - The RPC request depends on a live local environment.

   How to verify:

   - The terminal where you launched `offckb node` is still active.
   - You have not stopped or cleaned the node since startup.

2. Use the exact validated request format.

   Run this command in a second terminal:

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

   Why this matters:

   - This request was already captured successfully in the repository's validation log.
   - Using the validated request reduces ambiguity while Milestone 1 is still focused on first success.

   How to verify:

   - The command returns a JSON object.
   - The response includes `"jsonrpc":"2.0"` and `"id":2`.
   - The response includes a `"result"` field with a hex string.

3. Interpret the response as an RPC success check, not as a full environment diagnosis.

   One validated success response was:

   ```json
   {"jsonrpc":"2.0","result":"0x0","id":2}
   ```

   A later validated rerun returned:

   ```json
   {"jsonrpc":"2.0","result":"0x2e","id":2}
   ```

   A later validated request to the startup-reported endpoint returned:

   ```json
   {"jsonrpc":"2.0","result":"0xa","id":2}
   ```

   What this means for Milestone 1:

   - The request reached the local RPC service.
   - The service accepted the JSON-RPC payload.
   - The service returned a valid JSON-RPC response.

   What this does not prove by itself:

   - that every local port is interchangeable
   - that the node is fully progressed beyond its initial chain state
   - that broader developer workflows are already validated

   How to verify:

   - You can explain why the response is considered valid even if the block number is low.

4. Avoid the most common false-negative check.

   Do not verify the RPC endpoint by opening it in a browser and judging the result from a GET request.

   The validation pass recorded this response when the endpoint was accessed the wrong way:

   ```text
   Used HTTP Method is not allowed. POST or OPTIONS is required
   ```

   How to verify:

   - You understand that this message points to an HTTP-method mismatch, not automatically to a broken node.

5. Record the exact endpoint you used.

   Why this matters:

   - The repository already contains evidence that multiple local-looking endpoints can appear during onboarding.
   - Recording the exact endpoint helps avoid later confusion when comparing your notes to startup logs.

   How to verify:

   - Your notes include the full request command and full response.

## Verification

You have completed this page if:

- you sent a POST request with a JSON-RPC payload
- the request returned a valid JSON-RPC response
- you can distinguish between a valid low block number and a transport failure
- you understand that browser access is not the correct RPC validation method here

## Expected Output

At the end of this page, you should have:

- one recorded successful JSON-RPC request
- a clear success condition for Milestone 1
- written evidence of which endpoint and method you actually used

## Common Issues

### Using The Wrong HTTP Method

If you try to test the endpoint in a browser, you may see `Used HTTP Method is not allowed. POST or OPTIONS is required`. In the repository's validation work, that was an expected misuse case, not proof that the RPC layer was unavailable.

### Treating `0x0` As Automatic Failure

The validated first response returned `0x0`. A later rerun returned `0x2e`. Both count as success because the JSON-RPC request and response cycle worked correctly.

### Guessing Which Local Port To Use

This repository has not yet published a full endpoint-routing explanation. Local validation now suggests `8114` is served by `ckb` while `28114` is served by `node`, and both accepted the same JSON-RPC POST request on the validation machine. You should still record which endpoint you used instead of assuming every local port behaves the same way.
