# Validation Log

## Metadata

- Date: 2026-04-20
- Tester: repository maintainer
- Section being validated: Dual-endpoint local RPC POST behavior after restart
- Source used: Milestone 1 restart and RPC verification commands
- Operating system: macOS (shell prompt indicates local macOS workstation)

## Command Executed

```bash
offckb node
```

## Observed Output

```text
Launching CKB devnet Node...
CKB:
2026-04-20 06:49:08.440 +00:00 main WARN ckb_network::network  Customized supported protocols: [Ping, Discovery, Identify, Feeler, DisconnectMessage, Sync, Relay, Time, Alert, LightClient, Filter]

CKB devnet RPC Proxy server running on http://127.0.0.1:28114
```

## Failure Cases

- None

## Confusion Points

- A beginner may still interpret the warning-style log as a startup failure.

## Possible Root Cause (Optional)

- N/A

## Notes

- Confirms the restart after cleanup still reached the expected startup signal.

---

## Command Executed

```bash
lsof -nP -iTCP:8114 -sTCP:LISTEN
```

## Observed Output

```text
COMMAND   PID         USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
ckb     89095 <local-user>   59u  IPv4 0xe663d3695adb0d88      0t0  TCP *:8114 (LISTEN)
```

## Failure Cases

- None

## Confusion Points

- A beginner may not know whether listening on `*:8114` means localhost-only access or a broader bind on the machine.

## Possible Root Cause (Optional)

- N/A

## Notes

- Confirms a `ckb` process was listening on port `8114` during the validation run.
- At this point in the validation sequence, the process-level relationship between the two ports was still incomplete.

---

## Command Executed

```bash
lsof -nP -iTCP:28114 -sTCP:LISTEN
```

## Observed Output

```text
COMMAND   PID         USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
node    97118 <local-user>   19u  IPv6 0xef0b3f518488268b      0t0  TCP *:28114 (LISTEN)
```

## Failure Cases

- None

## Confusion Points

- A beginner may not immediately realize that the process name `node` points to the OffCKB Node.js layer rather than the Rust `ckb` binary itself.

## Possible Root Cause (Optional)

- N/A

## Notes

- Confirms a `node` process was listening on port `28114` during the validation run.
- Combined with the earlier `lsof` result on `8114`, this strongly suggests that `28114` is a Node.js-exposed proxy layer while `8114` is the underlying `ckb` listener on the validation machine.

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
http://localhost:8114
```

## Observed Output

```text
{"jsonrpc":"2.0","result":"0x0","id":2}%
```

## Failure Cases

- None

## Confusion Points

- A beginner may still think the trailing `%` is part of the JSON response.

## Possible Root Cause (Optional)

- N/A

## Notes

- Confirms `localhost:8114` still accepts the JSON-RPC POST request after restart.

---

## Command Executed

```bash
echo '{
    "id": 1,
    "jsonrpc": "2.0",
    "method": "get_tip_block_number",
    "params": []
}' \
| tr -d '\n' \
| curl -i -H 'content-type: application/json' -d @- \
http://localhost:8114
```

## Observed Output

```text
HTTP/1.1 200 OK
content-type: application/json
vary: origin, access-control-request-method, access-control-request-headers
access-control-allow-origin: *
access-control-expose-headers: *
content-length: 40
date: Mon, 20 Apr 2026 06:54:08 GMT

{"jsonrpc":"2.0","result":"0x20","id":1}%
```

## Failure Cases

- None

## Confusion Points

- A beginner may not know whether the HTTP headers matter or whether only the JSON body matters.

## Possible Root Cause (Optional)

- N/A

## Notes

- Confirms `localhost:8114` returned `HTTP/1.1 200 OK` and a valid JSON-RPC body for the same method.

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
http://127.0.0.1:28114
```

## Observed Output

```text
{"jsonrpc":"2.0","result":"0xa","id":2}%
```

## Failure Cases

- None

## Confusion Points

- A beginner may expect the proxy endpoint to fail because earlier docs only used `localhost:8114`.
- A beginner may still think the trailing `%` is part of the JSON response.

## Possible Root Cause (Optional)

- N/A

## Notes

- Confirms the startup-reported endpoint `127.0.0.1:28114` also accepts the same JSON-RPC POST request in this environment.
- This reduces one Milestone 1 uncertainty, even though the full routing relationship between the two local endpoints is still not fully explained.

---

## Command Executed

```bash
echo '{
    "id": 1,
    "jsonrpc": "2.0",
    "method": "get_tip_block_number",
    "params": []
}' \
| tr -d '\n' \
| curl -i -H 'content-type: application/json' -d @- \
http://127.0.0.1:28114
```

## Observed Output

```text
HTTP/1.1 200 OK
content-type: application/json
vary: origin, access-control-request-method, access-control-request-headers
access-control-allow-origin: *
access-control-expose-headers: *
content-length: 40
connection: close
date: Mon, 20 Apr 2026 06:54:41 GMT

{"jsonrpc":"2.0","result":"0x27","id":1}%
```

## Failure Cases

- None

## Confusion Points

- A beginner may not know whether the slightly different headers, such as `connection: close`, are significant for onboarding.

## Possible Root Cause (Optional)

- N/A

## Notes

- Confirms `127.0.0.1:28114` also returned `HTTP/1.1 200 OK` and a valid JSON-RPC body for the same method.
