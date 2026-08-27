# Lesson 12 --- Directory Roles

## Learning Objectives

By the end of this lesson, you will be able to:

-   Explain what Microsoft Entra directory roles are.
-   Distinguish role definitions from role assignments.
-   Discover Graph commands for role-management data.
-   Retrieve role definitions and assignments in a read-only manner.
-   Understand why privileged roles deserve additional scrutiny.
-   Recognize that Privileged Identity Management adds another layer to
    role governance.
-   Build a basic privileged-access inventory.

------------------------------------------------------------------------

# What Are Directory Roles?

Microsoft Entra roles grant administrative capabilities.

Examples include roles related to:

``` text
User administration
Groups
Applications
Security
Authentication
Global administration
```

Role assignment is security-sensitive because it can grant substantial
administrative authority.

------------------------------------------------------------------------

# Definitions vs. Assignments

Two concepts matter:

``` text
Role definition
Role assignment
```

A role definition describes the role.

A role assignment connects a principal to that role.

Conceptually:

``` text
Role definition
      +
Principal
      ↓
Role assignment
```

------------------------------------------------------------------------

# Unified Role Management

Microsoft Graph exposes role-management resources through unified
role-management APIs.

Discover relevant commands:

``` powershell
Get-Command '*MgRoleManagementDirectory*'
```

Look for commands related to:

``` text
RoleDefinition
RoleAssignment
```

Then use:

``` powershell
Get-Help
Find-MgGraphCommand
```

before querying the tenant.

------------------------------------------------------------------------

# Retrieve Role Definitions

A typical command is:

``` powershell
Get-MgRoleManagementDirectoryRoleDefinition
```

Select useful properties:

``` powershell
Get-MgRoleManagementDirectoryRoleDefinition |
    Select-Object Id,DisplayName,Description,IsBuiltIn
```

------------------------------------------------------------------------

# Retrieve Role Assignments

Use:

``` powershell
Get-MgRoleManagementDirectoryRoleAssignment
```

Assignments include identifiers that connect:

``` text
Principal
Role definition
Directory scope
```

Additional lookups may be needed to turn IDs into human-readable names.

------------------------------------------------------------------------

# Resolve IDs

Administrative reports often begin with IDs.

Your script may need to:

1.  Retrieve role assignments.
2.  Retrieve role definitions.
3.  Retrieve or resolve principals.
4.  Join the information into a readable report.

This is a good example of why PowerShell objects, loops, hashtables, and
custom objects are useful.

------------------------------------------------------------------------

# Privileged Roles

Not every role has the same risk.

Highly privileged assignments deserve careful monitoring.

A useful report can answer:

``` text
Who has administrative roles?
Which roles are assigned?
Are assignments expected?
Are assignments permanent or governed through PIM?
```

------------------------------------------------------------------------

# Privileged Identity Management

Microsoft Entra Privileged Identity Management (PIM) can govern
privileged access using concepts such as eligibility and activation.

A simple role-assignment query does not necessarily tell the entire PIM
story.

Treat PIM as an additional governance layer that you may need to query
separately for a complete privileged-access audit.

------------------------------------------------------------------------

# Do Not Practice Role Assignment in Production

Adding a role assignment can grant powerful administrative access.

For this course, the lab remains read-only.

If you later automate role assignments, use a controlled environment,
least privilege, approval, and explicit validation.

------------------------------------------------------------------------

# Common Beginner Mistakes

## Confusing a Role with an Assignment

The definition describes the role; the assignment connects it to a
principal.

## Ignoring Scope

Role assignments can include scope information.

## Treating All Admin Roles as Equivalent

Risk varies greatly.

## Assuming One Query Fully Represents PIM

PIM governance can require additional role-management queries.

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

[Lab 12 --- Directory
Roles](../labs/lesson-12-lab-12-directory-roles.md)

------------------------------------------------------------------------

## Additional Resources

-   [Microsoft Entra roles
    documentation](https://learn.microsoft.com/entra/identity/role-based-access-control/)
-   [Microsoft Graph role
    management](https://learn.microsoft.com/graph/api/resources/rolemanagement-read-directory)
