# First Developer Workflow

## Goal

Show one small end-to-end CKB onboarding workflow that a beginner can complete without pretending contract development, deployment, or indexer-backed application logic are already finished.

## Requirements

Before using this page, complete:

- [Prerequisites](prerequisites.md)
- [Environment Setup](environment-setup.md)
- [Quick Start](../quick-start.md)
- [CKB Node Setup](ckb-node-setup.md)
- [RPC Basics](rpc-setup.md)
- [Configuration Setup](configuration-setup.md)

This workflow is intentionally narrow.

- It is not a smart contract build-and-deploy workflow.
- It is not an indexer-backed application workflow.
- It is the first validated happy path from local setup into a confirmed chain interaction.

## The Workflow

### 1. Confirm The Local Developer Environment Is Ready

At this point, the beginner should already have:

- working local tools
- a dedicated onboarding workspace
- a terminal flow they understand

If those basics still feel uncertain, stop here and return to the earlier setup documents.

### 2. Start The Local Node

Use the repository-validated local node flow from the node setup page.

The first success condition is not "everything is fully built."
The first success condition is that the local chain process starts and stays running.

### 3. Keep The Running Process Stable

Do not collapse the workflow by killing the node process too early.

For this guide, an important beginner habit is:

- keep the node running in one terminal
- use a second terminal for the first RPC interaction

### 4. Send One Validated RPC Health Check

Use the repository-validated `get_tip_block_number` request from the RPC basics page.

Why this is the right first workflow checkpoint:

- it proves the local request path works
- it gives the beginner one clear success signal
- it avoids pretending broader application behavior is already validated

### 5. Record What Actually Happened

At minimum, record:

- the exact command you ran
- the exact endpoint you used
- the exact response you received
- whether the node showed any warning-like output before stabilizing

This keeps the workflow reproducible and makes later troubleshooting much easier.

### 6. Stop Before Expanding Scope

After one successful local node start and one successful RPC response, the beginner has completed the first real workflow this guide is trying to teach.

Do not accidentally redefine success too early as:

- full contract development
- full deployment
- full indexing
- production readiness

Those are later workflows.

## What Counts As Success

This workflow counts as successful if:

- the local node starts
- the process remains running long enough to test
- one validated RPC request returns a valid JSON-RPC response
- the developer can explain why the result counts as success

## What This Workflow Does Not Yet Prove

This workflow does not yet prove:

- contract tooling is ready
- deployment is ready
- indexer-backed reads are ready
- every local endpoint relationship is fully understood
- the environment is production-ready

## Common Beginner Mistakes

- trying to do too much immediately after first node startup
- forgetting which endpoint actually returned the successful response
- treating a low block number as failure
- assuming one successful RPC call means every later workflow is already safe

## Verification

You are aligned with this page if you can explain the workflow in one sentence:

"Start the local node, keep it running, send one validated RPC health check, and record the exact outcome."

## Expected Output

At the end of this page, you should have:

- one simple first-developer workflow you can repeat
- one concrete success record from your own machine
- a clearer boundary between first success and later development work
