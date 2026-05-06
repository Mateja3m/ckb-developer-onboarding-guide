# 03. CKB Overview

## Goal

Understand the basic CKB concepts that matter before choosing between a local node, a public RPC endpoint, or later tooling.

## Requirements

Before using this page, complete:

- [00. Overview](00-overview.md)
- [01. Prerequisites](01-prerequisites.md)
- [02. Environment Setup](02-environment-setup.md)

This page is where the guide moves from generic onboarding foundations into CKB-specific onboarding context.

## What CKB Is

CKB stands for Common Knowledge Base.

In practical onboarding terms, CKB is the blockchain layer a developer interacts with when reading chain data, checking network state, or sending JSON-RPC requests to a node.

For this guide, the important point is simple:

- CKB is the system you are trying to talk to
- the node and RPC layers are how you talk to it during early setup

## What Nervos Is

Nervos is the broader ecosystem around CKB.

In this repository, you do not need a deep ecosystem map before you start. What matters first is that CKB-specific tooling, node setup, and RPC usage sit within the Nervos ecosystem.

## What Role A CKB Node Plays

A CKB node is the software process that participates in the network and exposes data or actions through an interface.

For a beginner, the node usually matters for four reasons:

- it runs the local chain process when you are doing local development
- it stores or serves the chain state your tools query
- it exposes RPC methods that scripts, wallets, or test commands can call
- it gives you a concrete success signal when local setup is working

## What RPC Is

RPC stands for Remote Procedure Call.

In practice, RPC is the request-and-response interface your tools use to ask a node for information or to submit actions. In this guide, RPC matters because it gives you a simple way to test whether your local or remote CKB access is actually working.

## Why Developers May Need A Local Node Or RPC Endpoint

You do not always need the same setup for every task.

Use a local node when:

- you need a controlled local development environment
- you want to reproduce onboarding steps without depending on a shared service
- you need a beginner-safe place to test whether node startup and RPC behavior make sense together

Use a public or shared RPC endpoint when:

- you only need to read chain data for a simple experiment
- a tutorial or tool explicitly supports that remote endpoint
- you are not yet validating local node management

The guide treats these as different onboarding choices, not as interchangeable defaults.

## What This Guide Covers

At this stage, the guide covers:

- the CKB-specific concepts a beginner needs before deeper setup
- how to think about local node setup versus RPC-only access
- a first validated local node and RPC path already recorded in this repository
- the role of indexer, workflow, troubleshooting, and support material in the broader onboarding path

## What This Guide Does Not Cover Yet

This guide does not yet provide complete instructions for:

- advanced node operations
- production deployment
- contract development workflows
- a fully validated public RPC provider comparison
- every exact indexer installation or hosted provider command a beginner might choose later

Where the repository does not already contain validated evidence for an exact command or path, the later documents use `TODO: verify against official CKB documentation before finalizing.`

## How To Use The Next Pages

Continue in this order:

1. [04. CKB Node Setup](04-ckb-node-setup.md) if you want the local-node path.
2. [05. RPC Basics](05-rpc-setup.md) to understand the first RPC checks and what success means.
3. [06. Indexer Setup](06-indexer-setup.md) to understand when an indexer belongs in the onboarding flow.
4. [07. Configuration Setup](07-configuration-setup.md) to understand the minimal configuration details already validated in this repository.
5. [08. First Developer Workflow](08-first-developer-workflow.md) to see the smallest repeatable happy path through the current guide.

## Verification

You are ready to continue if you can explain:

- what CKB is at a beginner level
- what a node does in the onboarding flow
- what RPC is used for
- why a local node is useful in some cases but not required in every case
- which parts of the broader CKB workflow this repository still does not document yet

## Expected Output

After reading this page, you should know:

- what system you are trying to access
- what role the node and RPC layers play in that access
- why the next setup choices are practical, not just theoretical
- where the current CKB-specific onboarding boundary stops

## Common Issues

### Treating CKB, Nervos, Node, And RPC As The Same Thing

They are related, but they are not identical. CKB is the blockchain layer, Nervos is the broader ecosystem, a node is the running software process, and RPC is the interface used to communicate with that process.

### Assuming A Local Node Is Always Required

Some learning steps only need RPC access. The local-node path is useful because it gives beginners a controlled environment, not because every CKB task requires local infrastructure immediately.

### Expecting This Page To Replace Official Technical References

This page is an onboarding explanation layer. Official documentation remains the source of truth for exact product, network, and command details that are not already validated in this repository.
