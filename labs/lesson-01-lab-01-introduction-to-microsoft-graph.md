# Lab 01 --- Introduction to Microsoft Graph

## Lab Objective

This first lab is mostly discovery and review.

You will:

-   Confirm your PowerShell environment.
-   Explore Graph-related command naming.
-   Review safe vs. change-oriented PowerShell verbs.
-   Connect Microsoft Graph concepts to your existing PowerShell
    knowledge.
-   Prepare for installing the SDK in Lesson 02.

You do **not** need to connect to a Microsoft 365 tenant in this lab.

------------------------------------------------------------------------

# Exercise 1 --- Check PowerShell

Run:

``` powershell
$PSVersionTable
```

Record:

``` text
PowerShell version:
________________________________________

Edition:
________________________________________
```

------------------------------------------------------------------------

# Exercise 2 --- Review PowerShell Verbs

Run:

``` powershell
Get-Verb |
    Sort-Object Verb
```

Find these verbs:

``` text
Get
New
Set
Remove
Update
```

Which of these would you generally expect to be safest for an
introductory read-only administration lab?

``` text
________________________________________
```

Why?

``` text
____________________________________________________
```

------------------------------------------------------------------------

# Exercise 3 --- Understand Graph Command Names

Graph PowerShell commands commonly use:

``` text
Verb-MgNoun
```

Classify these hypothetical or common command names by intent:

``` text
Get-MgUser
Get-MgGroup
New-MgGroup
Update-MgUser
Remove-MgGroup
```

  Command          Read or Change?
  ---------------- -----------------
  Get-MgUser       
  Get-MgGroup      
  New-MgGroup      
  Update-MgUser    
  Remove-MgGroup   

------------------------------------------------------------------------

# Exercise 4 --- PowerShell Skills That Transfer

For each command below, write what it does:

``` powershell
Select-Object
Where-Object
Sort-Object
Get-Member
Export-Csv
```

``` text
Select-Object:
____________________________________________________

Where-Object:
____________________________________________________

Sort-Object:
____________________________________________________

Get-Member:
____________________________________________________

Export-Csv:
____________________________________________________
```

These same tools will be used with Graph objects later.

------------------------------------------------------------------------

# Exercise 5 --- Design a Read-Only Graph Task

Choose one Microsoft cloud resource:

``` text
Users
Groups
Devices
Applications
Teams
SharePoint
OneDrive
```

Resource:

``` text
________________________________________
```

Write one useful read-only IT question:

``` text
____________________________________________________
```

Example:

``` text
Which user accounts are currently enabled?
```

What output might be useful?

``` text
____________________________________________________
```

------------------------------------------------------------------------

# Exercise 6 --- Authentication vs. Authorization

Fill in:

``` text
Authentication asks:
____________________________________________________

Authorization asks:
____________________________________________________
```

Why does a cloud administration tool need both?

``` text
____________________________________________________
____________________________________________________
```

------------------------------------------------------------------------

# Exercise 7 --- Least Privilege

Scenario:

> You need to generate a user report. You do not need to modify users.

Which general permission type sounds safer?

``` text
Read
ReadWrite
```

Answer:

``` text
________________________________________
```

Explain:

``` text
____________________________________________________
```

------------------------------------------------------------------------

# Knowledge Check

1.  What does Microsoft Graph provide?

    A. Only local Windows administration B. Access to many Microsoft
    cloud resources and services C. A replacement for PowerShell
    itself D. Only Exchange mailboxes

2.  What does `Mg` commonly identify in a PowerShell command?

    A. Microsoft Graph B. Management Group only C. Microsoft Git D.
    Module Generator

3.  Which verb normally indicates retrieval?

    A. Remove B. New C. Get D. Update

4.  Which principle says you should request only the access needed?

    A. Least privilege B. Maximum consent C. Full control D. Inheritance

------------------------------------------------------------------------

# Lab Complete

Continue to:

[Lesson 02 --- Installing the Microsoft Graph PowerShell
SDK](../lessons/lesson-02-installing-the-graph-sdk.md)
