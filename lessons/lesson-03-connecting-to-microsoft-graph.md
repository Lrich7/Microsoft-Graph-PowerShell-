# Lesson 03 --- Connecting to Microsoft Graph

## Learning Objectives

By the end of this lesson, you will be able to:

-   Explain why Graph PowerShell requires authentication.
-   Connect with `Connect-MgGraph`.
-   Understand interactive and device-code delegated authentication.
-   Verify a connection with `Get-MgContext`.
-   Identify the signed-in account, tenant, authentication type, and
    scopes.
-   Explain why context verification is important.
-   Disconnect with `Disconnect-MgGraph`.
-   Follow a safe connection workflow.

------------------------------------------------------------------------

# Authentication Comes Before Administration

Microsoft Graph contains protected cloud data.

Before accessing it, Graph must know who or what is making the request.

The primary Graph PowerShell connection command is:

``` powershell
Connect-MgGraph
```

The Graph authentication module uses modern Microsoft authentication to
obtain an access token for the session.

------------------------------------------------------------------------

# Start with Delegated Access

This course begins with delegated authentication.

Conceptually:

``` text
You sign in
    ↓
Graph PowerShell
    ↓
Acts on your behalf
    ↓
Microsoft Graph
```

Your effective access depends on both the permissions granted to the
application/session and the access available to the signed-in identity.

------------------------------------------------------------------------

# A Simple Connection

A Graph connection includes the permissions needed for the task.

For a basic self-profile scenario, an example is:

``` powershell
Connect-MgGraph -Scopes 'User.Read'
```

This can open an interactive authentication experience.

The exact sign-in and consent experience depends on your environment and
tenant policies.

------------------------------------------------------------------------

# Device Code Authentication

In environments where interactive browser authentication is
inconvenient, Graph PowerShell also supports device authentication.

Example:

``` powershell
Connect-MgGraph `
    -Scopes 'User.Read' `
    -UseDeviceAuthentication
```

PowerShell provides instructions for completing sign-in.

Be careful when multiple Microsoft accounts are already signed into your
browser.

Always verify which identity you used.

------------------------------------------------------------------------

# Verify the Connection

Connecting successfully is not the end of the process.

Immediately run:

``` powershell
Get-MgContext
```

This returns information about the current Graph session.

Useful fields include:

``` text
Account
TenantId
Scopes
AuthType
AppName
ContextScope
```

------------------------------------------------------------------------

# Why Get-MgContext Matters

Imagine you administer:

``` text
Production tenant
Test tenant
Client tenant
Personal developer tenant
```

A successful connection does not guarantee you connected to the intended
environment.

A safe habit is:

``` text
Connect
   ↓
Get-MgContext
   ↓
Verify
   ↓
Then administer
```

------------------------------------------------------------------------

# Inspect Specific Context Properties

Store the context:

``` powershell
$context = Get-MgContext
```

Then inspect:

``` powershell
$context.Account
```

``` powershell
$context.TenantId
```

``` powershell
$context.AuthType
```

``` powershell
$context.Scopes
```

This is normal PowerShell object usage.

------------------------------------------------------------------------

# Verify the Signed-In Account

Check:

``` powershell
(Get-MgContext).Account
```

Ask:

``` text
Is this the account I intended to use?
```

If not, disconnect before continuing.

------------------------------------------------------------------------

# Verify the Tenant

Check:

``` powershell
(Get-MgContext).TenantId
```

A tenant ID is a unique identifier for a Microsoft Entra tenant.

In real administration, you should know which tenant your script is
intended to target.

------------------------------------------------------------------------

# Verify the Authentication Type

Check:

``` powershell
(Get-MgContext).AuthType
```

For the interactive scenarios in this lesson, you should be working with
delegated access.

Later in the course, app-only authentication will look different.

------------------------------------------------------------------------

# Verify Scopes

Check:

``` powershell
(Get-MgContext).Scopes
```

This shows permissions associated with the current context.

Do not simply glance at the list.

Ask:

``` text
Why does this session have these permissions?
Are they appropriate for what I am about to do?
```

Lesson 04 focuses on this topic.

------------------------------------------------------------------------

# Connection Lifetime

A Graph PowerShell connection remains available in the session until it
is disconnected or the relevant session/authentication state ends.

You do not normally need to reconnect before every individual command.

Conceptually:

``` text
Connect once
   ↓
Run authorized Graph work
   ↓
Disconnect when finished
```

------------------------------------------------------------------------

# Disconnecting

Use:

``` powershell
Disconnect-MgGraph
```

Then check:

``` powershell
Get-MgContext
```

Disconnecting when finished is a good administrative habit, particularly
on shared or privileged workstations.

------------------------------------------------------------------------

# Reconnecting with Different Needs

As your task changes, required scopes may change.

Do not begin every session with a giant list of permissions "just in
case."

Instead:

``` text
Define task
   ↓
Determine permission
   ↓
Connect
   ↓
Verify
```

This supports least privilege.

------------------------------------------------------------------------

# Authentication vs. Authorization

These concepts are related but different.

## Authentication

``` text
Who are you?
```

Example:

``` powershell
Connect-MgGraph
```

## Authorization

``` text
What are you allowed to do?
```

This depends on permissions/scopes and, in some scenarios, directory
roles or other authorization controls.

A successful login does not mean every Graph command will succeed.

------------------------------------------------------------------------

# Failed Commands After Successful Sign-In

You may successfully connect and still receive errors such as:

``` text
Forbidden
Insufficient privileges
Authorization_RequestDenied
```

Possible reasons include:

``` text
Missing Graph permission
Consent not granted
Signed-in user lacks required role/access
Wrong tenant
Resource restrictions
```

Do not respond by automatically requesting the broadest permission
available.

Investigate the actual requirement.

------------------------------------------------------------------------

# Safe Connection Pattern

A useful interactive pattern is:

``` powershell
Connect-MgGraph -Scopes 'User.Read'

$context = Get-MgContext

$context |
    Select-Object Account, TenantId, AuthType, Scopes
```

After verifying the session, perform the intended read-only work.

When finished:

``` powershell
Disconnect-MgGraph
```

------------------------------------------------------------------------

# Common Beginner Mistakes

## Forgetting to Verify Context

Always verify:

``` text
Account
Tenant
Scopes
```

------------------------------------------------------------------------

## Signing In with the Wrong Browser Account

Multiple cached Microsoft accounts can cause confusion.

Read the account shown by:

``` powershell
Get-MgContext
```

------------------------------------------------------------------------

## Assuming Admin Role Equals Graph Permission

Microsoft Entra roles and Microsoft Graph permissions are related
authorization concepts, but they are not interchangeable.

Some operations can require appropriate Graph permissions and
appropriate administrative authority.

------------------------------------------------------------------------

## Requesting Broad Scopes to Avoid Errors

An authorization error is a reason to investigate---not automatically a
reason to request write access.

------------------------------------------------------------------------

## Leaving Privileged Sessions Open

Disconnect when your administrative task is complete.

------------------------------------------------------------------------

# Key Takeaways

-   Use `Connect-MgGraph` before accessing protected Graph resources.
-   This course begins with delegated access.
-   Interactive and device-code authentication are supported.
-   Use `Get-MgContext` immediately after connecting.
-   Verify account, tenant, authentication type, and scopes.
-   Authentication and authorization are different.
-   Successful authentication does not guarantee authorization for every
    operation.
-   Use least privilege.
-   Use `Disconnect-MgGraph` when finished.

------------------------------------------------------------------------

# Lab

Continue to:

[Lab 03 --- Connecting to Microsoft
Graph](../labs/lesson-03-lab-03-connecting-to-microsoft-graph.md)

------------------------------------------------------------------------

## Additional Resources

-   [Authentication commands in Microsoft Graph
    PowerShell](https://learn.microsoft.com/powershell/microsoftgraph/authentication-commands)
-   [Get started with Microsoft Graph
    PowerShell](https://learn.microsoft.com/powershell/microsoftgraph/get-started)
