# Beginner Failure Detection Checklist

## What To Observe During Onboarding

- Long pauses before a command is run
- Re-reading the same line multiple times
- Switching between multiple tabs to infer missing context
- Asking what a dependency is before starting
- Asking whether a command is safe to run
- Uncertainty about the current directory
- Uncertainty about whether a process is still running
- Uncertainty about whether a result is correct
- Copying a command but editing it without confidence
- Stopping after a warning even when the step may still be recoverable

## Common Signs Of Confusion

- "Am I supposed to already have this installed?"
- "Which terminal or folder should I use?"
- "Did this succeed or fail?"
- "What am I looking at?"
- "Is this for testnet or mainnet?"
- "Do I need to run this locally?"
- "Why is nothing happening?"
- "Which part of this output matters?"
- "What should I do next?"
- "Is this an error or just a warning?"

## Typical Failure Patterns

- Missing dependency that was never stated explicitly
- Tool installed, but not available in the current shell
- Wrong directory or wrong file path
- Permission problem that looks like a tool failure
- Network problem that looks like a configuration issue
- Version mismatch that produces vague errors
- Process starts but gives no clear success signal
- Output is technically correct but hard for a beginner to interpret
- One successful step incorrectly suggests the entire setup is complete
- The tester reaches a failure and has no obvious next action

## What To Record When These Happen

- The exact moment confusion started
- The exact message or output shown on screen
- The assumption the tester made
- What the tester tried next without guidance
- What instruction would have prevented the problem
