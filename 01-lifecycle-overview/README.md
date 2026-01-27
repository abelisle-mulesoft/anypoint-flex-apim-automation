# Lifecycle Overview – Automating API Management for Flex Gateway

This repository complements the MuleSoft blog article **Automating API Management for Flex Gateway with the Anypoint CLI**.

The blog article introduces *why* and *what* to automate in API management with Flex Gateway: the lifecycle, its rationale, and how Anypoint Exchange, Anypoint API Manager, and Anypoint Flex Gateway fit together.

This repository focuses on *how*. It provides practical guidance, tested CLI examples, and patterns for implementing that lifecycle using the Anypoint Platform Command Line Interface (CLI).

## Lifecycle at a Glance

Automating API management for Flex Gateway typically follows this sequence:

1. **Source control is the system of record**
   API specifications and configuration are versioned in the source control system, and new versions trigger automation.
2. **Publish versioned assets to Anypoint Exchange**
   APIs are cataloged as immutable, versioned assets identified by a groupId, assetId, and semantic version (GAV).
3. **Register APIs in Anypoint API Manager**
   Published Exchange assets are registered as API instances in a specific environment and associated with Flex Gateway.
4. **Deploy APIs to Flex Gateway**
   API instances are deployed to managed or self-managed Flex Gateway targets.
5. **Apply policies and governance**
   Security, traffic management, and governance policies are applied programmatically.
6. **Promote APIs across environments**
   Fully configured APIs are promoted through environments, for example, from development to testing.

Each step depends on identifiers and metadata from the previous one. Automation scripts must preserve and reuse these values to ensure reliability and idempotency.

## How This Repository Is Organized

Each folder in this repository corresponds to one stage of the lifecycle described in the blog article.

- **00-prerequisites/**
  Install and authenticate the Anypoint CLI for non-interactive, CI/CD-friendly usage.
- **02-exchange-cataloging/**
  Publish APIs and related assets to Anypoint Exchange.
- **03-api-manager/**
  Register APIs in Anypoint API Manager and manage API instances for Flex Gateway.
- **04-flex-gateway/**
  Deploy APIs to managed or self-managed Flex Gateway targets.
- **05-policies-and-promotion/**
  Apply policies and promote APIs across environments.
- **06-reference/**
  Shared concepts, identifier models, and common pitfalls are referenced throughout the repository.

Within each lifecycle stage, you will typically find:

- A **conceptual guide** explaining mechanics and intent
- A **CLI workpad** containing tested commands and practical patterns

## Assumptions and Scope

This repository assumes that:

- You are using Anypoint CLI 4.x.
- Authentication is performed using a connected app or another non-interactive method suitable for automation.
- Flex Gateway is operating in **connected mode**.
- CI/CD pipeline design is outside the scope of these documents.

The goal is not to replace MuleSoft’s official documentation but to bridge the gap between product capabilities and real-world automation.

## Where to Start

If you are new to the repository:

1. Review the prerequisites in folder 00-prerequisites/.
2. Start with 02-exchange-cataloging/ and follow the lifecycle in order.
3. Use the workpad documents as reference material when building automation scripts.

## Relationship to the Blog Article

This repository stands on its own as an implementation guide for automating API management with the Anypoint CLI.

The accompanying MuleSoft blog article provides additional background, context, and architectural perspective on the same lifecycle. If you have already read the article, this repository picks up where it leaves off. If not, the material here remains fully usable on its own.

The two resources are intentionally aligned, but neither is required to understand or apply the other.