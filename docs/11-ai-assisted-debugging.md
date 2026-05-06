# 11. AI-Assisted Debugging

## Goal

Help beginners use AI tools safely and effectively during CKB onboarding without treating AI output as automatically correct or authoritative.

## Requirements

Before using this page, complete:

- [09. Common Errors And Remediation](09-common-errors-and-remediation.md)
- [10. Troubleshooting Matrix](10-troubleshooting-matrix.md)

This page is tool-agnostic by design.

## What AI Is Good At In This Workflow

AI can be helpful when you need to:

- summarize confusing terminal output
- separate likely causes into simpler categories
- compare what you expected to happen against what actually happened
- turn rough notes into a clearer troubleshooting record

## What AI Is Not Good At By Default

AI should not be treated as the source of truth for:

- unverified CKB commands
- unverified configuration edits
- network-specific operational details
- assumptions about your local machine that you did not actually confirm

## The Best Prompting Pattern

When asking for debugging help, provide:

- the exact command you ran
- the exact output you saw
- what you expected to happen
- which step of the onboarding flow you were in
- whether you are using a local node or a hosted service

The more exact your context is, the less likely the AI is to guess incorrectly.

## The Worst Prompting Pattern

Avoid asking:

- "It does not work, what should I do?"
- "Give me the right command" when you have not shown the command you ran
- "Fix this setup" without sharing the actual output

These patterns increase the chance that the AI invents missing details.

## Safe Use Rules

When using AI during onboarding:

- prefer exact copied commands and outputs over paraphrases
- ask the AI to explain uncertainty instead of hiding it
- verify CKB-specific commands against official documentation when this repository has not already validated them
- change one thing at a time instead of applying a long list of speculative fixes

## Good Questions To Ask

- "Can you classify this failure as tooling, network, node, endpoint, or request-format related?"
- "Can you explain which part of this output is the actual blocker?"
- "Can you compare this command output to the expected success pattern from the guide?"
- "Can you help me write down the exact failure clearly before I try a fix?"

## Questions To Treat Carefully

- "What is the exact command I should run next?"
- "Can I ignore this warning?"
- "Are these two endpoints interchangeable?"
- "Should I edit this config file?"

For these, the AI may still help reason through the problem, but the answer should be checked against validated repository evidence or official documentation.

## Verification Habit

After getting AI help, ask yourself:

- did the answer rely on the exact output I provided
- did it clearly separate fact from guesswork
- did it preserve the validation-first rule
- can I verify the next step before I run it

If the answer fails those checks, do not treat it as a final recommendation.

## Expected Output

At the end of this page, you should know how to use AI as:

- a clarity tool
- a triage tool
- a note-organization tool

But not as:

- an unquestioned source of exact CKB commands
- a replacement for official documentation
- a substitute for reading your own terminal output carefully
