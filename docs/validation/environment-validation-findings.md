# Environment Validation Findings

## Goal

Summarize the first real validation pass for local environment readiness and capture what should influence later onboarding documentation.

## Findings

- On April 14, 2026, the local shell environment was confirmed to be the repository root at `$HOME/Desktop/personal/Projects/ckb-developer-onboarding-guide`.
- The active shell was confirmed as `/bin/zsh`.
- The machine was identified as macOS on `arm64`.
- Core local tooling was available and responding:
  - Node.js `v20.19.4`
  - npm `11.4.2`
  - Git `2.50.1`
  - `curl` `8.7.1`
- The basic HTTPS connectivity check failed with:
  - `curl: (6) Could not resolve host: example.com`
- A rerun on April 19, 2026 showed the same HTTPS connectivity failure:
  - `curl: (6) Could not resolve host: example.com`
- On April 20, 2026, a rerun against a real HTTPS target succeeded:
  - `curl --head https://google.com`
  - `HTTP/2 301`

## Interpretation

- Local developer tooling appears ready for onboarding.
- Basic HTTPS connectivity is available in this environment when tested against a reachable real HTTPS target.
- The repeated `example.com` failure should not be treated as proof that all network-dependent onboarding is blocked.
- DNS resolution and target selection should still be called out explicitly in the final environment validation flow.

## Documentation Implications

- The environment setup guide should keep a dedicated network validation step before any download or RPC-related work.
- The guide should use a real HTTPS target that has been validated locally rather than a sample domain that produced misleading failure signals in this environment.
- The guide should explicitly mention that `curl: (6) Could not resolve host` is a likely DNS or network-resolution problem, not necessarily a CKB-specific issue.
- The validation materials should distinguish between "target-specific failure" and "general HTTPS connectivity failure."

## Suggested Future Troubleshooting Entry

- Symptom: `curl: (6) Could not resolve host`
- Likely categories: DNS issue, VPN/proxy issue, firewall restriction, temporary connectivity issue
- Placement later: environment setup troubleshooting or common errors section
