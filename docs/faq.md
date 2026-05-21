# FAQ

## What is the fastest way to prove the guide works?

Run the public RPC request in [Quick Start](quick-start.md).
You succeeded when the response includes `"jsonrpc":"2.0"` and a `"result"` field.

## Do I need a local node for the first success signal?

No.
Start with [Path A. Public RPC Only](branching-paths.md#path-a-public-rpc-only) if you want the cheapest path.

## When should I switch to a local node?

Switch when you need local control, local logs, or a reproducible devnet path.
Use [Path B. Local Node](branching-paths.md#path-b-local-node).

## Why did the RPC endpoint say `POST or OPTIONS is required`?

That usually means the endpoint was opened with the wrong HTTP method.
Return to the documented POST request in [Quick Start](quick-start.md#step-2-call-public-ckb-rpc).

## Does a low block number such as `0x0` mean the step failed?

No.
If the response is valid JSON-RPC, the step passed.
Use [Low block number misread as failure](troubleshooting-matrix.md#low-block-number-misread-as-failure) first, then [Local node process stopped](troubleshooting-matrix.md#local-node-process-stopped) only if the local environment still looks unstable.

## Which local endpoint should I trust: `localhost:8114` or `127.0.0.1:28114`?

Use the documented endpoint for the current step and record the one that actually worked on your machine.
If you are unsure, use [Wrong network or wrong endpoint](troubleshooting-matrix.md#wrong-network-or-wrong-endpoint) before changing ports.

## When do I need the indexer check?

Use it only after Path B works.
The local indexer check is part of [Path C. Full Local Check](branching-paths.md#path-c-full-local-check).

## Where is the verification evidence in this repo?

Start with [How to Verify](how-to-verify.md).
The current repository evidence is stored in [environment-validation-findings.md](validation/environment-validation-findings.md) and [ckb-node-and-rpc-validation-findings.md](validation/ckb-node-and-rpc-validation-findings.md).
