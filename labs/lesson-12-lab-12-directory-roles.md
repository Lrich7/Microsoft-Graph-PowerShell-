# Lab 12 --- Directory Roles

## Lab Objective

Create a read-only directory-role inventory. Do not add or remove
administrative role assignments in this lab.

------------------------------------------------------------------------

# Exercise 1 --- Discover Role Commands

``` powershell
Get-Command '*MgRoleManagementDirectory*'
```

Find commands for:

``` text
Role definitions
Role assignments
```

Then use `Find-MgGraphCommand` to research each.

------------------------------------------------------------------------

# Exercise 2 --- Retrieve Role Definitions

With an authorized read connection:

``` powershell
Get-MgRoleManagementDirectoryRoleDefinition |
    Select-Object Id,DisplayName,IsBuiltIn
```

Sort by display name.

------------------------------------------------------------------------

# Exercise 3 --- Retrieve Assignments

``` powershell
Get-MgRoleManagementDirectoryRoleAssignment -All
```

Inspect one:

``` powershell
$assignment = Get-MgRoleManagementDirectoryRoleAssignment -Top 1
$assignment | Get-Member
```

Identify:

``` text
PrincipalId
RoleDefinitionId
DirectoryScopeId
```

------------------------------------------------------------------------

# Exercise 4 --- Resolve a Role Name

Choose one assignment.

Match its `RoleDefinitionId` to the role definitions you retrieved.

Display:

``` text
PrincipalId
Role name
Directory scope
```

``` powershell
# Your solution
```

------------------------------------------------------------------------

# Exercise 5 --- Risk Review

Choose three role definitions and write why each could matter to an IT
security review.

``` text
1. ____________________________________

2. ____________________________________

3. ____________________________________
```

------------------------------------------------------------------------

# Exercise 6 --- PIM Question

Why might a simple active role-assignment report not provide a complete
picture of privileged access in an organization using PIM?

``` text
____________________________________________________
```

------------------------------------------------------------------------

# Knowledge Check

1.  What describes the capabilities of a directory role?\
    A. Role definition\
    B. Role assignment\
    C. User license\
    D. Device object

2.  What connects a principal to a role?\
    A. Role assignment\
    B. SKU\
    C. Group owner\
    D. AppId

3.  Should you assign powerful roles merely to practice?\
    A. No\
    B. Yes

------------------------------------------------------------------------

# Lab Complete

------------------------------------------------------------------------

# 🛠️ Project 03 — Microsoft Entra Security Inventory

You have completed the Microsoft Entra Administration section of the course.

Now apply the skills from Lessons 10–12 by completing Project 03.

➡️ **[Project 03 — Microsoft Entra Security Inventory](../projects/project-03-entra-security-inventory.md)**

In this project, you will combine your Microsoft Graph PowerShell skills to inventory Microsoft Entra devices, applications, service principals, and directory roles.

------------------------------------------------------------------------

**Continue to:**

[Lesson 13 --- Microsoft 365 and Microsoft
Graph](../lessons/lesson-13-microsoft-365-and-microsoft-graph.md)
