# Lesson 07 --- Managing Users

## Learning Objectives

By the end of this lesson, you will be able to:

-   Distinguish user reporting from user modification.
-   Discover `New-MgUser`, `Update-MgUser`, and `Remove-MgUser`.
-   Plan a user creation safely.
-   Understand how user properties can be updated.
-   Explain why disabling or deleting users requires additional care.
-   Build a preview-first workflow for user changes.
-   Avoid placing credentials or secrets in scripts.

------------------------------------------------------------------------

# Moving from Read to Write

Previous lessons focused mainly on retrieving information.

This lesson introduces commands that can change Microsoft Entra ID:

``` powershell
New-MgUser
Update-MgUser
Remove-MgUser
```

> Do not practice user creation, modification, disabling, or deletion on
> production users merely to complete a training exercise.

------------------------------------------------------------------------

# Discover Before Changing

Before using an unfamiliar write command:

``` powershell
Get-Help New-MgUser -Examples
```

Then:

``` powershell
Find-MgGraphCommand -Command New-MgUser
```

Repeat this process for:

``` powershell
Update-MgUser
```

and:

``` powershell
Remove-MgUser
```

------------------------------------------------------------------------

# Permissions Change with the Task

Reading users and modifying users are different operations.

A reporting script may need only read permissions.

A management script may require write permissions.

Always research the least-privileged supported permission for the actual
operation.

------------------------------------------------------------------------

# Creating a User

`New-MgUser` creates a Microsoft Entra user.

User creation requires planning for information such as:

``` text
Display name
User principal name
Mail nickname
Account state
Password profile
Usage location when relevant
Department
Job title
```

The exact required properties depend on the operation and environment.

------------------------------------------------------------------------

# Password Safety

Never commit real passwords to GitHub.

Avoid scripts such as:

``` powershell
$Password = 'CompanyPassword123!'
```

in real repositories.

Also avoid committing:

``` text
Access tokens
Client secrets
Private keys
Certificates containing private keys
```

------------------------------------------------------------------------

# Updating a User

Use:

``` powershell
Update-MgUser
```

Conceptually:

``` powershell
Update-MgUser `
    -UserId '<verified-user-id>' `
    -Department 'IT'
```

Before running a change, verify the target.

A safe workflow is:

``` text
Find user
   ↓
Display current values
   ↓
Verify ID / UPN
   ↓
Preview proposed values
   ↓
Confirm authorization
   ↓
Make change
   ↓
Read user again
   ↓
Verify result
```

------------------------------------------------------------------------

# AccountEnabled

The `AccountEnabled` property affects whether the account can sign in.

Changing account state is a security-sensitive administrative action.

Do not disable accounts as casual practice.

------------------------------------------------------------------------

# Removing Users

`Remove-MgUser` deletes a user.

This course does not require you to delete a real user.

Learn how to discover the command, understand its permissions, and
recognize it as destructive.

------------------------------------------------------------------------

# Preview-First Automation

Bulk automation should normally begin by showing what it intends to
change.

A preview report could contain:

``` text
Target
Current value
Proposed value
Action
Validation status
```

This lets an administrator review the proposed operation before a change
phase begins.

------------------------------------------------------------------------

# Validate Targets

Do not target a user based only on display name.

Verify information such as:

``` text
Id
UserPrincipalName
DisplayName
Tenant
```

before changing anything.

------------------------------------------------------------------------

# Common Beginner Mistakes

## Practicing Write Commands on Real Employees

Use a controlled test identity or lab tenant.

## Skipping Verification

Read the object again after a change.

## Performing Bulk Changes Without Preview

Validate the input and proposed actions first.

## Committing Secrets to Git

Training repositories should never contain real credentials.

## Treating Delete as a Normal Practice Command

Deletion is destructive.

------------------------------------------------------------------------

# Key Takeaways

-   User management introduces write operations.
-   Discover commands and permissions before using them.
-   Use a controlled test environment for practice.
-   Verify the exact user before making changes.
-   Build preview and validation stages into automation.
-   Read back the object after a change.
-   Never commit real credentials or secrets to Git.
-   Treat account disabling and deletion as sensitive operations.

------------------------------------------------------------------------

# Lab

Continue to:

[Lab 07 --- Managing Users](../labs/lesson-07-lab-07-managing-users.md)

------------------------------------------------------------------------

## Additional Resources

-   [New-MgUser](https://learn.microsoft.com/powershell/module/microsoft.graph.users/new-mguser)
-   [Update-MgUser](https://learn.microsoft.com/powershell/module/microsoft.graph.users/update-mguser)
-   [Microsoft Graph permissions
    reference](https://learn.microsoft.com/graph/permissions-reference)
