# 05. RPC Basics

## Goal

Understand what RPC means in CKB development, how local and public RPC access differ, and how to interpret a first successful health-check response.

## Requirements

Before using this page:

- complete [03. CKB Overview](03-quick-start.md)
- decide whether you are using the repository's local-node path or a separately verified remote endpoint
- keep the local node running if you are following the validated local flow

This page includes exact request examples only where the repository already contains direct validation evidence.

## What RPC Means

RPC stands for Remote Procedure Call.

In practical CKB development, RPC is the interface a script, tool, or developer uses to ask a node for information or submit a request. Instead of clicking through a graphical interface, you send a structured request and read a structured response.

## Why RPC Matters In CKB Development

RPC matters because it is one of the first concrete proof points that your setup is working.

If you can send a valid request and receive a valid response, you know at least one important part of the chain-access path is alive:

- your terminal command ran
- your endpoint was reachable
- your request format was accepted
- the node or proxy returned real JSON-RPC data

That does not prove every later workflow is ready, but it is an important early success signal.

## Local RPC Versus Public RPC

Local RPC usually means:

- you started the node or a local proxy on your own machine
- you control the local process lifecycle
- you can inspect startup logs directly
- you can test a local devnet flow without relying on a shared service

Public or shared RPC usually means:

- someone else operates the endpoint
- you depend on the remote service being reachable and suitable for your tutorial or workflow
- you may be able to read data without running local infrastructure
- you have less visibility into the underlying process and local configuration

This repository now validates both:

- a local RPC onboarding path through the repository's local node flow
- a public testnet RPC onboarding path using a shared CKB testnet endpoint

## Basic Health-Check Concept

A health check in this guide means sending a simple RPC request that is easy to interpret.

The repository validation notes already used `get_tip_block_number` for that purpose. It is useful because:

- it is simple
- it returns a direct value
- it helps confirm the endpoint is answering JSON-RPC requests at all

## Repository-Validated Local Example

If you are following the local flow already validated in this repository, run:

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

The repository validation notes also recorded the same JSON-RPC POST request succeeding against `http://127.0.0.1:28114` on the validation machine. The guide still treats `http://localhost:8114` as the primary example because that request already existed in the earlier repo flow and is easier to keep consistent.

## Repository-Validated Public Testnet Example

The same health-check request was also validated against a public CKB testnet RPC endpoint.

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
https://testnet.ckb.dev/rpc
```

What success looks like:

- the endpoint returns valid JSON-RPC output
- the response includes `"jsonrpc":"2.0"` and a `"result"` field
- the exact tip block number can vary from one request to the next

## What A Successful Response Means

A successful response usually means:

- the request reached a listening endpoint
- the endpoint accepted your JSON-RPC structure
- the node or proxy returned a valid JSON response

The repository validation notes recorded successful responses such as:

- `{"jsonrpc":"2.0","result":"0x0","id":2}`
- `{"jsonrpc":"2.0","result":"0x2e","id":2}`
- `{"jsonrpc":"2.0","result":"0xa","id":2}`

For this guide, those different block numbers all count as success because the important signal is the valid request-and-response cycle.

## What Failure Usually Means

Failure usually falls into one of these categories:

- the endpoint is not running or not reachable
- the request used the wrong HTTP method
- the JSON-RPC payload was malformed
- the wrong port or endpoint was tested
- a local process stopped earlier than expected

The repository validation notes recorded this response when the endpoint was accessed with the wrong method:

```text
Used HTTP Method is not allowed. POST or OPTIONS is required
```

That message points to a request-method problem, not automatically to a broken CKB environment.

## Conceptual Examples

Conceptually, early RPC usage often looks like one of these patterns:

- a health check asks for the current tip block number
- a tool asks for chain state before doing deeper work
- a developer compares whether the same request works locally but fails against another endpoint

This guide keeps those examples conceptual unless the repository already contains the exact request and response being discussed.

## Milestone 2 Local Checkpoint

Before moving on, confirm these points from the existing onboarding flow:

- Node.js and npm still work in the shell you are using
- Git still works in that environment
- terminal basics are no longer a blocker, including keeping the node terminal separate from the RPC terminal when needed
- the local node is still running if you chose the local-node path
- you already reached at least one successful RPC response with the validated request
- you wrote down which endpoint actually worked on your machine
- you can still follow official documentation carefully when this repository marks a detail for later verification
- you can roughly classify a failure as a tool issue, shell issue, network issue, endpoint issue, request-method issue, or response-interpretation issue

If you need to rerun the tool checks, use the exact commands already listed in the prerequisites page. If you need to rerun the RPC health check, use the validated `get_tip_block_number` request shown above instead of inventing a new test.

## Verification

You are ready to continue if:

- you can explain what RPC is in plain language
- you understand why a valid JSON response counts as an early success signal
- you can describe the difference between local RPC and public RPC
- you can recognize that the same health-check pattern can work against either a validated local endpoint or a validated shared testnet endpoint
- you know that a low block number is not, by itself, a failure

## Expected Output

At the end of this page, you should have:

- one clear mental model for what the RPC layer does
- one validated health-check request, either against the local path or the shared testnet path documented here
- a short explanation of what success and failure usually mean

## Common Issues

### Using A Browser As The RPC Test

A browser-style GET request is not the same as a JSON-RPC POST request. The repository validation notes explicitly recorded the method-mismatch error for this misuse case.

### Treating Any Nonzero Or Low Result As The Main Signal

For the first health check, the key signal is a valid JSON-RPC response. The exact block number can vary with local chain state and timing.

### Assuming Local And Public RPC Behave The Same Way

They can support similar request formats, but they are not the same onboarding environment. Local RPC gives you process visibility and reproducibility. Public RPC shifts some of that control to an external service.
