# Test Command Pack

This file contains commands you can run during validation and send back with their outputs.

It intentionally avoids inventing CKB-specific commands.

## 1. Prepare A Folder For Validation Logs

Run:

```bash
mkdir -p validation-logs
```

## 2. Capture Local Environment Readiness

Run these commands one by one and paste the outputs back to me:

```bash
pwd
```

```bash
echo "$SHELL"
```

```bash
uname -a
```

```bash
node --version
```

```bash
npm --version
```

```bash
git --version
```

```bash
curl --version
```

```bash
curl --head https://example.com
```

## 3. Save A Blank Validation Log You Can Reuse

Run:

```bash
cat > validation-logs/validation-log-template.md <<'EOF'
# Validation Log

## Metadata

- Date:
- Tester:
- Section being validated:
- Source used:
- Operating system:

## Command Executed

```bash
<paste the exact command you ran>
```

## Observed Output

```text
<paste the full output or the most relevant part>
```

## Failure Cases

- 

## Confusion Points

- 

## Possible Root Cause (Optional)

- 

## Notes

- 
EOF
```

## 4. Capture A Real CKB Test Without Rewriting The Command

When you test a node setup or RPC step from an official source, do not paraphrase the command.

Instead:

1. Copy the exact command from the official source you are testing.
2. Run it manually.
3. Paste both the exact command and the full output into a new log based on `validation-logs/validation-log-template.md`.

If you want a very small copy-paste capture format, use this:

```md
## Command Executed
```bash
<paste exact official command here>
```

## Observed Output
```text
<paste exact output here>
```

## Failure Cases
- 

## Confusion Points
- 

## Possible Root Cause (Optional)
- 

## Notes
- 
```

## 5. What To Send Back To Me

Send me:

- the exact command you ran
- the observed output
- whether it succeeded or failed
- what felt unclear or confusing

With that, I can turn your real test evidence into validated documentation notes without inventing behavior.
