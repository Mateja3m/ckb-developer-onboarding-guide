# 12. CKB Mental Model

## Goal

Give beginners a small mental model for how the main parts of the CKB onboarding flow relate to each other.

## Why This Page Matters

Many onboarding problems come from mixing together concepts that belong to different layers.

This page is meant to reduce that confusion before deeper development work begins.

## The Simple Model

### CKB

CKB is the blockchain system you are trying to interact with.

For onboarding purposes, it is the system behind the data, responses, and local chain state you are testing.

### Nervos

Nervos is the broader ecosystem around CKB.

In this guide, that mainly matters because the tools, documentation, and workflows you touch are part of that broader ecosystem.

### Node

The node is the running software process that participates in the chain and exposes a way for tools to interact with it.

In early onboarding:

- the node is the thing you start
- the node is the thing that must keep running
- the node is the thing your first health-check requests depend on

### RPC

RPC is the request-and-response interface used to talk to the node.

In practical terms:

- the node is the running service
- RPC is how you ask it for information

### Indexer

The indexer is a convenience layer for searching or organizing chain data more efficiently.

In beginner terms:

- the node gives you direct blockchain access
- the indexer helps with broader read patterns and search

That is why the guide treats indexer setup as later than first node and RPC success.

### Devnet

Devnet is the local development-oriented environment used in this repository's validated onboarding flow.

It matters because:

- it gives beginners a controlled environment
- it reduces early dependency on shared infrastructure
- it makes repeated local onboarding tests easier to reason about

## How The Pieces Fit Together

The simplest onboarding chain looks like this:

1. prepare the local machine
2. start the node in the local devnet flow
3. send an RPC request
4. confirm a valid response
5. optionally add indexer-backed or broader application workflows later

If you skip the earlier steps mentally, later tools become much harder to understand.

## What This Mental Model Prevents

This page is especially meant to prevent these confusions:

- thinking the node and RPC are the same thing
- thinking an indexer replaces the node
- thinking a hosted service proves local setup is complete
- thinking one successful response means every later workflow is already validated

## What This Page Does Not Do

This page does not yet try to teach:

- deep chain architecture
- contract internals
- advanced storage mechanics
- production infrastructure design

It only gives the minimal mental map needed to make the onboarding flow easier to follow.

## Expected Output

At the end of this page, you should be able to explain:

- what system you are interacting with
- what part the node plays
- what RPC actually is
- why an indexer is useful later but not required for the first success path
