# Lab 06 --- Working with Users

## Lab Objective

Build a read-only Microsoft Entra user report.

Use only a tenant you are authorized to query.

------------------------------------------------------------------------

# Exercise 1 --- Connect

If approved in your tenant:

``` powershell
Connect-MgGraph -Scopes 'User.Read.All'
```

Verify:

``` powershell
Get-MgContext
```

If consent is unavailable, do not bypass your organization's policy.

------------------------------------------------------------------------

# Exercise 2 --- Retrieve a Small Sample

Run:

``` powershell
Get-MgUser -Top 10
```

How many users were returned?

``` text
________________________________________
```

------------------------------------------------------------------------

# Exercise 3 --- Request Properties

Run:

``` powershell
Get-MgUser -Top 10 `
    -Property Id,DisplayName,UserPrincipalName,Department,AccountEnabled |
    Select-Object DisplayName,
                  UserPrincipalName,
                  Department,
                  AccountEnabled
```

Why was `Department` requested explicitly?

``` text
____________________________________________________
```

------------------------------------------------------------------------

# Exercise 4 --- Inspect a User Object

Run:

``` powershell
$user = Get-MgUser -Top 1 `
    -Property Id,DisplayName,UserPrincipalName,Department,AccountEnabled

$user | Get-Member
```

Find these properties:

``` text
Id
DisplayName
UserPrincipalName
Department
AccountEnabled
```

------------------------------------------------------------------------

# Exercise 5 --- Filter Enabled Users

Try:

``` powershell
Get-MgUser `
    -Filter "accountEnabled eq true" `
    -Top 10 `
    -Property DisplayName,UserPrincipalName,AccountEnabled |
    Select-Object DisplayName,UserPrincipalName,AccountEnabled
```

------------------------------------------------------------------------

# Exercise 6 --- Find Missing Departments

Retrieve an authorized sample or user collection and identify users with
a blank department.

``` powershell
# Your solution here
```

------------------------------------------------------------------------

# Exercise 7 --- Export a Report

Create a CSV containing:

``` text
DisplayName
UserPrincipalName
Department
AccountEnabled
```

Sort the report by display name.

``` powershell
# Your solution here
```

------------------------------------------------------------------------

# Offline Practice Option

If you cannot query a tenant:

``` powershell
$users = @(
    [pscustomobject]@{
        DisplayName='Alex Smith'
        UserPrincipalName='alex@example.com'
        Department='IT'
        AccountEnabled=$true
    }
    [pscustomobject]@{
        DisplayName='Jordan Lee'
        UserPrincipalName='jordan@example.com'
        Department=''
        AccountEnabled=$true
    }
    [pscustomobject]@{
        DisplayName='Former User'
        UserPrincipalName='former@example.com'
        Department='Operations'
        AccountEnabled=$false
    }
)
```

Practice:

``` text
Filtering
Sorting
Selecting
Exporting
```

------------------------------------------------------------------------

# Knowledge Check

1.  Which command retrieves Graph users?

    A. `Get-MgUser`\
    B. `Get-ADUser`\
    C. `Get-MgGroup`\
    D. `New-MgUser`

2.  What does `-All` do?

    A. Retrieves all result pages\
    B. Grants all permissions\
    C. Selects every tenant\
    D. Modifies all users

3.  Should a display name automatically be treated as a unique
    identifier?

    A. No\
    B. Yes

------------------------------------------------------------------------

# Lab Complete

Continue to:

[Lesson 07 --- Managing Users](../lessons/lesson-07-managing-users.md)
