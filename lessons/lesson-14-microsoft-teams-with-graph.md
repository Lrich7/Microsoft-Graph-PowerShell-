# Lesson 14 --- Microsoft Teams with Graph

## Learning Objectives

By the end of this lesson, you will be able to:

-   Discover Microsoft Graph PowerShell commands for Teams.
-   Retrieve Teams and channels.
-   Understand Teams membership as an administrative relationship.
-   Build a read-only Teams inventory.
-   Recognize the relationship between Microsoft 365 groups and Teams.
-   Explain when the Microsoft Teams PowerShell module may also be
    relevant.
-   Avoid modifying Teams membership without understanding access
    impact.

------------------------------------------------------------------------

# Teams in Microsoft Graph

Microsoft Graph exposes many Microsoft Teams resources.

Examples include:

``` text
Teams
Channels
Members
Owners
Apps
Messages and other collaboration resources
```

Permissions vary by operation.

------------------------------------------------------------------------

# Discover Team Commands

Because the SDK is large, discovery is especially useful:

``` powershell
Get-Command '*MgTeam*'
```

Then inspect likely commands with:

``` powershell
Get-Help
Find-MgGraphCommand
```

------------------------------------------------------------------------

# Retrieve Teams

A common read command is:

``` powershell
Get-MgTeam
```

A team is associated with a Microsoft 365 group, and the team ID
corresponds to the backing group's ID.

This relationship is useful when building combined group/Teams reports.

------------------------------------------------------------------------

# Retrieve Channels

For a known team:

``` powershell
Get-MgTeamChannel -TeamId '<team-id>'
```

Select useful fields such as:

``` text
Id
DisplayName
Description
MembershipType
```

------------------------------------------------------------------------

# Team Members

Graph provides commands for Team membership.

Discover them:

``` powershell
Get-Command '*MgTeamMember*'
```

Then research the exact command and required permission.

Membership can affect access to collaborative information, so adding or
removing members is a real change.

------------------------------------------------------------------------

# Owners

Owners have additional management responsibilities.

When creating a report, distinguish:

``` text
Members
Owners
```

depending on the requirement.

------------------------------------------------------------------------

# Build a Teams Inventory

A useful inventory could contain:

``` text
Team ID
Team display name
Description
Channel count
Member count
Owner information
```

Some values may require separate Graph calls per team.

Be mindful of performance when querying many teams.

------------------------------------------------------------------------

# Graph vs. Microsoft Teams PowerShell

The Microsoft Teams PowerShell module remains useful for various Teams
administrative tasks.

Do not assume every Teams setting should be administered through Graph.

Choose the supported interface that best matches the task.

------------------------------------------------------------------------

# API Volume

A script that retrieves:

``` text
100 teams
then every channel
then every member
then every owner
```

can generate many Graph requests.

Later lessons will cover pagination and production considerations.

For now, start with small samples.

------------------------------------------------------------------------

# Common Beginner Mistakes

## Assuming a Team Is Unrelated to a Group

Teams use Microsoft 365 groups as part of their underlying membership
model.

## Running Membership Changes for Practice

Use read-only inventory first.

## Querying Every Relationship Immediately

Start small and understand the data model.

## Ignoring the Teams PowerShell Module

Graph is one administration option, not the only one.

------------------------------------------------------------------------

# Key Takeaways

-   Use Microsoft Graph PowerShell deliberately and verify your Graph
    context before administrative work.
-   Prefer read-only discovery and reporting before introducing changes.
-   Request only the permissions required for the task.
-   Inspect returned objects and properties rather than relying only on
    formatted screen output.
-   Validate targets before performing administrative changes.

------------------------------------------------------------------------

# Lab

Continue to:

[Lab 14 --- Microsoft Teams with
Graph](../labs/lesson-14-lab-14-microsoft-teams-with-graph.md)

------------------------------------------------------------------------

## Additional Resources

-   [Microsoft Graph Teams API
    overview](https://learn.microsoft.com/graph/teams-concept-overview)
-   [Microsoft Graph team
    resource](https://learn.microsoft.com/graph/api/resources/team)
-   [Microsoft Teams
    PowerShell](https://learn.microsoft.com/microsoftteams/teams-powershell-overview)
