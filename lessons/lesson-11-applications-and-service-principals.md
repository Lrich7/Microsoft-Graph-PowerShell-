# Lesson 11 --- Applications and Service Principals

## Learning Objectives

By the end of this lesson, you will be able to:

-   Explain the difference between an application registration and a
    service principal.
-   Retrieve applications with `Get-MgApplication`.
-   Retrieve service principals with `Get-MgServicePrincipal`.
-   Recognize application IDs and object IDs.
-   Inspect application credentials without exposing secret material.
-   Build a read-only application inventory.
-   Explain why application permissions require careful review.

------------------------------------------------------------------------

# Two Related Objects

Microsoft Entra applications commonly involve two related concepts:

``` text
Application object
Service principal
```

The application object describes the application definition.

A service principal represents the application's identity in a tenant.

A useful mental model is:

``` text
Application registration
        ↓
Application definition

Service principal
        ↓
Tenant-local identity used for access
```

------------------------------------------------------------------------

# Retrieve Applications

Use:

``` powershell
Get-MgApplication
```

Example:

``` powershell
Get-MgApplication -Top 10 |
    Select-Object Id, AppId, DisplayName
```

------------------------------------------------------------------------

# Id vs. AppId

Applications commonly expose:

``` text
Id
AppId
```

`Id` is the Microsoft Graph directory-object ID.

`AppId` is the application/client ID.

They are different identifiers.

------------------------------------------------------------------------

# Retrieve Service Principals

Use:

``` powershell
Get-MgServicePrincipal
```

Example:

``` powershell
Get-MgServicePrincipal -Top 10 |
    Select-Object Id, AppId, DisplayName, ServicePrincipalType
```

------------------------------------------------------------------------

# Match an Application to a Service Principal

The `AppId` can help relate an application definition to service
principals associated with that application.

Do not assume the Graph object IDs will match.

------------------------------------------------------------------------

# Credentials

Application objects can have credential metadata such as certificate/key
credentials and password credentials.

Inventorying credential expiration can be useful.

However:

> Never print, export, or commit actual secret values to a repository.

Graph generally does not allow you to retrieve an existing client
secret's secret text after creation. Treat any newly generated secret
value as sensitive from the moment it exists.

------------------------------------------------------------------------

# Why Service Principals Matter

Service principals can receive:

``` text
Microsoft Graph permissions
Application access
Directory roles in some scenarios
Resource-specific permissions
```

This makes them important security inventory objects.

------------------------------------------------------------------------

# Read-Only Application Inventory

A useful first report might include:

``` text
DisplayName
AppId
Object Id
Sign-in audience
Credential expiration metadata
```

A separate service-principal report might include:

``` text
DisplayName
AppId
Object Id
ServicePrincipalType
AccountEnabled
```

------------------------------------------------------------------------

# Application Permission Review

An app-only automation can operate without an interactive user.

That makes application permissions powerful.

Before granting them:

``` text
Understand the automation requirement
Identify the least privilege
Understand admin consent
Protect the credential
Document the owner
Review permissions over time
```

------------------------------------------------------------------------

# Common Beginner Mistakes

## Confusing AppId and Id

They identify different things.

## Treating Application and Service Principal as Synonyms

They are related but distinct directory objects.

## Putting Client Secrets in Git

Never commit secrets.

## Ignoring Old Credentials

Credential expiration should be part of application inventory and
lifecycle management.

------------------------------------------------------------------------

# Key Takeaways

-   Use Microsoft Graph PowerShell deliberately and verify your Graph
    context before administrative work.
-   Prefer read-only discovery and reporting before introducing changes.
-   Request only the permissions required for the task.
-   Inspect returned objects and properties rather than relying only on
    formatted screen output.
-   Validate targets before performing administrative changes.

------------------------------------------------------------------------

# Lab

Continue to:

[Lab 11 --- Applications and Service
Principals](../labs/lesson-11-lab-11-applications-and-service-principals.md)

------------------------------------------------------------------------

## Additional Resources

-   [Get-MgApplication](https://learn.microsoft.com/powershell/module/microsoft.graph.applications/get-mgapplication)
-   [Get-MgServicePrincipal](https://learn.microsoft.com/powershell/module/microsoft.graph.applications/get-mgserviceprincipal)
-   [Application and service principal
    objects](https://learn.microsoft.com/entra/identity-platform/app-objects-and-service-principals)
