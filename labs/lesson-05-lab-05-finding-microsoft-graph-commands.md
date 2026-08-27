# Lab 05 --- Finding Microsoft Graph Commands

## Lab Objective

Practice discovering Graph commands and permissions without making
tenant changes.

------------------------------------------------------------------------

# Exercise 1 --- Find User Commands

Run:

``` powershell
Get-Command -Name '*MgUser*' |
    Sort-Object Name
```

Find one command using each verb:

``` text
Get: ___________________________________

New: ___________________________________

Update: ________________________________
```

------------------------------------------------------------------------

# Exercise 2 --- Read Help

Run:

``` powershell
Get-Help Get-MgUser -Examples
```

Then:

``` powershell
Get-Help Get-MgUser -Parameter UserId
```

What does `UserId` identify?

``` text
____________________________________________________
```

------------------------------------------------------------------------

# Exercise 3 --- Find the Graph Operation

Run:

``` powershell
Find-MgGraphCommand -Command Get-MgUser
```

Record:

``` text
Module:
________________________________________

HTTP method:
________________________________________
```

------------------------------------------------------------------------

# Exercise 4 --- Compare Read and Write Operations

Compare:

``` powershell
Find-MgGraphCommand -Command Get-MgUser
```

and:

``` powershell
Find-MgGraphCommand -Command Update-MgUser
```

What difference do you notice?

``` text
____________________________________________________
```

------------------------------------------------------------------------

# Exercise 5 --- Permission Discovery

Run:

``` powershell
Find-MgGraphPermission 'User.Read'
```

Find one delegated read permission related to users.

``` text
________________________________________
```

------------------------------------------------------------------------

# Exercise 6 --- Build Your Own Discovery Workflow

Your task is:

> Find a Graph PowerShell command that retrieves groups and determine
> what permission it requires.

Write the commands you would use:

``` powershell
# Your commands here
```

------------------------------------------------------------------------

# Knowledge Check

1.  Which cmdlet helps connect Graph PowerShell commands with Graph API
    operations?

    A. `Find-MgGraphCommand`\
    B. `Get-Service`\
    C. `Export-Csv`\
    D. `Set-Location`

2.  Which cmdlet helps research Graph permissions?

    A. `Find-MgGraphPermission`\
    B. `Get-Verb`\
    C. `Get-Process`\
    D. `Measure-Object`

3.  Which HTTP method normally retrieves information?

    A. GET\
    B. DELETE\
    C. PATCH\
    D. POST

------------------------------------------------------------------------

# Lab Complete

Continue to:

[Lesson 06 --- Working with
Users](../lessons/lesson-06-working-with-users.md)
