# Introduction

## Abstract

This informal document discusses three authentication approaches when using the Anypoint Platform Command-Line Interface (CLI) — or simply the Anypoint CLI. It recommends using a connected app and provides resources to help you get started.

## Purpose

The purpose of this document is to complement the documentation that MuleSoft publishes, not to replace it. It aims to provide additional documentation and examples to help you get started quickly.

# Authenticating to the Anypoint CLI

## Overview

The article [Authentication to the Anypoint Platform CLI](https://docs.mulesoft.com/anypoint-cli/latest/) outlines three authentication approaches: using a bearer token, a client ID and client secret, or a username and password. However, it overlooks the critical importance of applying the principle of least privilege and lacks practical specificity. Each authentication method can vary in real-world applications. For example, depending on your Anypoint Platform configuration, you might use a personal or dedicated account (i.e., username and password), a connected app, or a SAML assertion to generate a bearer token. 

The purpose of this repository is to lay the groundwork for CI/CD pipelines that automate API management for Anypoint Flex Gateway. Although bearer tokens provide short-lived, scoped access, they introduce additional steps without significantly enhancing security, since initial authentication and secure credential management remain equally critical. Whether using accounts, connected apps, or SAML assertions to generate tokens, the fundamental security posture depends on how these credentials are handled in the pipeline. 

While authenticating to the Anypoint CLI with a username and password is possible, it is generally not recommended for CI/CD pipelines. Personal accounts often introduce unnecessary permissions and make password rotation more difficult. A dedicated account with limited permissions helps mitigate risks but still involves securely storing long-lived credentials and managing their rotation. Username and password authentication is best reserved for ad-hoc testing or temporary manual use. 

A connected app with a client ID and client secret is well-suited for CI/CD pipelines, as it avoids user credential dependency and enables the principle of least privilege. A dedicated connected app for automation allows scoped access, limited permissions, and straightforward credential rotation. Although the client secret is long-lived and requires secure storage, this method is safer, more maintainable, and auditable, without the need for frequent token refreshes.

## Summary of Authentication Methods

| Authentication Method | Pros | Cons | Recommended Use |
|-----------------------|------|------|-----------------|
| **Bearer Token** | Short-lived, scoped access | Requires other credentials to generate; expires quickly | Rarely used in CI/CD |
| **Client ID and Secret** | Best for automation; supports least privilege | Requires secure secret storage |  Preferred for CI/CD |
| **Username and Password** | Simple for ad-hoc use | Long-lived, hard to rotate, risky for automation | Manual testing only |

## Using a Connected App with the Anypoint CLI

Several articles within the MuleSoft documentation, as well as resources available on the internet, outline how to create a connected app that acts on its own behalf. This section, nonetheless, provides a step-by-step approach for configuring a connected app and using its client ID and secret for authentication when executing Anypoint CLI commands.

- First, in a browser, log in to the Anypoint Platform (https://anypoint.mulesoft.com).
- On the landing page, select **Access Management** towards the bottom right of the page.
- In **Access Management**, select the **Connected Apps** option from the left menu.
- On the **Connected Apps** page, you can optionally select a **Business Group** from the drop-down list.

> [!TIP]
> The Business Group selected directly influences the business groups available when adding scopes to the connected app. For example, selecting the root organization enables you to select the root organization and any of its descendants.
>
> As a reminder, a scope is a role with associated permissions that determines the actions the connected app can perform within a business group and environment [1]. 

- Click the **Create app** button to create a new connected app.
- On the **Create app** form:
  - Enter a **Name** for your connected app,
  - Select the option **App acts on its own behalf (client credentials)** for the **Type**, and
  - Click the **Add Scopes** button.

<img src="assets/images/cli-authen-2-3-01-create-app-form.png" style="margin-left:60px;width:6.5in;height:3.2in"/>

- In the **Add Scopes** dialog:
  - For step 1, **Add Scopes**, select the scopes listed in the table below.

<img src="assets/images/cli-authn-2-3-02-create-app-add-scopes.png" style="margin-left:60px;width:4.0in;height:4.5in"/>

<style>
  table {
    margin-left:60px;
  }
</style>

| Scopes   | Roles                |
| -------- | -------------------- |
| Exchange | Exchange Contributor |
|          |                      |
|          |                      |


  - For step 2, **Select Business Groups**, select all the relevant business groups; i.e., where you plan to register and manage APIs.
  - For step 3, **Review,** optionally review your selection and click the **Add Scopes** button.
- Click the **Save** button.
- Finally, on the **Connected Apps** page, you can copy the client ID and client secret by clicking the **Copy Id** and **Copy Secret** buttons, respectively. You will need those values for authentication when executing Anypoint CLI commands.

<img src="assets/images/cli-authn-2-3-05-client-id-client-secret.png" style="margin-left:30px;width:6.5in;height:3.0in"/>

# References

- [1] https://docs.mulesoft.com/access-management/creating-connected-apps-dev#create-connected-app-on-its-own-behalf



# Additionnal Resources

- Authentication to the Anypoint Platform CLI - https://docs.mulesoft.com/anypoint-cli/latest/auth
- How to generate your Authorization Bearer token for Anypoint Platform - https://help.salesforce.com/s/articleView?id=001115323&type=1
- Obtaining an API Bearer Token Using a SAML Assertion - https://docs.mulesoft.com/access-management/saml-bearer-token
- Getting the Bearer Token for a Connected App Example - https://docs.mulesoft.com/access-management/connected-app-bearer-token-example
- How to Get the Anypoint Authorization Access or Bearer Token from Chrome Browser Session - https://help.salesforce.com/s/articleView?id=001116775&type=1
- How long does an Anypoint bearer token expire? - https://help.salesforce.com/s/articleView?id=001118158&type=1
- How to use Anypoint CLI with a connected app - https://help.salesforce.com/s/articleView?id=001117606&type=1
- Creating Connected Apps - https://docs.mulesoft.com/access-management/creating-connected-apps-dev
