# Lab 14 --- Microsoft Teams with Graph

## Lab Objective

Build a small read-only Teams inventory. If your tenant does not permit
the required Graph access, complete the discovery and planning portions
without bypassing policy.

------------------------------------------------------------------------

# Exercise 1 --- Discover Team Commands

``` powershell
Get-Command '*MgTeam*' |
    Sort-Object Name
```

Find commands for:

``` text
Teams
Channels
Members
```

------------------------------------------------------------------------

# Exercise 2 --- Research Permissions

Use `Find-MgGraphCommand` on the read commands you selected.

Record the least-privileged read permissions that appear appropriate for
your scenario.

``` text
________________________________________
```

------------------------------------------------------------------------

# Exercise 3 --- Retrieve a Small Team Sample

After an authorized connection, retrieve a small number of teams.

Use Help to determine the appropriate syntax for your installed SDK
version.

Store the results:

``` powershell
$teams = # Your command
```

Display useful properties.

------------------------------------------------------------------------

# Exercise 4 --- Retrieve Channels

Choose one authorized team.

Use:

``` powershell
Get-MgTeamChannel -TeamId '<team-id>'
```

Display:

``` text
DisplayName
Description
MembershipType
```

------------------------------------------------------------------------

# Exercise 5 --- Discover Membership

Find the Graph command for retrieving team members.

``` powershell
Get-Command '*MgTeamMember*'
```

Use Help and retrieve membership only if authorized.

Do not add or remove members.

------------------------------------------------------------------------

# Exercise 6 --- Build an Inventory

For a small sample, create a report containing at least:

``` text
Team ID
Team display name
Channel count
```

Optional:

``` text
Member count
Owner count
```

Be aware that these values can require additional Graph requests.

------------------------------------------------------------------------

# Exercise 7 --- Group Relationship

Why is the relationship between a Team and its Microsoft 365 group
useful when building administrative reports?

``` text
____________________________________________________
```

------------------------------------------------------------------------

# Knowledge Check

1.  Which Graph resource is used for channels?\
    A. Team channel\
    B. User license\
    C. Device\
    D. Application credential

2.  Can changing Team membership affect access?\
    A. Yes\
    B. No

3.  Is Graph the only PowerShell administration option for Teams?\
    A. No\
    B. Yes

------------------------------------------------------------------------

# Lab Complete

Continue to:

[Lesson 15 --- SharePoint and OneDrive with
Graph](../lessons/lesson-15-sharepoint-and-onedrive-with-graph.md)
