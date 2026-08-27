# Lab 13 --- Microsoft 365 and Microsoft Graph

## Lab Objective

Practice choosing the appropriate Microsoft 365 administration tool.
This lab is primarily planning and command research, so no tenant
changes are required.

------------------------------------------------------------------------

# Exercise 1 --- Classify the Requirement

For each task, decide whether you would research Microsoft Graph, a
workload-specific PowerShell module, or both.

  Requirement                             Graph / Workload Module / Both
  --------------------------------------- --------------------------------
  Report Entra users                      
  Review group membership                 
  Configure an Exchange mailbox setting   
  Inventory Teams                         
  Inventory SharePoint sites              
  Build a cross-service user report       

There may be more than one valid research path. Explain your reasoning.

------------------------------------------------------------------------

# Exercise 2 --- Research a Graph Resource

Choose one:

``` text
Teams
SharePoint
OneDrive
Mail
Calendar
```

Use Microsoft Graph PowerShell command discovery to find related
commands.

``` powershell
Get-Command '*Mg*' | Where-Object Name -like '*YourResource*'
```

Use more targeted module/command discovery if the broad search returns
too much.

Record three relevant commands:

``` text
1. ____________________________________

2. ____________________________________

3. ____________________________________
```

------------------------------------------------------------------------

# Exercise 3 --- Dependency Planning

Imagine a script that:

``` text
Retrieves Entra users
Checks Exchange mailbox information
Checks Teams membership
Exports one report
```

List likely module/tool dependencies:

``` text
1. ____________________________________

2. ____________________________________

3. ____________________________________
```

------------------------------------------------------------------------

# Exercise 4 --- Authentication Planning

Why should a multi-module script not assume that connecting to Graph
automatically authenticates every other Microsoft 365 PowerShell module?

``` text
____________________________________________________
```

------------------------------------------------------------------------

# Exercise 5 --- Design a Tool-Selection Checklist

Create five questions you would ask before choosing Graph or a
workload-specific module.

``` text
1. ____________________________________
2. ____________________________________
3. ____________________________________
4. ____________________________________
5. ____________________________________
```

------------------------------------------------------------------------

# Knowledge Check

1.  Does Microsoft Graph PowerShell replace every Microsoft 365
    administrative module?\
    A. No\
    B. Yes

2.  Can one automation workflow use more than one PowerShell module?\
    A. Yes\
    B. No

3.  What should determine tool choice?\
    A. The supported requirements of the task\
    B. Whichever cmdlet name is shortest

------------------------------------------------------------------------

# Lab Complete

Continue to:

[Lesson 14 --- Microsoft Teams with
Graph](../lessons/lesson-14-microsoft-teams-with-graph.md)
