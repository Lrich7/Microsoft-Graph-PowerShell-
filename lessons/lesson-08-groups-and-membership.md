# Lesson 08 --- Groups and Membership

## Learning Objectives

By the end of this lesson, you will be able to:

-   Retrieve Microsoft Entra groups.
-   Inspect group properties and types.
-   Retrieve direct group members.
-   Explain direct vs. transitive membership.
-   Understand that group members can be different directory object
    types.
-   Distinguish group owners from members.
-   Build a read-only group inventory.
-   Explain the risks of membership changes.

------------------------------------------------------------------------

# Retrieve Groups

Use:

``` powershell
Get-MgGroup
```

For all result pages:

``` powershell
Get-MgGroup -All
```

Select useful information:

``` powershell
Get-MgGroup -All |
    Select-Object Id,
                  DisplayName,
                  Mail,
                  MailEnabled,
                  SecurityEnabled,
                  GroupTypes
```

------------------------------------------------------------------------

# Retrieve a Specific Group

Once you know the object ID:

``` powershell
Get-MgGroup -GroupId '<group-id>'
```

Store it:

``` powershell
$group = Get-MgGroup -GroupId '<group-id>'
```

Object IDs are particularly important when preparing administrative
changes.

------------------------------------------------------------------------

# Group Types

Microsoft Entra can contain different kinds of groups.

Useful properties include:

``` text
MailEnabled
SecurityEnabled
GroupTypes
```

Do not assume every group serves the same purpose.

A group might be related to:

``` text
Security
Microsoft 365 collaboration
Teams
Licensing
Application access
Resource access
```

------------------------------------------------------------------------

# Retrieve Group Members

Use:

``` powershell
Get-MgGroupMember -GroupId '<group-id>' -All
```

This retrieves direct members.

Inspect a member object:

``` powershell
Get-MgGroupMember -GroupId '<group-id>' -Top 1 |
    Get-Member
```

------------------------------------------------------------------------

# Members Are Directory Objects

Do not automatically assume every member returned is a user.

Depending on the group and directory structure, membership can involve
different directory object types.

Your script should understand what it is receiving.

------------------------------------------------------------------------

# Direct vs. Transitive Membership

Direct membership means the object is immediately a member of the group.

Transitive membership considers nested relationships.

Conceptually:

``` text
Group A
   ↓
Group B
   ↓
User
```

The user may not be a direct member of Group A but may appear in a
transitive membership relationship.

Choose the query that matches the actual requirement.

------------------------------------------------------------------------

# Owners vs. Members

Group ownership and group membership are different concepts.

A report may need:

``` text
Members
Owners
Both
```

Clarify the requirement before building the script.

------------------------------------------------------------------------

# Membership Changes

Adding or removing a member can change access to organizational
resources.

Before changing membership:

``` text
Verify tenant
Verify group
Verify member
Understand what access the group controls
Confirm authorization
Perform change
Verify result
```

------------------------------------------------------------------------

# Group Inventory

A useful read-only inventory:

``` powershell
Get-MgGroup -All |
    Select-Object Id,
                  DisplayName,
                  Mail,
                  MailEnabled,
                  SecurityEnabled,
                  GroupTypes |
    Sort-Object DisplayName
```

Export when appropriate:

``` powershell
... |
    Export-Csv .\groups.csv -NoTypeInformation
```

------------------------------------------------------------------------

# Common Beginner Mistakes

## Assuming Every Group Is the Same Type

Inspect the group's properties.

## Assuming Every Member Is a User

Membership results can represent directory objects.

## Confusing Owners and Members

They answer different administrative questions.

## Changing Membership Without Understanding the Group

A group may control access, licensing, Teams, applications, or other
resources.

## Using a Name Instead of Resolving the Exact Group

Use a reliable identifier before changes.

------------------------------------------------------------------------

# Key Takeaways

-   `Get-MgGroup` retrieves groups.
-   `Get-MgGroupMember` retrieves direct group membership.
-   Group properties help identify the group's purpose/type.
-   Direct and transitive membership answer different questions.
-   Owners and members are different.
-   Membership changes can affect access.
-   Resolve the exact group and member before making changes.
-   Start with read-only inventory work.

------------------------------------------------------------------------

# Lab

Continue to:

[Lab 08 --- Groups and
Membership](../labs/lesson-08-lab-08-groups-and-membership.md)

------------------------------------------------------------------------

## Additional Resources

-   [Get-MgGroup](https://learn.microsoft.com/powershell/module/microsoft.graph.groups/get-mggroup)
-   [Get-MgGroupMember](https://learn.microsoft.com/powershell/module/microsoft.graph.groups/get-mggroupmember)
-   [Microsoft Graph group
    resource](https://learn.microsoft.com/graph/api/resources/group)
