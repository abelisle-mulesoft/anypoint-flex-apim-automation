# Anypoint CLI Prerequisites – CLI Playbook

## Abstract

This playbook provides tested, practical command-line patterns for preparing a workstation or CI/CD runner to use the Anypoint Platform Command Line Interface (CLI). 

## Purpose

The purpose of this document is to complement MuleSoft’s official documentation, not to replace it. It consolidates prerequisite steps, validation checks, and common failure patterns to help ensure a consistent and reliable starting point for automating API management with the Anypoint CLI. 

## Scope and Assumptions

This playbook assumes that:

- You are installing Anypoint CLI 4.x.
- You are operating on macOS, Linux, or a compatible CI/CD runner.
- You have sufficient privileges to install Node.js, npm packages, and global CLI tools.
- Authentication strategy is addressed separately (for example, connected apps).

This playbook does **not** cover:
- Automation of the API management lifecycle.
- CI/CD pipeline design.
- Policy configuration or deployment workflows.

## How to Use This Playbook

Use this document as:

- A repeatable checklist for setting up new machines or build agents.
- A reference for troubleshooting installation issues.
- A baseline validation step before running automation scripts.

All commands have been tested and are safe to reuse once adapted to your environment.

## Required Tooling

The Anypoint CLI depends on the following tools:

| Tool | Purpose |
|----|--------|
| Node.js | Runtime required by the Anypoint CLI |
| npm | Package manager used to install the CLI |
| nvm (recommended) | Manage Node.js versions consistently |

## Verify or Install Node.js and npm

Using nvm is strongly recommended to ensure predictable Node.js versions across environments.

### Check Current Versions

```shell
node -v
npm -v
```

If Node.js is not installed or the version is outside the supported range, install or update it as shown below.

### Install or Update nvm

```shell
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
```

Load `nvm` without restarting the shell:

```shell
. "$HOME/.nvm/nvm.sh"
```

### Install the Latest Node.js LTS Version

> [!NOTE]
> While the [official documentation](https://docs.mulesoft.com/anypoint-cli/latest/install) specifies `Node.js` versions 18.0.0 to 20.0.0, all examples in this repository have been authored and successfully tested with `Node.js` 22.20.0 LTS and `npm` 11.6.2. This indicates that newer LTS versions of Node.js may also work in practice, even if they are not explicitly listed as supported.

Install the latest available LTS version of Node.js:

```shell
nvm install --lts
nvm use --lts
```

Verify the installation:

```shell
node -v
npm -v
```

### Upgrade npm (If Needed)

```shell
npm install -g npm@latest
```

### Fix Common npm Cache Permission Issue (macOS)

Older versions of npm may leave root-owned files in the cache directory.

```shell
sudo chown -R $(id -u):$(id -g) "$HOME/.npm"
```

## Install the Anypoint CLI

Install the Anypoint CLI core package globally:

```shell
npm install -g anypoint-cli-v4
```

Verify the installation:

```shell
anypoint-cli-v4 version
```

Successful output confirms the CLI is available on your PATH.

## Install Required CLI Plugins

By default, no plugins are installed with the Anypoint CLI core package. Install only the plugins required for API automation to follow the principle of least privilege.

### List Installed Plugins

```shell
anypoint-cli-v4 plugins
```

### Install Commonly Required Plugins

```shell
anypoint-cli-v4 plugins:install anypoint-cli-account-plugin
anypoint-cli-v4 plugins:install anypoint-cli-api-mgr-plugin
anypoint-cli-v4 plugins:install anypoint-cli-exchange-plugin
```

Re-run the plugin list command to confirm installation.

## Authentication Smoke Tests

Before running automation scripts, verify that authentication and context resolution work as expected.

### List Business Groups

```shell
anypoint-cli-v4 account:business-group:list \
  --client_id <client-id> \
  --client_secret <client-secret>
```

Expected result:
- A list of business groups with their IDs

### List Environments in a Business Group

```shell
anypoint-cli-v4 account:environment:list \
  --organization <organization-id> \
  --client_id <client-id> \
  --client_secret <client-secret>
```

Expected result:
- A list of environments and their IDs

## Common Failure Modes

| Symptom | Likely Cause |
|-------|-------------|
| `command not found` | CLI not installed or not on PATH |
| 401 / 403 errors | Invalid credentials or missing scopes |
| Empty results | Incorrect organization context |
| Plugin command missing | Required plugin not installed |

## Best Practices

- Use **nvm** to standardize Node.js versions.
- Prefer the **latest Node.js LTS** unless constrained by policy.
- Install only the plugins required for automation.
- Validate CLI installation and authentication early in pipelines.
- Avoid username/password authentication for long-lived automation.

## Relationship to the Lifecycle

This playbook covers the prerequisites for automating API management with the Anypoint CLI. Complete the prerequisites before running any CLI commands that interact with the Anypoint Platform, including:

- Publishing versioned APIs to Anypoint Exchange.
- Registering APIs in Anypoint API Manager.
- Deploying APIs to Anypoint Flex Gateway.
- Applying policies programmatically.
- Promoting APIs across environments.

Review [01-lifecycle-overview/README](file:///Users/abelisle/Documents/GitHub/Mule-Docs/anypoint-flex-apim-automation/01-lifecycle-overview/README.md) for a concise explanation of the API management automation lifecycle and how these stages relate to one another.
