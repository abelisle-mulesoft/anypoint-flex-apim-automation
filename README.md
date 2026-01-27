# Automating API Management for Flex Gateway

This repository contains **work-in-progress documentation and examples** for automating API management for **Anypoint Flex Gateway** with the **Anypoint Platform Command Line Interface (CLI)**.

The goal of this repository is to provide a **practical, lifecycle-oriented companion** to the MuleSoft blog article **Automating API Management for Flex Gateway with the Anypoint CLI**. It focuses on real-world automation patterns rather than exhaustive reference documentation.

## Repository Status

> [!IMPORTANT]
> This repository is evolving and should be considered **work in progress**.

Only the following sections are currently complete and intended for early consumption:

- assets/
- 00-prerequisites/
- 01-lifecycle-overview/

The remaining lifecycle stages are **not yet completed**:

- 02-exchange-cataloging/
- 03-api-manager/
- 04-flex-gateway/
- 05-policies-and-promotion/
- 06-reference/

These folders will be populated as the repository evolves.

## What This Repository Covers

When complete, this repository will document how to automate the full API management lifecycle for Flex Gateway, including:

- Publishing versioned API assets to Anypoint Exchange.
- Registering APIs in API Manager.
- Deploying APIs to Anypoint Flex Gateway.
- Applying policies programmatically.
- Promoting APIs across environments.

The emphasis is on **automation-first usage of the Anypoint CLI**, suitable for scripting and CI/CD pipelines.

## How to Use This Repository Today

If you are exploring the repository as it is now:

1. Start with [00-prerequisites/anypoint-cli-installation.md](./00-prerequisites/anypoint-cli-installation.md) to install the Anypoint CLI and [00-prerequisites/anypoint-cli-authentication.md](./00-prerequisites/anypoint-cli-authentication.md) to plan and decide your authentication approach.
2. Review [01-lifecycle-overview/README.md](./01-lifecycle-overview/README.md) for a concise explanation of the automation lifecycle and the repository's organization.

Each completed section is designed to be **self-contained**, with clear lifecycle placement and forward navigation.

> [!TIP]
> Review the document  [anypoint-cli-prerequisites-playbook](./00-prerequisites/anypoint-cli-prerequisites-playbook.md) within the `00-prerequisites` section, which provides **tested, practical command-line patterns** for preparing a workstation or CI/CD runner to use the Anypoint Platform Command Line Interface (CLI). 

## Design Principles

This repository follows a few guiding principles:

- **Lifecycle-driven structure** rather than feature-by-feature documentation.
- **Separation of concepts and execution**, with CLI playbooks capturing tested command patterns.
- **Alignment with official MuleSoft documentation** without duplicating it.
- **Practical experience over theoretical completeness**.

## Relationship to the MuleSoft Blog

The accompanying MuleSoft blog article explains *why* automating API management for Flex Gateway matters and how the Anypoint Platform components fit together. This repository focuses on implementing that lifecycle using the Anypoint CLI. Both resources are designed to complement each other, but this repository can still be used on its own.

## Contributing and Feedback

Because this repository is under development, feedback and suggestions are welcome. Content, structure, and examples may change as more lifecycle stages are added.

## License

This repository is licensed under the Apache License, Version 2.0. Unless otherwise stated, all content is provided as-is, without warranties or guarantees of support.
