# 00. Overview

## Goal

Understand what this onboarding guide covers, who it is for, and what "first success" means in the context of CKB onboarding.

## Requirements

Before using this guide, you should have:

- access to a computer with terminal access
- access to a web browser
- time to follow the documents in order instead of skipping directly to later setup steps

No prior CKB experience is assumed.

## Steps

1. Read the project scope before starting setup.

   This guide is focused on onboarding, environment preparation, and first interactions. It is not a contract development guide, and it is not intended to replace official CKB documentation.

2. Understand the definition of success.

   In this repository, a successful onboarding means a developer can make a valid RPC request and receive a correct response from the CKB network.

3. Follow the documents in sequence.

   Start with prerequisites, then environment setup, then the CKB overview, node, RPC, and configuration pages. Later sections that still say `TODO: VALIDATE` remain planned structure rather than finished onboarding guidance, and later-phase placeholders may include a target milestone inline.

4. Treat placeholders as planned structure, not finished instructions.

   Several files exist to show the intended shape of the complete guide. If a section says `TODO: VALIDATE`, it is not ready to be treated as final guidance. If a milestone is listed next to that marker, treat it as planned sequencing rather than completed scope.

5. Understand the role of this project.

   Official documentation provides commands, component references, and technical explanations. This project is a proof-of-concept for a validated onboarding layer that focuses on reducing setup friction, clarifying success signals, and capturing failure states early.

## Verification

You are ready to continue if you can answer these questions clearly:

- What is this guide trying to help you do?
- Why is this guide different from official reference documentation?
- What is included in scope for the onboarding flow?
- What is not included in this early documentation phase?
- What counts as a successful first outcome?

## Expected Output

After reading this page, you should understand that:

- this is a beginner-first onboarding repository
- this repository is designed as an execution-focused onboarding path, not just a reference
- Milestone 1 is complete as the documentation foundation
- Milestone 2 has started with the first CKB-specific overview, node setup, RPC basics, and local verification guidance
- later sections outside that scope still need validation before they become full instructions

## Common Issues

### Expecting a Complete Build Guide

This repository is not yet a full end-to-end development guide. It is currently a structured foundation for one.

### Skipping Ahead Too Early

Many onboarding issues happen when developers jump into node, RPC, or indexer setup before checking local prerequisites. Follow the documents in order.

### Assuming Commands Alone Solve Onboarding

The main problem is usually not the absence of commands. It is missing prerequisites, unclear dependencies, partial setup, silent misconfiguration, or uncertainty about whether a step succeeded.

### Assuming "Accessible" Means "Validated"

A document may exist in the repository before it is fully complete. Use the validation notes and `TODO: VALIDATE` markers to tell the difference, and use any milestone note next to the marker as a scope signal.
