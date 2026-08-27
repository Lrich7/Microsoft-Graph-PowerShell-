# Lab 04 --- Microsoft Graph Permissions and Scopes

## Lab Objective

In this lab, you will examine Graph permissions from a least-privilege
perspective.

The lab is designed to remain low risk. Do not request broad write
permissions merely for practice.

------------------------------------------------------------------------

# Exercise 1 --- Connect with User.Read

If you are not already connected:

``` powershell
Connect-MgGraph -Scopes 'User.Read'
```

Then:

``` powershell
Get-MgContext
```

------------------------------------------------------------------------

# Exercise 2 --- Inspect Current Scopes

Run:

``` powershell
(Get-MgContext).Scopes |
    Sort-Object
```

Record the Graph permission you intentionally requested:

``` text
________________________________________
```

------------------------------------------------------------------------

# Exercise 3 --- Decode Permission Names

For each permission, identify:

``` text
Resource
Access level
Scope breadth
```

### User.Read

``` text
Resource:
________________________________________

Access:
________________________________________
```

### User.Read.All

``` text
Resource:
________________________________________

Access:
________________________________________
```

### User.ReadWrite.All

``` text
Resource:
________________________________________

Access:
________________________________________
```

### Group.Read.All

``` text
Resource:
________________________________________

Access:
________________________________________
```

------------------------------------------------------------------------

# Exercise 4 --- Choose Least Privilege

Choose the better starting permission concept for each scenario.

## Scenario A

> Display information about the signed-in user's own profile.

``` text
User.Read
User.ReadWrite.All
```

Answer:

``` text
________________________________________
```

## Scenario B

> Build a read-only report of users across the organization.

``` text
User.Read.All
User.ReadWrite.All
```

Answer:

``` text
________________________________________
```

## Scenario C

> Build a read-only report of groups.

``` text
Group.Read.All
Group.ReadWrite.All
```

Answer:

``` text
________________________________________
```

Explain the pattern:

``` text
____________________________________________________
```

------------------------------------------------------------------------

# Exercise 5 --- Permission vs. Role

Answer:

``` text
Does being authenticated automatically authorize every Graph operation?
Yes / No
```

``` text
Does requesting a Graph permission automatically guarantee every required administrative authority?
Yes / No
```

Explain:

``` text
____________________________________________________
____________________________________________________
```

------------------------------------------------------------------------

# Exercise 6 --- Consent Review

Consider:

> You request a permission and the tenant says administrator approval is
> required.

What should you do?

``` text
A. Find a way around the policy
B. Request a broader permission
C. Follow the organization's approval/consent process
D. Use another employee's account
```

Answer:

``` text
________________________________________
```

------------------------------------------------------------------------

# Exercise 7 --- Permission Planning

Scenario:

> IT wants a report containing user display names and user principal
> names. No changes are required.

Fill out:

``` text
Resource:
________________________________________

Read or write?
________________________________________

Likely permission family:
________________________________________

Why not request ReadWrite by default?
____________________________________________________
```

------------------------------------------------------------------------

# Exercise 8 --- Inspect Before Disconnecting

Run:

``` powershell
$context = Get-MgContext

$context |
    Select-Object Account, TenantId, AuthType, Scopes
```

Before ending the session, verify:

``` text
[ ] Correct account
[ ] Correct tenant
[ ] Expected authentication type
[ ] Expected scope
```

Then:

``` powershell
Disconnect-MgGraph
```

------------------------------------------------------------------------

# Exercise 9 --- Build a Permission Checklist

Complete this checklist in your own words:

``` text
Before requesting a Graph permission, I should know:

1. ____________________________________
2. ____________________________________
3. ____________________________________
4. ____________________________________
5. ____________________________________
```

------------------------------------------------------------------------

# Knowledge Check

1.  Delegated permissions are commonly called:

    A. Scopes B. Drives C. Modules D. Pipelines

2.  Application permissions are primarily associated with:

    A. App-only access B. Local file access C. PowerShell aliases D. CSV
    files

3.  For a read-only report, which is generally the better starting
    point?

    A. Read permission B. ReadWrite permission C. Full control D. Every
    available permission

4.  What principle should guide permission selection?

    A. Least privilege B. Maximum access C. Convenience first D.
    Permanent consent

5.  What should you do if admin consent is required?

    A. Follow the approved consent process B. Bypass it C. Share
    credentials D. Disable tenant security

------------------------------------------------------------------------

# Lab Complete

You have completed Lessons 01--04.

Continue to the next lesson when it is added:

``` text
Lesson 05 — Finding Microsoft Graph Commands
```
