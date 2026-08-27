# Lesson 04 --- Microsoft Graph Permissions and Scopes

## Learning Objectives

By the end of this lesson, you will be able to:

-   Explain why Microsoft Graph requires permissions.
-   Define delegated permissions and application permissions.
-   Explain what a scope is in delegated access.
-   Recognize permission naming patterns.
-   Understand consent at a beginner level.
-   Apply least privilege.
-   Distinguish read permissions from read/write permissions.
-   Inspect the scopes in your current Graph context.
-   Understand that some operations can require both Graph permissions
    and administrative authority.

------------------------------------------------------------------------

# Why Permissions Exist

Microsoft Graph can expose sensitive organizational data.

Examples include:

``` text
User profiles
Group membership
Devices
Mail
Files
Applications
Directory information
```

Microsoft Graph does not assume that every authenticated connection
should have access to everything.

Permissions define what an application or session is authorized to
access.

------------------------------------------------------------------------

# Authentication Is Not Permission

Remember:

``` text
Authentication
    ↓
Who are you?

Authorization
    ↓
What are you allowed to do?
```

You can successfully authenticate and still be denied access to a Graph
resource.

That is expected security behavior.

------------------------------------------------------------------------

# Two Major Permission Types

Microsoft Graph supports two primary access scenarios:

``` text
Delegated permissions
Application permissions
```

------------------------------------------------------------------------

# Delegated Permissions

Delegated permissions are used when a user is signed in.

Conceptually:

``` text
Signed-in user
      +
Delegated permission
      ↓
Graph request
```

The application acts on behalf of the user.

Delegated permissions are commonly called:

``` text
Scopes
```

This is the access model used in the early lessons of this course.

------------------------------------------------------------------------

# Application Permissions

Application permissions are used for app-only access.

There is no interactive signed-in user.

Conceptually:

``` text
Application identity
        ↓
Application permission
        ↓
Microsoft Graph
```

This is commonly used for unattended automation.

Because application permissions can provide broad organizational access,
they require careful design and administrative consent.

App-only authentication will be covered later.

------------------------------------------------------------------------

# Permission Naming

Graph permissions often use names such as:

``` text
User.Read
User.Read.All
User.ReadWrite.All
Group.Read.All
Group.ReadWrite.All
```

The name gives useful clues.

For example:

``` text
User
```

indicates the resource.

``` text
Read
```

indicates read access.

``` text
ReadWrite
```

indicates the ability to read and modify data.

``` text
All
```

often indicates access across a broader set of organizational resources
for that permission.

Always read the actual permission documentation instead of relying only
on the name.

------------------------------------------------------------------------

# Read vs. ReadWrite

Compare:

``` text
User.Read.All
```

and:

``` text
User.ReadWrite.All
```

If your task is:

> Generate a user inventory report.

a read permission is normally more appropriate than requesting write
access.

This is least privilege in practice.

------------------------------------------------------------------------

# Least Privilege

Least privilege means:

> Give an identity, application, or session only the access required to
> perform its task.

For Graph PowerShell:

``` text
Task
   ↓
Required Graph operation
   ↓
Required permission
   ↓
Connect with that permission
```

Avoid:

``` text
Request everything
   ↓
Figure out what was actually needed later
```

------------------------------------------------------------------------

# Consent

Requesting a delegated scope does not automatically mean it will be
granted.

Consent behavior depends on factors such as:

``` text
Permission requested
Tenant policies
User consent settings
Whether admin consent is required
```

Some permissions can require administrator consent.

Do not bypass organizational consent controls merely to complete a lab.

------------------------------------------------------------------------

# Your Current Scopes

After connecting:

``` powershell
Get-MgContext
```

Inspect:

``` powershell
(Get-MgContext).Scopes
```

You can also make the output easier to read:

``` powershell
(Get-MgContext).Scopes |
    Sort-Object
```

This is a good habit before sensitive administrative work.

------------------------------------------------------------------------

# A Minimal Training Connection

For a basic exercise involving only the signed-in user's profile, a
connection may use:

``` powershell
Connect-MgGraph -Scopes 'User.Read'
```

Then verify:

``` powershell
Get-MgContext
```

This is intentionally narrow.

------------------------------------------------------------------------

# A Broader Read Scenario

Suppose the task becomes:

> Build a report of users across the organization.

That may require a broader read permission such as:

``` text
User.Read.All
```

Whether you can consent to that permission depends on your tenant and
policies.

The important process is:

``` text
Requirement changed
      ↓
Permission requirement changed
      ↓
Review before requesting
```

------------------------------------------------------------------------

# Administrative Roles and Graph Permissions

A Graph permission does not always tell the entire authorization story.

Some operations may also depend on:

``` text
Microsoft Entra role
Resource ownership
RBAC
Other service-specific authorization
```

Microsoft Graph permissions answer part of the question:

``` text
What can this app/session request from Graph?
```

Your administrative identity may also need authority over the target
operation.

------------------------------------------------------------------------

# Permission Errors

Common authorization-related failures may include messages indicating:

``` text
Forbidden
Insufficient privileges
Access denied
Authorization request denied
```

When this happens:

1.  Confirm the command and resource.
2.  Confirm the current account.
3.  Confirm the tenant.
4.  Inspect current scopes.
5.  Research the command's required permissions.
6.  Determine whether admin consent or a role is also required.

Do not jump directly to the broadest permission.

------------------------------------------------------------------------

# Discovering Required Permissions

Microsoft Graph PowerShell provides discovery tools, including:

``` powershell
Find-MgGraphCommand
Find-MgGraphPermission
```

You will explore command and permission discovery in a later lesson.

For now, understand the principle:

> Determine permissions from the operation you intend to perform.

------------------------------------------------------------------------

# Permission Planning Example

Requirement:

``` text
Create a report of users.
```

Plan:

``` text
Need to read users
       ↓
Find appropriate read permission
       ↓
Connect
       ↓
Verify scopes
       ↓
Retrieve users
       ↓
Export report
```

Different requirement:

``` text
Modify user properties.
```

That is a different risk level and can require different permissions.

Do not treat them as the same task.

------------------------------------------------------------------------

# Permission Review Checklist

Before connecting for administrative work, ask:

``` text
What am I trying to do?
Which resource am I accessing?
Do I need read or write access?
Does this permission apply to one user or many?
Does it require admin consent?
Does the signed-in user need an administrative role?
Am I in the correct tenant?
```

------------------------------------------------------------------------

# Avoid Permission Creep

Permission creep happens when scripts or applications accumulate
permissions over time that they no longer need.

Example:

``` text
Version 1 needs read access
Version 2 temporarily needs write access
Version 3 goes back to reporting
```

If the broad permission is never removed or reconsidered, unnecessary
access remains.

Treat permissions as something to review, not a one-time setup detail.

------------------------------------------------------------------------

# Common Beginner Mistakes

## Confusing Roles and Scopes

A Global Administrator role does not mean a Graph session automatically
contains every Graph permission.

Likewise, a Graph permission does not necessarily provide every
administrative authority required for an operation.

------------------------------------------------------------------------

## Using ReadWrite for Read-Only Reporting

If the task is read-only, start by looking for a read permission.

------------------------------------------------------------------------

## Copying Scope Lists from Random Scripts

A copied script may request far more access than your task requires.

Understand every requested scope.

------------------------------------------------------------------------

## Ignoring the Tenant

Permissions are granted in a tenant context.

Always verify where you are connected.

------------------------------------------------------------------------

## Treating Consent as an Annoyance

Consent is a security control.

If your organization requires administrator approval, follow that
process.

------------------------------------------------------------------------

# Key Takeaways

-   Microsoft Graph uses permissions to authorize access.
-   Delegated permissions are used with a signed-in user.
-   Application permissions are used for app-only access.
-   Delegated permissions are commonly called scopes.
-   Permission names often indicate resource and access level.
-   Read and ReadWrite permissions carry different risk.
-   Apply least privilege.
-   Consent may be controlled by tenant policy.
-   Some operations may require Graph permissions plus appropriate
    administrative authority.
-   Inspect current scopes with `Get-MgContext`.
-   Research the actual permission requirement before requesting broader
    access.

------------------------------------------------------------------------

# Lab

Continue to:

[Lab 04 --- Permissions and
Scopes](../labs/lesson-04-lab-04-permissions-and-scopes.md)

------------------------------------------------------------------------

## Additional Resources

-   [Microsoft Graph permissions
    overview](https://learn.microsoft.com/graph/permissions-overview)
-   [Get started with Microsoft Graph
    PowerShell](https://learn.microsoft.com/powershell/microsoftgraph/get-started)
-   [Microsoft Graph PowerShell authentication
    commands](https://learn.microsoft.com/powershell/microsoftgraph/authentication-commands)
