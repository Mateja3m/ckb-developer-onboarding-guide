# CKB Developer Onboarding Guide

Lightweight, documentation-first onboarding for developers who want a clear path into the Nervos CKB ecosystem.

## Goal

Provide a proof-of-concept for a validated, beginner-first CKB onboarding path.

This project is not focused on rewriting official documentation. Its purpose is to reduce onboarding friction by turning fragmented setup information into a more reliable execution path.

This repository contains the completed Milestone 1 onboarding foundation:

- repository structure
- project overview
- prerequisites guide
- environment setup guide
- initial quick-start structure
- CKB node setup foundation
- RPC setup foundation
- minimal configuration guidance

This repository now also contains the completed Milestone 2 documentation layer:

- CKB-specific overview and mental model guidance
- practical node, RPC, and indexer onboarding guidance
- first workflow, troubleshooting, and remediation guidance
- AI-assisted debugging and misconception guidance for early onboarding

Some exact commands and provider-specific details still remain marked with TODO notes where they have not yet been validated locally.

## Requirements

The current repository scope is intentionally limited to:

- providing a beginner-first onboarding path through local environment setup and first successful CKB interaction
- documenting the core Milestone 1 and Milestone 2 onboarding concepts and workflows
- preserving clear validation boundaries where exact commands or provider details are not yet confirmed locally

This repository still does not yet document:

- advanced contract development workflows
- production deployment guidance
- fully validated hosted provider comparisons for every later-stage service
- deeper production operations beyond beginner onboarding

This repository is being written as a validation-first guide.

- Commands are included only when they are standard and low risk.
- CKB-specific commands, outputs, and configuration details are included only where they have already been validated in this repository.
- Any step that still requires confirmation is marked with a TODO note.
- Official documentation remains the source of truth for commands and technical references.
- This repository focuses on execution flow, validation points, and early failure handling.

## Steps

1. Start with the documents in this order.

   - [Overview](docs/00-overview.md)
   - [Prerequisites](docs/01-prerequisites.md)
   - [Environment Setup](docs/02-environment-setup.md)
   - [CKB Overview](docs/03-quick-start.md)
   - [CKB Node Setup](docs/04-ckb-node-setup.md)
   - [RPC Basics](docs/05-rpc-setup.md)
   - [Indexer Setup](docs/06-indexer-setup.md)
   - [Configuration Setup](docs/07-configuration-setup.md)
   - [First Developer Workflow](docs/08-first-developer-workflow.md)
   - [Common Errors And Remediation](docs/09-common-errors-and-remediation.md)
   - [Troubleshooting Matrix](docs/10-troubleshooting-matrix.md)
   - [AI-Assisted Debugging](docs/11-ai-assisted-debugging.md)
   - [CKB Mental Model](docs/12-ckb-mental-model.md)
   - [Common Misconceptions](docs/13-common-misconceptions.md)

2. Continue through the completed Milestone 1 and Milestone 2 onboarding path after environment readiness is confirmed.

   The guide now continues from the Milestone 1 foundation through the full Milestone 2 CKB-specific documentation layer, including indexer context, first workflow guidance, troubleshooting, AI-assisted debugging, and conceptual support material.

3. Follow the repository structure when reviewing or extending the guide.

   ```text
   .
   ├── README.md
   └── docs
       ├── 00-overview.md
       ├── 01-prerequisites.md
       ├── 02-environment-setup.md
       ├── 03-quick-start.md
       ├── 04-ckb-node-setup.md
       ├── 05-rpc-setup.md
       ├── 06-indexer-setup.md
       ├── 07-configuration-setup.md
       ├── 08-first-developer-workflow.md
       ├── 09-common-errors-and-remediation.md
       ├── 10-troubleshooting-matrix.md
       ├── 11-ai-assisted-debugging.md
       ├── 12-ckb-mental-model.md
       └── 13-common-misconceptions.md
   ```

4. Use the documentation map to understand the current scope.

   - [00 Overview](docs/00-overview.md): what this guide is, who it is for, and how to read it
   - [01 Prerequisites](docs/01-prerequisites.md): what you need before touching CKB-specific setup
   - [02 Environment Setup](docs/02-environment-setup.md): how to prepare a clean local workspace
   - [03 CKB Overview](docs/03-quick-start.md): beginner-friendly introduction to CKB, Nervos, nodes, and RPC
   - [04 CKB Node Setup](docs/04-ckb-node-setup.md): practical local-node decision guide and validated local startup path
   - [05 RPC Basics](docs/05-rpc-setup.md): first RPC health-check concepts and response interpretation
   - [06 Indexer Setup](docs/06-indexer-setup.md): where the indexer fits and how to think about local versus hosted choices
   - [07 Configuration Setup](docs/07-configuration-setup.md): minimal validated configuration awareness for Milestone 1
   - [08 First Developer Workflow](docs/08-first-developer-workflow.md): smallest repeatable happy path from setup into confirmed chain interaction
   - [09 Common Errors and Remediation](docs/09-common-errors-and-remediation.md): beginner-facing failures with likely causes and next actions
   - [10 Troubleshooting Matrix](docs/10-troubleshooting-matrix.md): fast symptom-to-check-to-action lookup
   - [11 AI-Assisted Debugging](docs/11-ai-assisted-debugging.md): safe, validation-first use of AI during onboarding
   - [12 CKB Mental Model](docs/12-ckb-mental-model.md): simple relationships between node, RPC, indexer, devnet, and onboarding steps
   - [13 Common Misconceptions](docs/13-common-misconceptions.md): common beginner assumptions that lead to confusion

## Verification

You are aligned with the current repository state if you understand that:

- this repository is a proof-of-concept for validated onboarding
- official docs provide the reference layer, while this project focuses on execution and reliability
- Milestone 1 is complete as the documentation foundation
- Milestone 2 is complete as the CKB-specific onboarding documentation layer
- unresolved or untested details are marked with TODO notes
- this repository is for onboarding, not advanced CKB development

## Expected Output

After reading this file, you should know:

- what this repository currently includes
- what is intentionally out of scope for this phase
- why this project exists alongside official documentation
- which documents to read first
- how the full guide is planned to grow over time

## Common Issues

### Treating TODO Notes As Fully Validated Commands

Some sections now include practical guidance together with TODO notes for exact commands or provider-specific details that have not yet been validated locally. Do not treat those TODO-marked details as final commands.

### Expecting Advanced CKB Content Too Early

This repository is currently focused on onboarding foundations, not contract development, deployment, or advanced workflows.

### Treating This Repository As A Reference Manual

Official documentation already serves that role. This repository is intended to help beginners execute the onboarding path more reliably and understand what to do when early steps go wrong.

### Ignoring TODO Notes

If a step or recommendation is marked with a TODO note, it still needs confirmation before being treated as final documentation.
