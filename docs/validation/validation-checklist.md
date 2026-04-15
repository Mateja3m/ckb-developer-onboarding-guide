# Validation Checklist

## Local Environment Readiness

- Confirm the tester can open a terminal without help.
- Confirm the tester knows which directory they are working in.
- Confirm Node.js is installed and returns a version.
- Confirm npm is installed and returns a version.
- Confirm Git is installed and returns a version.
- Confirm `curl` is installed and returns version information.
- Confirm basic HTTPS connectivity works from the terminal.
- Record any version mismatch, missing tool, or shell/path issue.
- Record whether the tester had to search elsewhere before completing this step.

## Initial CKB Node Setup Attempt

- Record the exact source used for the node setup attempt.
- Record the exact command or commands used from that source.
- Record whether the tester understood what the command was supposed to do before running it.
- Record whether any prerequisite was assumed but not stated clearly.
- Record whether installation, startup, or verification failed.
- Record whether the tester could tell if the node was running successfully.
- Record whether logs, status messages, or errors were understandable to a beginner.
- Record whether the tester knew what to do after the first failure.

## Basic RPC Interaction Attempt

- Record the exact source used for the RPC attempt.
- Record the exact request command or request payload used.
- Record whether the tester understood what endpoint they were using.
- Record whether the tester understood whether the request depended on local setup or a public service.
- Record whether the response was returned, empty, malformed, or erroring.
- Record whether the tester could tell if the failure came from networking, configuration, or the request itself.
- Record whether the expected success condition was obvious.
- Record whether the tester could explain what the response meant in simple terms.
