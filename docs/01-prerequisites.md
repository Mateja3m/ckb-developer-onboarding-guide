# 01. Prerequisites

## Goal

Confirm that you have the basic tools and local conditions needed before starting any CKB-specific setup.

## Requirements

For this phase of the guide, you should have access to:

- a terminal
- a web browser
- permission to install developer tools on your machine

The following tools should be available before moving forward:

- Node.js
- npm
- Git
- `curl`

## Steps

1. Confirm you can open a terminal.

   If you are new to development tooling, this is the application where you can type commands and see their output.

2. Confirm you can browse official documentation.

   Open a web browser and verify that normal HTTPS websites load correctly. Later sections of this guide will depend on official documentation and package downloads.

3. Check whether Node.js is installed.

   Run:

   ```bash
   node --version
   ```

   If the command is not found, install Node.js from the official source before continuing.

4. Check whether npm is installed.

   Run:

   ```bash
   npm --version
   ```

   If the command is not found, npm may not have been installed with Node.js, or your shell may not be picking it up correctly.

5. Check whether Git is installed.

   Run:

   ```bash
   git --version
   ```

   Git is useful for cloning repositories, tracking changes, and following open-source project workflows.

6. Check whether `curl` is installed.

   Run:

   ```bash
   curl --version
   ```

   `curl` is commonly used to test endpoints and download files from the terminal.

7. Write down anything that fails before moving on.

   If one of the commands above does not work, stop and fix it first. Do not continue into CKB-specific setup with missing local tooling.

## Verification

You are ready for the next document if:

- each command runs successfully
- each tool returns a version string
- you do not see `command not found` for any required tool

## Expected Output

At this stage, the expected result is simple:

- `node --version` returns a version string
- `npm --version` returns a version string
- `git --version` returns a version string
- `curl --version` returns version and build information

Exact version values may differ by machine. `TODO: VALIDATE` recommended version ranges for this project.

## Common Issues

### `command not found`

This usually means the tool is not installed or your shell cannot find it in your `PATH`.

### Tool Installed but Still Not Detected

If you installed a tool moments ago, close and reopen your terminal before testing again. Some systems do not refresh shell paths automatically.

### No Admin Permission to Install Tools

If you are using a work-managed machine, you may need approval from your administrator before you can install developer dependencies.
