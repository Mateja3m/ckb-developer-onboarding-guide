# 06. Indexer Setup

## Goal

Understand what an indexer does in CKB development, when you need one, and how to decide between local and hosted indexer access without inventing setup commands that have not yet been validated in this repository.

## Requirements

Before using this page, complete:

- [03. CKB Overview](03-quick-start.md)
- [04. CKB Node Setup](04-ckb-node-setup.md)
- [05. RPC Basics](05-rpc-setup.md)

This page is intentionally documentation-first.

- It explains where an indexer fits into the workflow.
- It includes exact examples only where the repository now contains direct validation evidence.
- Official CKB documentation remains the source of truth for exact indexer installation and provider-specific setup details.

## What An Indexer Is

An indexer is a service that reorganizes chain data into a form that is easier for applications to search.

In beginner terms:

- the node exposes raw blockchain data through RPC
- the indexer helps applications search that data more efficiently
- you usually care about an indexer when your work needs lookup convenience, not just one simple RPC check

## Why Developers Use An Indexer

An indexer becomes useful when you need to:

- search for on-chain objects by address or other criteria
- avoid manually piecing together larger data lookups from basic RPC calls
- support application flows that read more than one small piece of chain state

For a first onboarding pass, an indexer is often optional.
For broader application development, it becomes much more useful.

## When You May Not Need One Yet

You may not need an indexer yet if:

- you are still confirming that the local node starts correctly
- you are still learning what a successful RPC response looks like
- your current goal is only to prove that the environment can reach first chain interaction

That is why the guide introduces the concept now, but does not force indexer setup before the early local node and RPC checks are understood.

## Local Versus Hosted Indexer Choices

### Local Indexer

A local indexer is usually the better choice when:

- you want your read path to match your local devnet workflow
- you want to debug local data behavior without depending on a third-party service
- you want to keep the onboarding environment self-contained

Tradeoffs:

- more setup responsibility
- more moving parts to understand
- more chances for a beginner to confuse node, RPC, and indexer responsibilities

### Hosted Or Shared Indexer

A hosted or shared indexer may be enough when:

- you are only experimenting with read-oriented application behavior
- a tutorial already depends on a known hosted service
- your current work does not require local infrastructure ownership

Tradeoffs:

- less visibility into the underlying system
- more dependency on external service availability
- more risk that a hosted environment behaves differently from your local expectations

## What To Verify Before Treating An Indexer As Ready

Before you assume indexer setup is successful, confirm:

- the node or RPC layer you depend on is already working
- you know whether the indexer is local or hosted
- you know which endpoint or service the application is actually querying
- you can tell the difference between an indexer problem and a node or RPC problem

## Repository-Validated Local Indexer Example

If you are following the repository's local node flow, this repository now validates a local indexer health check through the same local endpoint path.

Run:

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "get_indexer_tip"
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

What success looks like:

- the endpoint returns valid JSON-RPC output
- the response includes a `result` object
- the `result` object includes `block_hash` and `block_number`

## Repository-Validated Public Testnet Indexer Example

This repository also now validates the same indexer health-check concept against a public CKB testnet indexer endpoint.

Run:

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "get_indexer_tip"
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
https://testnet.ckb.dev/indexer
```

What success looks like:

- the endpoint returns valid JSON-RPC output
- the response includes a `result` object
- the `result` object includes `block_hash` and `block_number`

## Common Beginner Mistakes

- assuming an indexer is required before basic node and RPC checks work
- confusing node RPC responses with indexer-backed query behavior
- treating a hosted indexer as if it proves the local environment is fully correct
- adding an indexer too early and then losing track of which service is failing

## Validation Boundaries

This repository now publishes validated local and public indexer health-check examples.

It does not try to document:

- a standalone indexer installation path outside the current onboarding flow
- a broader application-level indexer query guide
- every hosted provider variant a later-stage developer might choose

## Verification

You are aligned with this page if you can explain:

- what an indexer does at a high level
- why it is different from basic node RPC access
- when a beginner can postpone indexer setup
- what a successful `get_indexer_tip` response proves
- when a local or hosted indexer choice changes the debugging story

## Expected Output

At the end of this page, you should have:

- a clear mental model for where the indexer fits
- a practical rule for when not to introduce it too early
- one validated local or public indexer health-check pattern you can reuse during onboarding

## Common Issues

### Adding Too Many Components At Once

If you add node, RPC, indexer, and application logic all at the same time, it becomes much harder to identify which layer actually failed.

### Treating Better Search As Proof Of Correct Setup

An indexer can make data access easier, but it does not replace the need to understand whether the underlying node and RPC path are actually working.
