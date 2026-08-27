# Lab 08 --- Groups and Membership

## Lab Objective

Inventory Microsoft Entra groups and inspect direct membership without
changing it.

------------------------------------------------------------------------

# Exercise 1 --- Discover Commands and Permissions

Run:

``` powershell
Find-MgGraphCommand -Command Get-MgGroup
Find-MgGraphCommand -Command Get-MgGroupMember
```

Determine an appropriate read-only delegated permission for your
authorized environment.

------------------------------------------------------------------------

# Exercise 2 --- Retrieve Groups

After connecting with an approved read permission:

``` powershell
Get-MgGroup -Top 20 |
    Select-Object Id,
                  DisplayName,
                  Mail,
                  MailEnabled,
                  SecurityEnabled,
                  GroupTypes
```

------------------------------------------------------------------------

# Exercise 3 --- Select a Group

Choose a group you are authorized to inspect.

Store it in:

``` powershell
$group
```

Record:

``` text
Group name:
________________________________________

Group ID:
________________________________________
```

------------------------------------------------------------------------

# Exercise 4 --- Retrieve Direct Members

Run:

``` powershell
Get-MgGroupMember -GroupId $group.Id -Top 20
```

Then inspect one result:

``` powershell
Get-MgGroupMember -GroupId $group.Id -Top 1 |
    Get-Member
```

Why should you not assume every member is a user?

``` text
____________________________________________________
```

------------------------------------------------------------------------

# Exercise 5 --- Build a Group Inventory

Create a report containing:

``` text
Id
DisplayName
Mail
MailEnabled
SecurityEnabled
GroupTypes
```

Sort by display name.

``` powershell
# Your solution here
```

Export it to CSV.

------------------------------------------------------------------------

# Exercise 6 --- Membership Change Checklist

Without running a write command, complete the checklist:

``` text
[ ] Correct tenant
[ ] Correct group
[ ] Correct target member
[ ] ____________________________________
[ ] ____________________________________
[ ] ____________________________________
```

------------------------------------------------------------------------

# Knowledge Check

1.  Which cmdlet retrieves groups?

    A. `Get-MgGroup`\
    B. `Get-MgUser`\
    C. `Get-GroupLocal`\
    D. `Find-Group`

2.  Does `Get-MgGroupMember` retrieve direct members?

    A. Yes\
    B. No

3.  Are group owners and members always the same thing?

    A. No\
    B. Yes

------------------------------------------------------------------------

# Lab Complete

Continue to:

[Lesson 09 --- Microsoft 365 Licenses with Microsoft
Graph](../lessons/lesson-09-licenses.md)
