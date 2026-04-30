# 02. Environment Setup

## Goal

Prepare a clean local workspace so later CKB-specific setup can happen in an organized and repeatable way.

## Requirements

Before following this page, make sure you have completed [01. Prerequisites](01-prerequisites.md).

You should already have working access to:

- Node.js
- npm
- Git
- `curl`
- a terminal
- a web browser

This page does not install or configure a CKB node, RPC endpoint, or indexer.

## Steps

1. Create a dedicated working directory.

   Run:

   ```bash
   mkdir -p ~/ckb-test
   cd ~/ckb-test
   ```

   Using a dedicated folder makes it easier to keep downloads, notes, and example files in one place.

2. Confirm that you are in the expected directory.

   Run:

   ```bash
   pwd
   ```

   Make sure the terminal shows the path you expect to use for this onboarding work.

3. Create a place for notes and troubleshooting details.

   Run:

   ```bash
   mkdir -p notes
   touch notes/setup-log.md
   ```

   Use this file to record version numbers, errors, and anything unusual during setup. This becomes useful later when troubleshooting.

4. Confirm your basic developer tools still work inside the new directory.

   Run:

   ```bash
   node --version
   npm --version
   git --version
   curl --version
   ```

   This verifies that your tools are available in the shell session you will actually use for onboarding.

5. Verify that your machine can reach normal HTTPS resources.

   Run:

   ```bash
   curl --head https://google.com
   ```

   This is a simple connectivity check. Later onboarding steps may require downloading files or reaching public documentation.

   How to verify:

   - You receive HTTP response headers.
   - A redirect response such as `HTTP/2 301` still counts as proof that the terminal can reach a normal HTTPS site.

6. Stop here before moving into CKB-specific setup.

   At this point, your local environment should be organized and ready. Continue next with [03. CKB Overview](03-quick-start.md).

## Verification

You are ready to continue if:

- your dedicated working directory exists
- your `notes/setup-log.md` file exists
- your core tools still return version information
- your machine can make a basic HTTPS request

## Expected Output

At the end of this page, you should have:

- a clean local folder for onboarding work
- a simple notes file for tracking setup details
- confirmed access to the required developer tools
- confirmed general network access from the terminal

Exact command output will vary by operating system and installed tool versions.

## Common Issues

### Permission Errors When Creating Folders

Try creating the workspace somewhere inside your home directory, not in a restricted system location.

### HTTPS Request Fails

This can happen because of firewall rules, proxy settings, VPN configuration, temporary network issues, or a hostname-resolution problem with the exact target you tested.

### Skipping Local Organization

It can feel unnecessary to create a dedicated folder and notes file, but this small step reduces confusion later when more tools and configuration files are introduced.
