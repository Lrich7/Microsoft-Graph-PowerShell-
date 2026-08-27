# Lesson 06 --- Working with Users

## Learning Objectives

By the end of this lesson, you will be able to:

-   Retrieve Microsoft Entra users with `Get-MgUser`.
-   Retrieve a specific user.
-   Request additional user properties.
-   Understand `-Top`, `-All`, and `-Filter`.
-   Process Graph user objects with normal PowerShell commands.
-   Build a read-only user inventory.
-   Export Graph user data to CSV.

------------------------------------------------------------------------

# Working with User Objects

Users are one of the most common resources you will work with through
Microsoft Graph.

The primary read command is:

``` powershell
Get-MgUser
```

------------------------------------------------------------------------

# Connect for User Reporting

An organization-wide user report requires an appropriate Graph read
permission.

For example:

``` powershell
Connect-MgGraph -Scopes 'User.Read.All'
```

Your organization's consent policies determine whether that permission
can be granted.

Verify the session:

``` powershell
Get-MgContext
```

------------------------------------------------------------------------

# Retrieve Users

Retrieve users:

``` powershell
Get-MgUser
```

Retrieve a small sample:

``` powershell
Get-MgUser -Top 10
```

Retrieve all pages:

``` powershell
Get-MgUser -All
```

Use `-All` only when you actually need the complete directory.

------------------------------------------------------------------------

# Retrieve a Specific User

Use a supported user identifier such as the object ID or user principal
name:

``` powershell
Get-MgUser -UserId 'alex@contoso.com'
```

Store the result:

``` powershell
$user = Get-MgUser -UserId 'alex@contoso.com'
```

Then inspect the object:

``` powershell
$user | Get-Member
```

------------------------------------------------------------------------

# User Properties

Graph does not necessarily return every available property by default.

Request the properties you need:

``` powershell
Get-MgUser -Top 10 `
    -Property Id,DisplayName,UserPrincipalName,Department,AccountEnabled
```

Then select readable output:

``` powershell
Get-MgUser -Top 10 `
    -Property Id,DisplayName,UserPrincipalName,Department,AccountEnabled |
    Select-Object DisplayName,
                  UserPrincipalName,
                  Department,
                  AccountEnabled
```

------------------------------------------------------------------------

# Server-Side Filtering

When supported, Graph can filter before returning the data.

Example:

``` powershell
Get-MgUser `
    -Filter "accountEnabled eq true" `
    -Top 10 `
    -Property DisplayName,UserPrincipalName,AccountEnabled
```

This can be more efficient than retrieving a large directory and
filtering everything locally.

------------------------------------------------------------------------

# PowerShell Filtering

You can also use:

``` powershell
Get-MgUser -All |
    Where-Object AccountEnabled -eq $true
```

This retrieves data and then filters it in PowerShell.

Both techniques are useful, but they operate at different stages.

------------------------------------------------------------------------

# Sorting and Selecting

Normal PowerShell works with Graph objects:

``` powershell
Get-MgUser -All |
    Sort-Object DisplayName |
    Select-Object DisplayName, UserPrincipalName
```

------------------------------------------------------------------------

# Find Missing Data

Directory data is rarely perfect.

You may encounter users with:

``` text
No department
No job title
No mail value
Unexpected account state
```

Example:

``` powershell
$users |
    Where-Object { [string]::IsNullOrWhiteSpace($_.Department) }
```

This can help IT identify incomplete directory information.

------------------------------------------------------------------------

# Export a User Report

Example:

``` powershell
$users = Get-MgUser -All `
    -Property DisplayName,UserPrincipalName,Department,AccountEnabled

$users |
    Select-Object DisplayName,
                  UserPrincipalName,
                  Department,
                  AccountEnabled |
    Sort-Object DisplayName |
    Export-Csv .\users.csv -NoTypeInformation
```

------------------------------------------------------------------------

# Use Reliable Identifiers

Display names are useful for humans but should not automatically be
treated as unique.

Before targeting a user for administrative work, prefer identifiers such
as:

``` text
Object ID
User principal name
```

depending on the command and scenario.

------------------------------------------------------------------------

# Read Before Write

Before learning user modifications, make sure you can:

``` text
Find the correct user
Verify the tenant
Retrieve the correct properties
Filter safely
Create a trustworthy report
```

------------------------------------------------------------------------

# Common Beginner Mistakes

## Assuming Every Property Is Returned

Request the properties required by your report.

## Using Display Name as a Unique Identifier

Two users can potentially have the same display name.

## Using -All for Every Query

Retrieve only what you need.

## Forgetting the Tenant

Always verify your Graph context before working with organizational
data.

------------------------------------------------------------------------

# Key Takeaways

-   `Get-MgUser` retrieves Microsoft Entra user objects.
-   `-Top` limits results.
-   `-All` retrieves all pages.
-   Request additional properties when needed.
-   Graph supports server-side filtering for supported queries.
-   Standard PowerShell tools work with Graph objects.
-   Prefer reliable identifiers when targeting users.
-   Begin with read-only reporting.

------------------------------------------------------------------------

# Lab

Continue to:

[Lab 06 --- Working with
Users](../labs/lesson-06-lab-06-working-with-users.md)

------------------------------------------------------------------------

## Additional Resources

-   [Get-MgUser](https://learn.microsoft.com/powershell/module/microsoft.graph.users/get-mguser)
-   [Microsoft Graph user
    resource](https://learn.microsoft.com/graph/api/resources/user)
