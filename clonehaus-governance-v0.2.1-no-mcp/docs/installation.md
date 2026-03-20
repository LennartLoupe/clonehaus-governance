# Installing Clonehaus Governance Plugin

Clonehaus Governance adds upstream governance design to Claude Cowork so teams can define agent authority boundaries before deployment. It is built for teams using AI agents in legal, sales, finance, HR, and other regulated or high-accountability workflows.

## Prerequisites

- Claude Cowork with plugin support on a paid plan
- Claude CLI installed and signed in for command-line installation methods
- Internet access to GitHub for Methods 1 and 2
- `git` installed for Method 2
- Permission to install plugins in your Cowork workspace

## Installation Methods

### Method 1: Install from GitHub (Recommended)

Use this if you want the fastest install path and you are comfortable installing directly from the public repository.

```bash
claude plugin add https://github.com/LennartLoupe/clonehaus-governance
```

Expected result:

- Cowork downloads the plugin manifest and command files
- The plugin appears in your installed plugin list as `clonehaus-governance`
- Installation usually completes in under 1 minute

If the command succeeds, move to [Verify Installation](#verify-installation).

### Method 2: Local Clone and Install

Use this if you want to inspect the source first, make local changes, or install from a local checkout.

```bash
git clone https://github.com/LennartLoupe/clonehaus-governance.git
cd clonehaus-governance
claude plugin install .
```

When to use this method:

- You want to review the plugin before installing it
- You plan to customize commands or templates locally
- Your team prefers installing from a checked-out repository instead of GitHub directly

Expected result:

- Cowork installs the plugin from the current directory
- Local command and template files become available to the plugin
- Installation usually completes in 1-2 minutes

### Method 3: Download and Upload

Use this if you prefer installing through the Cowork UI instead of the CLI.

Steps:

1. Download the packaged `.plugin` file from your release source or internal distribution.
2. Open Claude Cowork.
3. Go to the plugin management screen.
4. Choose the option to upload or import a plugin file.
5. Select the downloaded `.plugin` file.
6. Confirm the install when Cowork shows the plugin details.

Notes:

- If a packaged `.plugin` file is not available yet, use Method 1 or Method 2.
- This method is useful for teams distributing approved plugin packages internally.

## Verify Installation

Run:

```bash
claude plugin list | grep clonehaus
```

Expected output:

```text
clonehaus-governance
```

Then verify the commands are available in Cowork:

```text
/clonehaus:create-charter
/clonehaus:export-context --framework=langchain
/clonehaus:check-compliance
/clonehaus:ratify
```

A simple functional check:

1. Open Cowork.
2. Run `/clonehaus:create-charter`.
3. Confirm the guided 6-step flow appears.

## Troubleshooting

### `claude: command not found`

The Claude CLI is not installed or is not on your shell path.

What to do:

- Install the Claude CLI
- Restart your terminal
- Run `which claude` to confirm it is available

### Plugin install fails from GitHub

This is usually a network, authentication, or repository access issue.

What to do:

- Confirm you can open the GitHub repository in a browser
- Make sure Claude CLI is signed in
- Retry the command
- If needed, fall back to Method 2

### Plugin installs but commands do not appear

This usually means the plugin did not load correctly in Cowork yet.

What to do:

- Run `claude plugin list` and confirm `clonehaus-governance` is installed
- Restart Cowork
- Remove and reinstall the plugin
- Make sure your Cowork workspace supports plugins

### Local install fails with `git` or path errors

What to do:

- Confirm `git` is installed
- Make sure you are inside the cloned `clonehaus-governance` directory before running `claude plugin install .`
- Check that the repository contains `.claude-plugin/plugin.json`

### Upload install fails

What to do:

- Confirm the file is a valid plugin package
- Re-download the package in case it was corrupted
- Try Method 1 or Method 2 if upload support is unavailable in your Cowork build

## Next Steps

After installation, the fastest way to get value from the plugin is:

1. Run `/clonehaus:create-charter`
2. Define authority boundaries across decision, data, communication, system, and escalation
3. Export governance code with `/clonehaus:export-context --framework=<framework>`
4. Run `/clonehaus:check-compliance` to review EU AI Act coverage
5. Use `/clonehaus:ratify` when you are ready to create the accountability record

Recommended first workflow:

```text
/clonehaus:create-charter
/clonehaus:export-context --framework=langchain
```

If you want a concrete walkthrough after install, start with the legal example in [legal_agent_example.md](/Users/lennartzanders/dev_clean/clonehaus-governance/examples/legal_agent_example.md).
