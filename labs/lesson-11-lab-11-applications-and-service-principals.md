# Lab 11 --- Applications and Service Principals

## Lab Objective

Build a read-only inventory of application registrations and service
principals.

------------------------------------------------------------------------

# Exercise 1 --- Discover Commands

``` powershell
Get-Command Get-MgApplication
Get-Command Get-MgServicePrincipal

Find-MgGraphCommand -Command Get-MgApplication
Find-MgGraphCommand -Command Get-MgServicePrincipal
```

Research the least-privileged read permissions appropriate for your
authorized environment.

------------------------------------------------------------------------

# Exercise 2 --- Retrieve Applications

``` powershell
Get-MgApplication -Top 10 |
    Select-Object Id,AppId,DisplayName
```

Record:

``` text
Id represents: ______________________________

AppId represents: ___________________________
```

------------------------------------------------------------------------

# Exercise 3 --- Retrieve Service Principals

``` powershell
Get-MgServicePrincipal -Top 10 |
    Select-Object Id,AppId,DisplayName,ServicePrincipalType
```

------------------------------------------------------------------------

# Exercise 4 --- Match by AppId

Choose an authorized application object.

Store its `AppId`.

Use a supported Graph query or PowerShell filtering to find
service-principal records with the same `AppId`.

``` powershell
# Your solution
```

------------------------------------------------------------------------

# Exercise 5 --- Credential Metadata

Inspect an authorized application object with:

``` powershell
$app | Get-Member
```

Locate credential-related properties.

Do **not** export secrets.

Write down the type of metadata that could be useful for an expiration
report:

``` text
____________________________________________________
```

------------------------------------------------------------------------

# Exercise 6 --- Export an Application Inventory

Create a CSV containing:

``` text
DisplayName
AppId
Id
```

Add other non-secret properties you think are useful.

------------------------------------------------------------------------

# Knowledge Check

1.  Which value is commonly called the client/application ID?\
    A. `AppId`\
    B. `Id` only\
    C. `DisplayName`\
    D. `TenantId`

2.  Is an application object the same thing as a service principal?\
    A. No\
    B. Yes

3.  Should client secrets be committed to Git?\
    A. No\
    B. Yes

------------------------------------------------------------------------

# Lab Complete

Continue to:

[Lesson 12 --- Directory Roles](../lessons/lesson-12-directory-roles.md)
