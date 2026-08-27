# Lesson 05 --- Finding Microsoft Graph Commands

## Learning Objectives

By the end of this lesson, you will be able to:

-   Discover Microsoft Graph PowerShell commands instead of memorizing
    them.
-   Use `Get-Command` and `Get-Help` with Graph cmdlets.
-   Use `Find-MgGraphCommand` to research Graph operations.
-   Use `Find-MgGraphPermission` to research permissions.
-   Identify whether a command is primarily read or write oriented.
-   Build a repeatable Graph command-discovery workflow.

------------------------------------------------------------------------

# Why Command Discovery Matters

Microsoft Graph PowerShell contains a very large number of cmdlets.

You do not need to memorize them.

A better workflow is:

``` text
Define the task
      ↓
Find the command
      ↓
Read Help
      ↓
Research permissions
      ↓
Connect with least privilege
      ↓
Test safely
```

------------------------------------------------------------------------

# Start with Get-Command

Search for Graph commands related to users:

``` powershell
Get-Command -Name '*MgUser*'
```

Search a particular module:

``` powershell
Get-Command -Module Microsoft.Graph.Users
```

Inspect a specific command:

``` powershell
Get-Command Get-MgUser
```

Pay attention to the verb:

``` text
Get       → retrieve
New       → create
Update    → modify
Remove    → delete
```

------------------------------------------------------------------------

# Use Get-Help

Once you find a command:

``` powershell
Get-Help Get-MgUser
```

Examples:

``` powershell
Get-Help Get-MgUser -Examples
```

Parameter help:

``` powershell
Get-Help Get-MgUser -Parameter UserId
```

This is often faster and safer than copying an unfamiliar command from
the internet.

------------------------------------------------------------------------

# Find-MgGraphCommand

Microsoft Graph PowerShell includes a specialized discovery cmdlet:

``` powershell
Find-MgGraphCommand -Command Get-MgUser
```

It can help connect a PowerShell cmdlet to the underlying Microsoft
Graph API operation.

Depending on the command, the results can help you identify:

``` text
Command
Module
HTTP method
Graph URI
Permissions
```

------------------------------------------------------------------------

# HTTP Methods

You may encounter methods such as:

``` text
GET
POST
PATCH
DELETE
```

A useful beginner mapping is:

``` text
GET      → retrieve data
POST     → commonly create something or perform an action
PATCH    → update something
DELETE   → delete something
```

This gives you another clue about the risk of an operation.

------------------------------------------------------------------------

# Find-MgGraphPermission

Use:

``` powershell
Find-MgGraphPermission 'User.Read'
```

You can also search a broader term:

``` powershell
Find-MgGraphPermission user
```

Review the returned permission information rather than selecting the
broadest permission available.

------------------------------------------------------------------------

# Combine the Discovery Tools

Suppose your task is:

> Retrieve Microsoft Entra users for a report.

Start with:

``` powershell
Get-Command -Name '*MgUser*'
```

Then:

``` powershell
Get-Help Get-MgUser -Examples
```

Then:

``` powershell
Find-MgGraphCommand -Command Get-MgUser
```

Finally, research the permissions required for the operation.

------------------------------------------------------------------------

# Modules Matter

The Graph SDK is divided into modules.

Examples include:

``` text
Microsoft.Graph.Authentication
Microsoft.Graph.Users
Microsoft.Graph.Groups
Microsoft.Graph.Identity.DirectoryManagement
```

If a command is unavailable, determine which module contains it before
assuming there is a problem with Graph.

------------------------------------------------------------------------

# Command Discovery Checklist

Before using an unfamiliar Graph command, ask:

``` text
[ ] What task am I trying to perform?
[ ] Which cmdlet performs it?
[ ] Which module contains it?
[ ] What does Get-Help say?
[ ] Is it a read or write operation?
[ ] Which permissions are required?
[ ] Am I using stable v1.0 functionality?
[ ] Am I connected to the correct tenant?
```

------------------------------------------------------------------------

# Common Beginner Mistakes

## Memorizing Instead of Discovering

Learn how to find commands rather than trying to remember the entire
SDK.

## Ignoring the Verb

Always notice whether the command begins with:

``` text
Get
New
Update
Remove
```

## Requesting the Broadest Permission

The goal is not to find a permission that definitely works.

The goal is to find the least-privileged permission appropriate for the
task.

------------------------------------------------------------------------

# Key Takeaways

-   Use `Get-Command` to discover Graph cmdlets.
-   Use `Get-Help` to understand syntax and parameters.
-   Use `Find-MgGraphCommand` to research Graph operations.
-   Use `Find-MgGraphPermission` to research permissions.
-   HTTP methods can help you recognize read and write operations.
-   The Graph SDK is divided into modules.
-   Command discovery is more valuable than command memorization.

------------------------------------------------------------------------

# Lab

Continue to:

[Lab 05 --- Finding Microsoft Graph
Commands](../labs/lesson-05-lab-05-finding-microsoft-graph-commands.md)

------------------------------------------------------------------------

## Additional Resources

-   [Find Microsoft Graph PowerShell
    commands](https://learn.microsoft.com/powershell/microsoftgraph/find-mg-graph-command)
-   [Find Microsoft Graph
    permissions](https://learn.microsoft.com/powershell/microsoftgraph/find-mg-graph-permission)
-   [Microsoft Graph PowerShell
    reference](https://learn.microsoft.com/powershell/microsoftgraph/)
