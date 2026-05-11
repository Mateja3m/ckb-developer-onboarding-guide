# Overview

## Goal

Use the shortest path first, then branch only when you need more local control.

## Reading Order

1. [Quick Start](../quick-start.md)
2. [Branching Paths](../branching-paths.md)
3. [Troubleshooting Matrix](../troubleshooting-matrix.md)
4. [FAQ](../faq.md)
5. [How to Verify](../how-to-verify.md)

## First Success

First success means one valid CKB JSON-RPC response.

PASS:

- the documented command runs
- the endpoint returns `"jsonrpc":"2.0"`
- the response includes `"result"`
- you record the command, endpoint, and output

FAIL:

- tool missing: use [Troubleshooting Matrix](../troubleshooting-matrix.md)
- endpoint unreachable: use [Troubleshooting Matrix](../troubleshooting-matrix.md)
- unclear response: use [FAQ](../faq.md)

## What To Skip At First

Do not start with long concept pages, old reports, or validation logs.
Use them only when the main path links to them.
