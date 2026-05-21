# Validation Log

## Metadata

- Date: 2026-04-20
- Tester: Milan Matejic
- Section being validated: Environment connectivity target and config-surface behavior
- Source used: Milestone 1 follow-up validation commands
- Operating system: macOS (shell prompt indicates local macOS workstation)

## Command Executed

```bash
curl --head https://google.com
```

## Observed Output

```text
HTTP/2 301
location: https://www.google.com/
content-type: text/html; charset=UTF-8
content-security-policy-report-only: object-src 'none';base-uri 'self';script-src 'nonce-6wMmZdV6xZkF6ivFgNqYNw' 'strict-dynamic' 'report-sample' 'unsafe-eval' 'unsafe-inline' https: http:;report-uri https://csp.withgoogle.com/csp/gws/other-hp
date: Mon, 20 Apr 2026 06:38:47 GMT
expires: Wed, 20 May 2026 06:38:47 GMT
cache-control: public, max-age=2592000
server: gws
content-length: 220
x-xss-protection: 0
x-frame-options: SAMEORIGIN
alt-svc: h3=":443"; ma=2592000,h3-29=":443"; ma=2592000
```

## Failure Cases

- None

## Confusion Points

- A beginner may not know whether an HTTP redirect still counts as a successful connectivity check.

## Possible Root Cause (Optional)

- N/A

## Notes

- Confirms the terminal can reach a normal HTTPS site and receive headers.
- Supports replacing the earlier placeholder-domain connectivity check with a real validated target.

---

## Command Executed

```bash
find "$HOME/Library/Application Support/offckb-nodejs" -type f -name ckb 2>/dev/null | sort
```

## Observed Output

```text
$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/ckb
```

## Failure Cases

- None

## Confusion Points

- A beginner may not know whether this path is machine-specific or globally standard.

## Possible Root Cause (Optional)

- N/A

## Notes

- Confirms the installed binary path can be discovered locally instead of assumed from memory.

---

## Command Executed

```bash
"$(find "$HOME/Library/Application Support/offckb-nodejs" -type f -name ckb 2>/dev/null | head -n 1)" --version
```

## Observed Output

```text
ckb 0.205.0 (b75a785 2026-03-17)
```

## Failure Cases

- None

## Confusion Points

- A beginner may not know whether this version must match every other environment exactly.

## Possible Root Cause (Optional)

- N/A

## Notes

- Confirms the discovered binary is executable and reports a real version string.

---

## Command Executed

```bash
find "$HOME/Library/Application Support/offckb-nodejs" -maxdepth 5 -mindepth 1 | sort
```

## Observed Output

```text
$HOME/Library/Application Support/offckb-nodejs/bins
$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0
$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/CHANGELOG.md
$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/COPYING
$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/README.md
$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/ckb
$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/ckb-cli
$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/docs
$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/docs/ci-workflow.md
$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/docs/ckb_async_block_sync.mermaid
$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/docs/ckb_sync.mermaid
$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/docs/configure.md
$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/docs/dev-miner.md
$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/docs/hashes.toml
$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/docs/integrity-check.md
$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/docs/platform-support.md
$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/docs/quick-start.md
$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/docs/rpc.md
$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/init
$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/init/README.md
$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/init/linux-systemd
$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/init/linux-systemd/README.md
$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/init/linux-systemd/ckb-miner.service
$HOME/Library/Application Support/offckb-nodejs/bins/0.205.0/init/linux-systemd/ckb.service
```

## Failure Cases

- None

## Confusion Points

- A beginner may not know which of these files matter for Milestone 1 versus later deep-dive setup.

## Possible Root Cause (Optional)

- N/A

## Notes

- Confirms the local OffCKB footprint includes the installed CKB binaries and bundled documentation files.

---

## Command Executed

```bash
offckb devnet config
```

## Observed Output

```text
Devnet config path does not exist: $HOME/Library/Application Support/offckb-nodejs/devnet
Tip: run `offckb node` once to initialize devnet config files first.
```

## Failure Cases

- The config editor did not open because the expected devnet config path did not exist.

## Confusion Points

- A beginner may expect the config editor to open immediately because `offckb devnet --help` advertises the command.

## Possible Root Cause (Optional)

- Devnet config files had not been initialized at the expected path.

## Notes

- This is valuable Milestone 1 behavior to document because it explains why a valid-looking config command may still fail before initialization.

---

## Command Executed

```bash
curl http://localhost:8114
```

## Observed Output

```text
Used HTTP Method is not allowed. POST or OPTIONS is required%
```

## Failure Cases

- Plain `curl` without a JSON-RPC POST payload does not count as a valid RPC verification method.

## Confusion Points

- A beginner may mistake this for a broken local endpoint.

## Possible Root Cause (Optional)

- HTTP method mismatch

## Notes

- Re-confirms the wrong-method behavior on `localhost:8114`.

---

## Command Executed

```bash
curl http://127.0.0.1:28114
```

## Observed Output

```text
Used HTTP Method is not allowed. POST or OPTIONS is required%
```

## Failure Cases

- Plain `curl` without a JSON-RPC POST payload does not count as a valid RPC verification method.

## Confusion Points

- A beginner may assume the startup-reported proxy endpoint should behave differently when opened directly.

## Possible Root Cause (Optional)

- HTTP method mismatch

## Notes

- Confirms the same wrong-method message appears on the startup-reported endpoint as well.

---

## Command Executed

```bash
offckb clean
```

## Observed Output

```text
Chain data cleaned.
```

## Failure Cases

- None in the observed output

## Confusion Points

- The shared output does not state explicitly whether the node had already been stopped before cleanup.

## Possible Root Cause (Optional)

- N/A

## Notes

- Confirms cleanup still returns the same success message in this environment.
