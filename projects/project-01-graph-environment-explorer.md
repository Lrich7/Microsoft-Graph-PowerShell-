# Project 01 --- Microsoft Graph Environment Explorer

## Lessons Used

This project reinforces approximately Lessons **01--05**:

``` text
Introduction to Microsoft Graph
Installing the Graph SDK
Connecting to Graph
Permissions and scopes
Finding Graph commands
```

------------------------------------------------------------------------

# Project Goal

Build a PowerShell script that inspects your Microsoft Graph environment
without making tenant changes.

The finished tool should help an administrator answer:

``` text
Am I connected?
Which tenant am I connected to?
Which account/authentication type am I using?
Which scopes are present?
Which Graph modules are installed?
Can I discover commands for a requested resource?
```

------------------------------------------------------------------------

# Requirements

Your script should:

1.  Check whether Microsoft Graph modules are installed.
2.  Display installed Graph module versions.
3.  Check `Get-MgContext`.
4.  Display safe context information.
5.  Accept a search term such as `User`, `Group`, or `Device`.
6.  Find matching Graph commands.
7.  Allow the administrator to inspect Help for a selected command.
8.  Avoid making changes to the tenant.

------------------------------------------------------------------------

# Suggested Output

``` text
MICROSOFT GRAPH ENVIRONMENT EXPLORER

Connected: Yes
Tenant: <tenant>
Authentication Type: Delegated
Account: <account>

Installed Graph Modules:
Microsoft.Graph.Authentication
Microsoft.Graph.Users
...

Command Search: User

Get-MgUser
Get-MgUserLicenseDetail
...
```

------------------------------------------------------------------------

# Suggested Script Structure

``` powershell
param(
    [string]$Search = 'User'
)

# Check modules
# Check Graph context
# Display context
# Search commands
# Display results
```

------------------------------------------------------------------------

# Challenge Tasks

Add:

-   A check for the installed PowerShell version.
-   A warning if Graph is not connected.
-   A count of matching commands.
-   An option to export module information.
-   Error handling.

------------------------------------------------------------------------

# Completion Checklist

``` text
[ ] Script checks Graph installation
[ ] Script checks Graph context
[ ] Script displays safe connection information
[ ] Script searches Graph commands
[ ] Script does not change tenant data
[ ] Output is readable
[ ] No secrets are stored
[ ] Script includes comments
```

------------------------------------------------------------------------

# What You Practiced

This project combines Graph setup, authentication awareness,
permissions, command discovery, and basic PowerShell scripting.
