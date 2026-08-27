# Lab 02 --- Installing the Microsoft Graph PowerShell SDK

## Lab Objective

In this lab, you will inspect your PowerShell environment and prepare or
verify a Microsoft Graph PowerShell SDK installation.

On managed company equipment, follow organizational policy before
installing modules.

------------------------------------------------------------------------

# Exercise 1 --- Verify PowerShell Version

Run:

``` powershell
$PSVersionTable.PSVersion
```

Record:

``` text
Version:
________________________________________
```

Are you using PowerShell 7 or later?

``` text
Yes / No
```

------------------------------------------------------------------------

# Exercise 2 --- Check Existing Graph Modules

Run:

``` powershell
Get-Module Microsoft.Graph* -ListAvailable |
    Sort-Object Name |
    Select-Object Name, Version, Path
```

Were Graph modules already available?

``` text
Yes / No
```

If yes, record one:

``` text
________________________________________
```

------------------------------------------------------------------------

# Exercise 3 --- Search the PowerShell Gallery

If `Find-Module` is available:

``` powershell
Find-Module Microsoft.Graph
```

Then:

``` powershell
Find-Module Microsoft.Graph.Authentication
```

Record the repository:

``` text
________________________________________
```

------------------------------------------------------------------------

# Exercise 4 --- Install or Review

If the SDK is not installed **and you are authorized to install it**,
use:

``` powershell
Install-Module Microsoft.Graph `
    -Scope CurrentUser `
    -Repository PSGallery
```

If prompted about repository trust, read the prompt before responding.

If you are **not** authorized to install software/modules on this
computer, do not bypass that restriction. Continue with the review
exercises.

------------------------------------------------------------------------

# Exercise 5 --- Verify Installation

If installed:

``` powershell
Get-InstalledModule Microsoft.Graph
```

Then:

``` powershell
Get-Module Microsoft.Graph* -ListAvailable |
    Sort-Object Name |
    Select-Object Name, Version
```

Record the main SDK version:

``` text
________________________________________
```

------------------------------------------------------------------------

# Exercise 6 --- Find Authentication Commands

Run:

``` powershell
Get-Command Connect-MgGraph -ErrorAction SilentlyContinue
Get-Command Get-MgContext -ErrorAction SilentlyContinue
Get-Command Disconnect-MgGraph -ErrorAction SilentlyContinue
```

Were all three found?

``` text
Yes / No
```

------------------------------------------------------------------------

# Exercise 7 --- Inspect the Authentication Module

Run:

``` powershell
Get-Command -Module Microsoft.Graph.Authentication |
    Sort-Object Name
```

Choose three commands that look useful:

``` text
1. ____________________________________
2. ____________________________________
3. ____________________________________
```

------------------------------------------------------------------------

# Exercise 8 --- Main SDK vs. Beta

Check:

``` powershell
Get-Module Microsoft.Graph.Beta* -ListAvailable
```

Is beta installed?

``` text
Yes / No
```

Do you need beta to continue this course?

``` text
Yes / No
```

Why is v1.0 normally preferred for production-oriented scripts?

``` text
____________________________________________________
```

------------------------------------------------------------------------

# Exercise 9 --- Module Location

Inspect:

``` powershell
Get-Module Microsoft.Graph.Authentication -ListAvailable |
    Select-Object Name, Version, Path
```

Record the path:

``` text
____________________________________________________
```

This helps reinforce that modules are files PowerShell locates and
loads.

------------------------------------------------------------------------

# Knowledge Check

1.  Which PowerShell version does Microsoft recommend for Graph
    PowerShell?

    A. PowerShell 2 B. PowerShell 7 or later C. CMD D. VBScript

2.  Which module contains `Connect-MgGraph`?

    A. Microsoft.Graph.Authentication B. ActiveDirectory C.
    ExchangeOnlineManagement D. Microsoft.Graph.Beta.Users only

3.  What does `-Scope CurrentUser` generally do?

    A. Installs for the current user B. Grants Graph permissions C.
    Connects to a tenant D. Creates an Entra user

4.  Which API/module family should normally be preferred when stable
    functionality meets the requirement?

    A. Beta B. v1.0 / Microsoft.Graph C. Preview only D. AzureADPreview

------------------------------------------------------------------------

# Lab Complete

Continue to:

[Lesson 03 --- Connecting to Microsoft
Graph](../lessons/lesson-03-connecting-to-microsoft-graph.md)
