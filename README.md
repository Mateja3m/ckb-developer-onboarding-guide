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

Milestone 2 work has started with initial CKB-specific setup, RPC basics, and local verification guidance.

Later sections that go beyond the currently validated scope are still intentionally scaffolded as placeholders so the guide can expand in a structured way without pretending unfinished sections are already validated.

## Requirements

The current repository scope is intentionally limited to:

- defining the documentation structure
- helping a beginner understand what the guide covers
- preparing a local development environment
- introducing the first CKB-specific onboarding layer for node setup, RPC basics, and local verification guidance

This repository still does not yet document:

- indexer setup details
- troubleshooting matrix content
- AI-assisted debugging workflows
- advanced workflow content beyond first successful local RPC interaction

This repository is being written as a validation-first guide.

- Commands are included only when they are standard and low risk.
- CKB-specific commands, outputs, and configuration details are included only where they have already been validated in this repository.
- Any step that still requires confirmation is marked with a TODO note, and later-phase placeholders now note their target milestone inline where known.
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
   - [Configuration Setup](docs/07-configuration-setup.md)

2. Continue into the Milestone 1 and early Milestone 2 setup path after environment readiness is confirmed.

   The guide now continues from the Milestone 1 foundation into the first Milestone 2 CKB-specific layer through overview, node setup, RPC basics, and minimal configuration guidance. The later placeholder files still show how the full guide will be organized, but they are not yet validated onboarding steps.

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
   - [06 Indexer Setup](docs/06-indexer-setup.md): placeholder
   - [07 Configuration Setup](docs/07-configuration-setup.md): minimal validated configuration awareness for Milestone 1
   - [08 First Developer Workflow](docs/08-first-developer-workflow.md): placeholder
   - [09 Common Errors and Remediation](docs/09-common-errors-and-remediation.md): placeholder
   - [10 Troubleshooting Matrix](docs/10-troubleshooting-matrix.md): placeholder
   - [11 AI-Assisted Debugging](docs/11-ai-assisted-debugging.md): placeholder
   - [12 CKB Mental Model](docs/12-ckb-mental-model.md): placeholder
   - [13 Common Misconceptions](docs/13-common-misconceptions.md): placeholder

## Verification

You are aligned with the current repository state if you understand that:

- this repository is a proof-of-concept for validated onboarding
- official docs provide the reference layer, while this project focuses on execution and reliability
- Milestone 1 is complete as the documentation foundation
- Milestone 2 has started with initial CKB-specific overview, node setup, RPC basics, and local verification guidance
- later files outside Milestone 1 remain placeholders by design
- unresolved or untested details are marked with TODO notes
- later placeholder sections note their intended milestone inline where the scope is already clear
- this repository is for onboarding, not advanced CKB development

## Expected Output

After reading this file, you should know:

- what this repository currently includes
- what is intentionally out of scope for this phase
- why this project exists alongside official documentation
- which documents to read first
- how the full guide is planned to grow over time

## Common Issues

### Treating Placeholder Files as Complete Guides

Most files in `docs/` exist to establish structure. Unless a section is fully drafted, do not assume it is ready for production use.

### Expecting Advanced CKB Content Too Early

This repository is currently focused on onboarding foundations, not contract development, deployment, or advanced workflows.

### Treating This Repository As A Reference Manual

Official documentation already serves that role. This repository is intended to help beginners execute the onboarding path more reliably and understand what to do when early steps go wrong.

### Ignoring TODO Notes

If a step or recommendation is marked with a TODO note, it still needs confirmation before being treated as final documentation. Where scope is already known, the marker may also note the intended milestone, such as `TODO: VALIDATE (Milestone 2)`.
