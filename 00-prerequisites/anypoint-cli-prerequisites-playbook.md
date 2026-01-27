# Anypoint CLI Prerequisites – CLI Playbook

This playbook provides **tested, practical command-line patterns** for preparing a workstation or CI/CD runner to use the Anypoint Platform Command Line Interface (CLI).

It focuses on **installation, verification, and basic smoke testing** required before automating API management tasks such as cataloging APIs, registering them in API Manager, and deploying them to Anypoint Flex Gateway.

> [!NOTE]
> While the [official documentation](https://docs.mulesoft.com/anypoint-cli/latest/install) specifies `Node.js` versions 18.0.0 to 20.0.0, all examples in this repository have been authored and successfully tested with `Node.js` 22.20.0 LTS and `npm` 11.6.2. This indicates that newer LTS versions of Node.js may also work in practice, even if they are not explicitly listed as supported.

## Scope and Assumptions

This playbook assumes that:

- You are installing Anypoint CLI 4.x.
- You are operating on macOS, Linux, or a compatible CI/CD runner.
- You have sufficient privileges to install Node.js, npm packages, and global CLI tools.
- Authentication strategy is addressed separately (for example, connected apps).

This playbook does **not** cover:
- API lifecycle automation.
- CI/CD pipeline design.
- Policy configuration or deployment workflows.

## How to Use This Playbook

Use this document as:

- A **repeatable checklist** for setting up new machines or build agents.
- A **reference for troubleshooting installation issues**.
- A **baseline validation step** before running automation scripts.

All commands have been tested and are safe to reuse once adapted to your environment.

## Required Tooling

The Anypoint CLI depends on the following tools:

| Tool | Purpose |
|----|--------|
| Node.js | Runtime required by the Anypoint CLI |
| npm | Package manager used to install the CLI |
| nvm (recommended) | Manage Node.js versions consistently |

## Verify or Install Node.js and npm

Using **nvm** is strongly recommended to ensure predictable Node.js versions across environments.

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

Install the **latest available LTS version** of Node.js:

```shell
nvm install --lts
nvm use --lts
```

Verify the installation:

```shell
node -v
npm -v
```

> **Note**  
> Although this repository was authored using Node.js 22.x, the Anypoint CLI does not require that specific version. Using the latest LTS version helps ensure security updates and long-term support.

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

This playbook supports the **prerequisites stage** of the automated API management lifecycle described in the MuleSoft blog article **_Automating API Management for Flex Gateway with the Anypoint CLI_**. It should be completed before executing any Exchange, API Manager, or Flex Gateway automation.

