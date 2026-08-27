# Lab 16 --- Advanced Queries and Pagination

## Lab Objective

Practice building efficient Microsoft Graph queries without making
tenant changes.

------------------------------------------------------------------------

# Exercise 1 --- Start Small

Run an authorized user query with:

``` powershell
Get-MgUser -Top 5
```

Then:

``` powershell
Get-MgUser -Top 20
```

Why is `-Top` useful while developing a script?

``` text
____________________________________________________
```

------------------------------------------------------------------------

# Exercise 2 --- Compare Filtering Methods

Try a supported server-side filter:

``` powershell
Get-MgUser `
    -Filter "accountEnabled eq true" `
    -Top 20 `
    -Property DisplayName,UserPrincipalName,AccountEnabled
```

Compare with:

``` powershell
Get-MgUser -Top 20 `
    -Property DisplayName,UserPrincipalName,AccountEnabled |
    Where-Object AccountEnabled -eq $true
```

Where does filtering occur in each example?

``` text
Graph filter:
________________________________________

PowerShell filter:
________________________________________
```

------------------------------------------------------------------------

# Exercise 3 --- Limit Properties

Retrieve a user sample containing only:

``` text
DisplayName
UserPrincipalName
Department
```

``` powershell
# Your solution
```

------------------------------------------------------------------------

# Exercise 4 --- Advanced Query Discovery

Use Microsoft documentation and command help to investigate:

``` powershell
-ConsistencyLevel
-CountVariable
```

Then create an advanced-query example appropriate for your authorized
environment.

``` powershell
# Your query
```

------------------------------------------------------------------------

# Exercise 5 --- Pagination

Explain what could happen if a script assumes the first Graph response
contains every object.

``` text
____________________________________________________
```

Then identify how Graph PowerShell commonly simplifies retrieving all
pages:

``` text
________________________________________
```

------------------------------------------------------------------------

# Exercise 6 --- Improve an Inefficient Design

Original idea:

``` text
Retrieve every user
For every user:
    Retrieve the same tenant SKU list
    Retrieve additional information
```

Write two ways you could reduce unnecessary requests:

``` text
1. ____________________________________

2. ____________________________________
```

------------------------------------------------------------------------

# Exercise 7 --- Build an Efficient Report

Create a read-only report that:

``` text
Retrieves enabled users
Requests only useful report properties
Sorts by display name
Exports to CSV
```

``` powershell
# Your solution
```

------------------------------------------------------------------------

# Knowledge Check

1.  What commonly tells Graph PowerShell to retrieve all result pages?

    A. `-All` B. `-Force` C. `-Everything` D. `-Complete`

2.  Why use `-Top` during development?

    A. To limit test results B. To grant permissions C. To modify
    objects D. To connect to Graph

3.  Is filtering at the Graph service often preferable when supported?

    A. Yes B. No

4.  Can excessive Graph requests lead to throttling?

    A. Yes B. No

------------------------------------------------------------------------

# Lab Complete

Continue to:

[Lesson 17 --- Error Handling and Reliable
Automation](../lessons/lesson-17-error-handling-and-reliable-automation.md)
