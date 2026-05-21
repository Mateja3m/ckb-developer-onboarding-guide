# Validation Log

## Metadata

- Date: 2026-04-19
- Tester: Milan Matejic
- Section being validated: Local environment readiness re-check
- Source used: Milestone 1 manual verification pass
- Operating system: macOS (shell prompt indicates local macOS workstation)

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

- None reported

## Possible Root Cause (Optional)

- N/A

## Notes

- Confirms Node.js is still available in the current shell.

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

- None reported

## Possible Root Cause (Optional)

- N/A

## Notes

- Confirms npm is still available in the current shell.

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

- None reported

## Possible Root Cause (Optional)

- N/A

## Notes

- Confirms Git is still available in the current shell.

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

- A beginner may still not know which parts of the feature list matter.

## Possible Root Cause (Optional)

- N/A

## Notes

- Confirms `curl` is present and reports normal version/build information.

---

## Command Executed

```bash
curl --head https://example.com
```

## Observed Output

```text
curl: (6) Could not resolve host: example.com
```

## Failure Cases

- Command failed.
- HTTPS connectivity could not be validated because hostname resolution failed.

## Confusion Points

- A beginner may not know whether this is a `curl` issue, a DNS issue, or a broader network restriction.
- A beginner may not know whether it is safe to continue into network-dependent onboarding steps after this failure.

## Possible Root Cause (Optional)

- DNS resolution issue
- Network restriction
- VPN or proxy interference

## Notes

- Tool availability is confirmed in this rerun.
- This rerun matches the Week 1 failure pattern and suggests the hostname-resolution issue persisted on April 19, 2026.
