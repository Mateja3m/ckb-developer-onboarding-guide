# 13. Common Misconceptions

## Goal

Call out the beginner assumptions that most often create confusion during the early CKB onboarding flow.

## 1. "If The Page Opens In A Browser, The RPC Check Worked"

Why this happens:

- beginners often treat an HTTP endpoint like a normal web page

Why it is misleading:

- the RPC check in this repository depends on a JSON-RPC POST request, not a browser-style GET request

Correct mental model:

- a browser visit is not the same thing as a valid RPC health check

## 2. "A Low Block Number Means The Setup Failed"

Why this happens:

- the beginner focuses on the numeric result instead of the response structure

Why it is misleading:

- the repository validation already showed that a valid JSON-RPC response can return different low or higher tip heights depending on timing and local chain state

Correct mental model:

- the first success signal is a valid JSON-RPC request-and-response cycle

## 3. "If One Step Worked, Everything Must Be Ready"

Why this happens:

- early success feels larger than it really is

Why it is misleading:

- one successful RPC request does not prove indexer setup, workflow readiness, deployment readiness, or production readiness

Correct mental model:

- each layer of the onboarding flow proves only a limited next step

## 4. "Public RPC And Local Node Setup Are The Same Kind Of Success"

Why this happens:

- both can return data, so they look interchangeable at first

Why it is misleading:

- a public endpoint can prove you reached a remote service
- a local node flow proves you can start and understand your own environment

Correct mental model:

- similar request formats do not mean identical onboarding value

## 5. "Any Warning-Looking Output Means Hard Failure"

Why this happens:

- beginners naturally focus on the scariest line in the terminal

Why it is misleading:

- the repository validation already recorded warning-like startup output before successful node startup

Correct mental model:

- read the full startup pattern before deciding whether the process actually failed

## 6. "The First Missing-Binary Message Means `offckb node` Is Broken"

Why this happens:

- the first-run output looks more serious than the later recovered state

Why it is misleading:

- on the validation machine, the first run recovered by downloading the required binary and then continued successfully

Correct mental model:

- first-run setup noise and final failure are not automatically the same thing

## 7. "Every Local Port Mentioned By The Tools Means The Same Service"

Why this happens:

- local addresses look similar and are easy to merge mentally

Why it is misleading:

- the repository already observed successful local behavior on more than one endpoint, and that relationship is easy to misunderstand

Correct mental model:

- record which endpoint actually worked instead of assuming every port is interchangeable

## 8. "If A Tool Suggests A Fix, It Must Be Safe To Apply Immediately"

Why this happens:

- beginners want the fastest possible recovery path

Why it is misleading:

- unverified fixes can turn one clear failure into multiple overlapping failures

Correct mental model:

- prefer one deliberate, evidence-based change at a time

## Expected Output

At the end of this page, you should be less likely to:

- misread the first signal you see
- overgeneralize from one success
- confuse neighboring layers such as node, RPC, and indexer
- apply speculative fixes too quickly
