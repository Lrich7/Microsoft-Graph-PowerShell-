# Lesson 16 --- Advanced Queries and Pagination

## Learning Objectives

By the end of this lesson, you will be able to:

-   Explain why Microsoft Graph returns paged results.
-   Use `-All` appropriately with Graph PowerShell cmdlets.
-   Use `-Top` to limit results during testing.
-   Understand server-side filtering and sorting.
-   Recognize when advanced queries require additional query settings.
-   Use `-ConsistencyLevel eventual` and count variables when required.
-   Design Graph queries that retrieve only the data you need.
-   Recognize throttling and inefficient query patterns.

------------------------------------------------------------------------

# Why Advanced Queries Matter

Small test environments can make Graph queries look simple.

Production environments may contain:

``` text
Thousands of users
Thousands of devices
Hundreds of groups
Large SharePoint libraries
Many applications
Large Teams environments
```

A production script should not retrieve everything unless everything is
actually required.

A better pattern is:

``` text
Define requirement
      ↓
Limit properties
      ↓
Filter at Graph when possible
      ↓
Handle pagination
      ↓
Process results
```

------------------------------------------------------------------------

# Pagination

Microsoft Graph frequently returns data in pages.

If more results exist, the API can provide a link to the next page.

The Microsoft Graph PowerShell SDK handles much of this complexity for
you.

For many cmdlets:

``` powershell
Get-MgUser -All
```

retrieves all pages.

Without `-All`, you may receive only the first page or the requested
result limit.

------------------------------------------------------------------------

# Use -Top During Development

When testing a command, start small:

``` powershell
Get-MgUser -Top 10
```

This is safer and faster than immediately retrieving an entire
directory.

A useful development progression is:

``` text
1 object
10 objects
Filtered sample
Full required dataset
```

------------------------------------------------------------------------

# Server-Side Filtering

Graph can filter many resources before returning them.

Example:

``` powershell
Get-MgUser `
    -Filter "accountEnabled eq true" `
    -All
```

Compare this with:

``` powershell
Get-MgUser -All |
    Where-Object AccountEnabled -eq $true
```

The second approach retrieves the data first and filters locally.

When Graph supports the filter you need, server-side filtering can
reduce unnecessary data transfer.

------------------------------------------------------------------------

# Request Only Needed Properties

Do not request every available property if your report needs only a few.

Example:

``` powershell
Get-MgUser -All `
    -Property DisplayName,UserPrincipalName,Department
```

Then:

``` powershell
Select-Object DisplayName,
              UserPrincipalName,
              Department
```

------------------------------------------------------------------------

# Advanced Queries

Some directory-object queries support advanced query capabilities.

Depending on the operation, advanced queries can require:

``` powershell
-ConsistencyLevel eventual
```

and sometimes a count query.

Example pattern:

``` powershell
$count = 0

Get-MgUser `
    -ConsistencyLevel eventual `
    -CountVariable count `
    -Filter "startsWith(DisplayName,'A')" `
    -All
```

Not every filter requires advanced-query settings.

Always check the documentation for the resource and query you are using.

------------------------------------------------------------------------

# CountVariable

Some Graph PowerShell commands support:

``` powershell
-CountVariable
```

Example:

``` powershell
$count = 0

$users = Get-MgUser `
    -ConsistencyLevel eventual `
    -CountVariable count `
    -All

$count
```

The exact behavior depends on the Graph operation.

------------------------------------------------------------------------

# Sorting

Some Graph operations support server-side ordering.

You may also sort locally:

``` powershell
$users |
    Sort-Object DisplayName
```

Choose the approach that fits the operation and dataset.

------------------------------------------------------------------------

# Query Efficiency

Compare:

``` powershell
Get-MgUser -All
```

with a requirement that only needs enabled IT users.

A better query might narrow the data at the source when supported.

The goal is:

``` text
Retrieve what you need
Not everything you can access
```

------------------------------------------------------------------------

# Throttling

Microsoft Graph protects services from excessive request volume.

A script can encounter throttling if it makes too many requests too
quickly.

Common causes include:

``` text
Large loops
One API call per object
Repeatedly retrieving the same data
Unnecessary full-directory queries
Recursive file inventories
```

Production scripts should be designed to minimize unnecessary calls and
handle transient failures appropriately.

------------------------------------------------------------------------

# Avoid the N+1 Pattern

Imagine retrieving 1,000 users and then making another Graph request for
every user.

That can become:

``` text
1 request
+
1,000 additional requests
```

Before doing this, ask whether the required information can be:

``` text
Retrieved in the original query
Retrieved in batches
Cached
Joined from another single inventory query
```

------------------------------------------------------------------------

# Common Beginner Mistakes

## Using -All Automatically

Use it when the requirement truly needs all results.

## Filtering Everything Locally

Prefer server-side filtering when Graph supports the requirement.

## Ignoring Pagination

A successful command does not always mean you retrieved every result.

## Requesting Too Many Properties

Retrieve only what your report needs.

## Making a Graph Call Inside Every Loop

This can create slow and heavily throttled scripts.

------------------------------------------------------------------------

# Key Takeaways

-   Microsoft Graph frequently uses pagination.
-   `-All` can retrieve all pages for supported Graph PowerShell
    cmdlets.
-   `-Top` is useful while developing and testing.
-   Filter at Graph when supported.
-   Advanced directory queries may require `ConsistencyLevel eventual`.
-   Retrieve only the properties and objects required.
-   Avoid unnecessary repeated Graph calls.
-   Efficient query design matters in production.

------------------------------------------------------------------------

# Lab

Continue to:

[Lab 16 --- Advanced Queries and
Pagination](../labs/lesson-16-lab-16-advanced-queries-and-pagination.md)

------------------------------------------------------------------------

## Additional Resources

-   [Microsoft Graph paging](https://learn.microsoft.com/graph/paging)
-   [Microsoft Graph advanced query
    capabilities](https://learn.microsoft.com/graph/aad-advanced-queries)
-   [Microsoft Graph throttling
    guidance](https://learn.microsoft.com/graph/throttling)
