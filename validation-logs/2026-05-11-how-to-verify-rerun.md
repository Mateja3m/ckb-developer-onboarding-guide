# Validation Log

## Metadata

- Date: 2026-05-11
- Tester: Milan Matejic
- Section being validated: `docs/how-to-verify.md`
- Source used: Current `How to Verify`, `Quick Start`, and `Branching Paths` guide flow
- Operating system: macOS, local zsh terminal

## Summary

This rerun validates the current beginner onboarding path:

- Path A: public RPC only
- Path B: local node and local RPC
- Path C: local indexer check

All tested steps returned the expected success signals.

---

## Command Executed

```bash
curl --version
```

## Observed Output

```text
curl 8.7.1 (x86_64-apple-darwin25.0) libcurl/8.7.1 (SecureTransport) LibreSSL/3.3.6 zlib/1.2.12 nghttp2/1.68.0
Release-Date: 2024-03-27
Protocols: dict file ftp ftps gopher gophers http https imap imaps ipfs ipns ldap ldaps mqtt pop3 pop3s rtsp smb smbs smtp smtps telnet tftp
Features: alt-svc AsynchDNS GSS-API HSTS HTTP2 HTTPS-proxy IPv6 Kerberos Largefile libz MultiSSL NTLM SPNEGO SSL threadsafe UnixSockets
```

## Failure Cases

- None

## Confusion Points

- None

## Notes

- Confirms `curl` is available for the low-cost public RPC path.

---

## Command Executed

```bash
curl --head https://google.com
```

## Observed Output

```text
HTTP/2 301
location: https://www.google.com/
content-type: text/html; charset=UTF-8
content-security-policy-report-only: object-src 'none';base-uri 'self';script-src 'nonce-lUGIMOEG2XKeafqQGrmwCw' 'strict-dynamic' 'report-sample' 'unsafe-eval' 'unsafe-inline' https: http:;report-uri https://csp.withgoogle.com/csp/gws/other-hp
date: Mon, 11 May 2026 07:02:44 GMT
expires: Wed, 10 Jun 2026 07:02:44 GMT
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

- A beginner may not know that `HTTP/2 301` is still a successful HTTPS reachability signal.

## Notes

- Confirms terminal HTTPS access works.

---

## Command Executed

```bash
echo '{
    "id": 2,
    "jsonrpc": "2.0",
    "method": "get_tip_block_number",
    "params": []
}' \
| tr -d '\n' \
| curl -H 'content-type: application/json' -d @- \
https://testnet.ckb.dev/rpc
```

## Observed Output

```text
{"jsonrpc":"2.0","result":"0x1413e1b","id":2}
```

## Failure Cases

- None

## Confusion Points

- The exact `result` block number can change between runs.

## Notes

- Confirms Path A public RPC returns valid JSON-RPC output.

---

## Command Executed

```bash
node --version
```

## Observed Output

```text
v20.19.4
```

## Failure Cases

- None

## Confusion Points

- None

## Notes

- Confirms Node.js is available for the local node path.

---

## Command Executed

```bash
npm --version
```

## Observed Output

```text
11.4.2
```

## Failure Cases

- None

## Confusion Points

- None

## Notes

- Confirms npm is available for the local node path.

---

## Command Executed

```bash
git --version
```

## Observed Output

```text
git version 2.50.1 (Apple Git-155)
```

## Failure Cases

- None

## Confusion Points

- None

## Notes

- Confirms Git is available in the local development environment.

---

## Command Executed

```bash
offckb --help
```

## Observed Output

```text
Usage: offckb [options] [command]

ckb development network for your first try

Options:
  -V, --version                                 output the version number
  -h, --help                                    display help for command

Commands:
  node [options] [CKB-Version]                  Use the CKB to start devnet
  create [options] [project-name]               Create a new CKB Smart Contract project in JavaScript.
  deploy [options]                              Deploy contracts to different networks, only supports devnet and testnet
  debug [options]                               Quickly debug transaction with tx-hash
  system-scripts [options]                      Print/Output system scripts of the CKB blockchain
  clean [options]                               Clean the devnet data, need to stop running the chain first
  accounts                                      Print account list info
  deposit [options] [toAddress] [amountInCKB]   Deposit CKB tokens to address, only devnet and testnet
  transfer [options] [toAddress] [amountInCKB]  Transfer CKB tokens to address, only devnet and testnet
  transfer-all [options] [toAddress]            Transfer All CKB tokens to address, only devnet and testnet
  balance [options] [toAddress]                 Check account balance, only devnet and testnet
  debugger                                      Port of the raw CKB Standalone Debugger
  config <action> [item] [value]                do a configuration action
  devnet                                        Devnet utility commands
  help [command]                                display help for command
```

## Failure Cases

- None

## Confusion Points

- The command list is long, but the beginner path only needs `node` for this validation.

## Notes

- Confirms OffCKB is installed and exposes the expected `node` command.

---

## Command Executed

```bash
offckb node
```

## Observed Output

```text
Launching CKB devnet Node...
CKB:
2026-05-11 07:05:15.056 +00:00 main WARN ckb_network::network  Customized supported protocols: [Ping, Discovery, Identify, Feeler, DisconnectMessage, Sync, Relay, Time, Alert, LightClient, Filter]

CKB devnet RPC Proxy server running on http://127.0.0.1:28114
```

## Failure Cases

- None

## Confusion Points

- A beginner may interpret the warning line as failure, but the startup signal appears after it.

## Notes

- Confirms the local devnet node started and reached the expected startup signal.

---

## Command Executed

```bash
echo '{"id":2,"jsonrpc":"2.0","method":"get_tip_block_number","params":[]}' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

## Observed Output

```text
{"jsonrpc":"2.0","result":"0x5adb","id":2}
```

## Failure Cases

- None

## Confusion Points

- The exact block number can change between runs.
- The trailing `%` shown by zsh after command output is not part of the JSON response.

## Notes

- Confirms Path B local RPC returns valid JSON-RPC output while `offckb node` is running.

---

## Command Executed

```bash
echo '{"id":2,"jsonrpc":"2.0","method":"get_indexer_tip"}' \
| curl -H 'content-type: application/json' -d @- \
http://localhost:8114
```

## Observed Output

```text
{"jsonrpc":"2.0","result":{"block_hash":"0x9a683bd05f2f206133ab0b354ef911b963bb55255c8baa301cdba023f87ad878","block_number":"0x5ac3"},"id":2}
```

## Failure Cases

- None

## Confusion Points

- The exact `block_hash` and `block_number` can change between runs.
- The trailing `%` shown by zsh after command output is not part of the JSON response.

## Notes

- Confirms Path C local indexer check returns a `result` object with `block_hash` and `block_number`.

## Final Result

PASS:

- Low-cost public RPC path passed.
- Local tool checks passed.
- `offckb --help` passed.
- Local devnet startup passed.
- Local RPC check passed.
- Local indexer check passed.
