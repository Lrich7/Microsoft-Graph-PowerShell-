# Microsoft Graph PowerShell Cheat Sheet

A quick-reference guide for common Microsoft Graph PowerShell tasks.

> **Tip:** Use this as a reference while working through the lessons and labs. For unfamiliar commands, always verify current Microsoft documentation and required permissions before running them in a tenant.

---

# Quick Start

## Check PowerShell Version

```powershell
$PSVersionTable.PSVersion
```

## Check Installed Graph Modules

```powershell
Get-Module Microsoft.Graph* -ListAvailable
```

## Install Microsoft Graph PowerShell

```powershell
Install-Module Microsoft.Graph `
    -Scope CurrentUser `
    -Repository PSGallery
```

## Import Authentication Module

```powershell
Import-Module Microsoft.Graph.Authentication
```

---

# Connect to Microsoft Graph

## Delegated Sign-In

```powershell
Connect-MgGraph -Scopes 'User.Read'
```

## Multiple Scopes

```powershell
Connect-MgGraph -Scopes `
    'User.Read.All',
    'Group.Read.All'
```

## Device Authentication

```powershell
Connect-MgGraph `
    -Scopes 'User.Read' `
    -UseDeviceAuthentication
```

## Verify Current Context

```powershell
Get-MgContext
```

## Useful Context Properties

```powershell
$context = Get-MgContext

$context.Account
$context.TenantId
$context.AuthType
$context.Scopes
```

## Disconnect

```powershell
Disconnect-MgGraph
```

---

# Safe Connection Workflow

```text
Define task
   ↓
Determine required permission
   ↓
Connect-MgGraph
   ↓
Get-MgContext
   ↓
Verify account / tenant / scopes
   ↓
Perform work
   ↓
Disconnect-MgGraph
```

---

# Find Commands

## Search Graph Commands

```powershell
Get-Command -Name '*MgUser*'
Get-Command -Name '*MgGroup*'
Get-Command -Name '*MgDevice*'
```

## Commands in a Module

```powershell
Get-Command -Module Microsoft.Graph.Users
```

## Read Help

```powershell
Get-Help Get-MgUser
```

## Examples

```powershell
Get-Help Get-MgUser -Examples
```

## Parameter Help

```powershell
Get-Help Get-MgUser -Parameter UserId
```

---

# Graph-Specific Discovery

## Find the Graph API Operation for a Cmdlet

```powershell
Find-MgGraphCommand -Command Get-MgUser
```

## Find Permissions for a Cmdlet

```powershell
Find-MgGraphCommand -Command Get-MgUser |
    Select-Object -First 1 -ExpandProperty Permissions
```

## Search Permissions

```powershell
Find-MgGraphPermission 'User.Read'
Find-MgGraphPermission user
```

---

# Common Graph Command Verbs

```text
Get       Retrieve information
New       Create an object
Update    Modify an object
Remove    Delete an object
Set       Change or assign something
Invoke    Perform an action
```

> **Safety:** `Get-Mg...` commands are usually the best starting point for learning and reporting.

---

# Permissions

## Common Patterns

```text
User.Read
User.Read.All
User.ReadWrite.All

Group.Read.All
Group.ReadWrite.All

Device.Read.All
Directory.Read.All
Directory.ReadWrite.All
```

## Permission Types

```text
Delegated
    Signed-in user present

Application
    App-only / unattended automation
```

## Least Privilege

Use read permissions for read-only reporting whenever possible.

Do not request broad write permissions simply because they are easier.

---

# Users

## Get Users

```powershell
Get-MgUser
```

## First 10 Users

```powershell
Get-MgUser -Top 10
```

## All Users

```powershell
Get-MgUser -All
```

## Specific User

```powershell
Get-MgUser -UserId 'user@contoso.com'
```

## Request Additional Properties

```powershell
Get-MgUser -All `
    -Property Id,
        DisplayName,
        UserPrincipalName,
        Department,
        AccountEnabled
```

## Clean User Report

```powershell
Get-MgUser -All `
    -Property DisplayName,
        UserPrincipalName,
        Department,
        AccountEnabled |
    Select-Object DisplayName,
        UserPrincipalName,
        Department,
        AccountEnabled |
    Sort-Object DisplayName
```

## Enabled Users

```powershell
Get-MgUser `
    -Filter "accountEnabled eq true" `
    -All
```

## Users Missing Department

```powershell
Get-MgUser -All `
    -Property DisplayName,
        UserPrincipalName,
        Department |
    Where-Object {
        [string]::IsNullOrWhiteSpace($_.Department)
    }
```

---

# User Changes

## Discover Creation Command

```powershell
Get-Help New-MgUser -Examples
```

## Discover Update Command

```powershell
Get-Help Update-MgUser -Examples
```

## Update Pattern

```powershell
Update-MgUser `
    -UserId '<verified-user-id>' `
    -Department 'IT'
```

> Always retrieve and verify the target user before a write operation.

## Safe Change Pattern

```text
Find user
   ↓
Verify ID / UPN
   ↓
Display current value
   ↓
Preview proposed value
   ↓
Confirm authorization
   ↓
Change
   ↓
Retrieve again
   ↓
Verify
```

---

# Groups

## Get Groups

```powershell
Get-MgGroup
```

## All Groups

```powershell
Get-MgGroup -All
```

## Specific Group

```powershell
Get-MgGroup -GroupId '<group-id>'
```

## Useful Group Inventory

```powershell
Get-MgGroup -All |
    Select-Object Id,
        DisplayName,
        Mail,
        MailEnabled,
        SecurityEnabled,
        GroupTypes |
    Sort-Object DisplayName
```

---

# Group Members

## Direct Members

```powershell
Get-MgGroupMember `
    -GroupId '<group-id>' `
    -All
```

> Direct membership is not the same as transitive membership.

## Inspect Member Objects

```powershell
Get-MgGroupMember `
    -GroupId '<group-id>' `
    -Top 1 |
    Get-Member
```

Remember: group members can include more than users.

---

# Licenses

## Tenant License SKUs

```powershell
Get-MgSubscribedSku
```

## Useful SKU Properties

```powershell
Get-MgSubscribedSku |
    Select-Object SkuPartNumber,
        SkuId,
        ConsumedUnits
```

## Inspect a SKU

```powershell
$sku = Get-MgSubscribedSku |
    Select-Object -First 1

$sku.PrepaidUnits
$sku.ServicePlans
```

## Calculate Available Licenses

```powershell
Get-MgSubscribedSku |
    ForEach-Object {
        [pscustomobject]@{
            SkuPartNumber = $_.SkuPartNumber
            Enabled       = $_.PrepaidUnits.Enabled
            Consumed      = $_.ConsumedUnits
            Available     = $_.PrepaidUnits.Enabled - $_.ConsumedUnits
        }
    }
```

## User License Detail

```powershell
Get-MgUserLicenseDetail `
    -UserId 'user@contoso.com'
```

## Direct License Change Command

```powershell
Set-MgUserLicense
```

> This is a write operation. Verify the user, SKU, available capacity, permissions, and licensing model before using it.

---

# Devices

## Get Devices

```powershell
Get-MgDevice
```

## Device Inventory

```powershell
Get-MgDevice -All `
    -Property Id,
        DeviceId,
        DisplayName,
        AccountEnabled,
        OperatingSystem,
        OperatingSystemVersion,
        TrustType,
        ApproximateLastSignInDateTime |
    Select-Object DisplayName,
        DeviceId,
        AccountEnabled,
        OperatingSystem,
        OperatingSystemVersion,
        TrustType,
        ApproximateLastSignInDateTime
```

## Windows Devices

```powershell
Get-MgDevice -All `
    -Property DisplayName,
        OperatingSystem |
    Where-Object OperatingSystem -eq 'Windows'
```

## Disabled Devices

```powershell
Get-MgDevice -All `
    -Property DisplayName,
        AccountEnabled |
    Where-Object AccountEnabled -eq $false
```

---

# Applications

## Get App Registrations

```powershell
Get-MgApplication -Top 10
```

## Useful Properties

```powershell
Get-MgApplication -All |
    Select-Object Id,
        AppId,
        DisplayName
```

Remember:

```text
Id      Graph object ID
AppId   Application / client ID
```

---

# Service Principals

## Get Service Principals

```powershell
Get-MgServicePrincipal -Top 10
```

## Useful Report

```powershell
Get-MgServicePrincipal -All |
    Select-Object Id,
        AppId,
        DisplayName,
        ServicePrincipalType,
        AccountEnabled
```

> Application objects and service principals are related, but they are not the same thing.

---

# Directory Roles

## Find Role Commands

```powershell
Get-Command '*MgRoleManagementDirectory*'
```

## Role Definitions

```powershell
Get-MgRoleManagementDirectoryRoleDefinition |
    Select-Object Id,
        DisplayName,
        IsBuiltIn
```

## Role Assignments

```powershell
Get-MgRoleManagementDirectoryRoleAssignment -All
```

Useful assignment properties include:

```text
PrincipalId
RoleDefinitionId
DirectoryScopeId
```

---

# Microsoft Teams

## Discover Teams Commands

```powershell
Get-Command '*MgTeam*'
```

## Get a Team

```powershell
Get-MgTeam -TeamId '<team-id>'
```

## Channels

```powershell
Get-MgTeamChannel `
    -TeamId '<team-id>'
```

## Find Membership Commands

```powershell
Get-Command '*MgTeamMember*'
```

> Teams membership changes can affect access. Start with inventory and reporting.

---

# SharePoint and OneDrive

## Discover Site Commands

```powershell
Get-Command '*MgSite*'
```

## Discover Site Drive Commands

```powershell
Get-Command '*MgSiteDrive*'
```

## Conceptual Hierarchy

```text
Site
  ↓
Drive / document library
  ↓
DriveItem
  ↓
File or folder
```

## Discover Drive Commands

```powershell
Get-Command '*MgDrive*'
```

> Prefer metadata inventory before requesting file-content or write permissions.

---

# Filtering and Querying

## Limit Results

```powershell
Get-MgUser -Top 10
```

## Retrieve All Pages

```powershell
Get-MgUser -All
```

## Server-Side Filter

```powershell
Get-MgUser `
    -Filter "accountEnabled eq true" `
    -All
```

## Local PowerShell Filter

```powershell
Get-MgUser -All |
    Where-Object AccountEnabled -eq $true
```

## Request Specific Properties

```powershell
Get-MgUser -All `
    -Property DisplayName,
        UserPrincipalName,
        Department
```

---

# Advanced Queries

Some directory queries may require:

```powershell
-ConsistencyLevel eventual
```

Example pattern:

```powershell
$count = 0

Get-MgUser `
    -ConsistencyLevel eventual `
    -CountVariable count `
    -All
```

Always verify whether the specific Graph query requires advanced-query settings.

---

# Export Data

## CSV

```powershell
$users |
    Export-Csv .\users.csv `
    -NoTypeInformation
```

## JSON

```powershell
$users |
    ConvertTo-Json -Depth 5 |
    Set-Content .\users.json
```

---

# Useful Reporting Pattern

```text
Connect
   ↓
Verify Context
   ↓
Collect
   ↓
Filter
   ↓
Sort
   ↓
Select
   ↓
Export
   ↓
Disconnect
```

Example:

```powershell
Connect-MgGraph -Scopes 'User.Read.All'

Get-MgContext

Get-MgUser -All `
    -Property DisplayName,
        UserPrincipalName,
        AccountEnabled |
    Where-Object AccountEnabled -eq $true |
    Sort-Object DisplayName |
    Select-Object DisplayName,
        UserPrincipalName |
    Export-Csv .\enabled-users.csv `
        -NoTypeInformation

Disconnect-MgGraph
```

---

# Error Handling

## Basic Pattern

```powershell
try {
    Get-MgUser `
        -UserId $UserId `
        -ErrorAction Stop
}
catch {
    Write-Warning $_.Exception.Message
}
```

## Context Check

```powershell
$context = Get-MgContext

if ($null -eq $context) {
    throw 'Microsoft Graph is not connected.'
}
```

## Recommended Workflow

```text
Validate
   ↓
Attempt
   ↓
Catch
   ↓
Log
   ↓
Continue or Stop Intentionally
```

---

# App-Only Authentication

## Certificate-Based Pattern

```powershell
Connect-MgGraph `
    -ClientId '<application-id>' `
    -TenantId '<tenant-id>' `
    -CertificateThumbprint '<certificate-thumbprint>'
```

Then:

```powershell
Get-MgContext
```

---

# Delegated vs. App-Only

```text
Delegated
    Interactive user signs in
    Uses delegated permissions

App-Only
    Application authenticates
    Uses application permissions
    Useful for unattended automation
```

---

# Never Put These in Git

```text
Passwords
Client secrets
Access tokens
Private keys
Private organizational reports
Sensitive tenant information
```

---

# Efficient Graph Scripting

Prefer:

```text
-Top while testing
Server-side filters
Only needed properties
One retrieval reused many times
Cached lookup data
```

Avoid:

```text
Get everything automatically
One Graph request inside every loop
Repeatedly retrieving static tenant data
Unnecessary broad permissions
```

---

# Troubleshooting Graph PowerShell

## Command Not Found

```powershell
Get-Module Microsoft.Graph* -ListAvailable
```

Then:

```powershell
Get-Command '<command>'
```

## Connected but Forbidden

Check:

```powershell
Get-MgContext
```

Verify:

```text
Account
Tenant
Scopes
Required permission
Administrative role if applicable
Consent
```

## Wrong Tenant or Account

```powershell
Disconnect-MgGraph
```

Reconnect intentionally.

## Property Is Blank

Check whether the property must be explicitly requested with:

```powershell
-Property
```

## Too Few Results

Check:

```text
-Top
-All
Pagination
Filter
```

---

# Common Safety Rules

```text
1. Verify the tenant before administrative work.
2. Verify the target object.
3. Use least privilege.
4. Start with Get-Mg... commands.
5. Preview bulk changes.
6. Never commit secrets.
7. Read back important changes.
8. Use a test tenant when learning write operations.
9. Document application permissions.
10. Disconnect when finished.
```

---

# Common Commands at a Glance

```text
Connect-MgGraph
Get-MgContext
Disconnect-MgGraph

Find-MgGraphCommand
Find-MgGraphPermission

Get-MgUser
New-MgUser
Update-MgUser

Get-MgGroup
Get-MgGroupMember

Get-MgSubscribedSku
Get-MgUserLicenseDetail
Set-MgUserLicense

Get-MgDevice

Get-MgApplication
Get-MgServicePrincipal

Get-MgRoleManagementDirectoryRoleDefinition
Get-MgRoleManagementDirectoryRoleAssignment

Get-MgTeam
Get-MgTeamChannel

Get-MgSite
```

---

# Official Microsoft Resources

**Microsoft Graph PowerShell documentation:**  
https://learn.microsoft.com/powershell/microsoftgraph/

**Get started with Microsoft Graph PowerShell:**  
https://learn.microsoft.com/powershell/microsoftgraph/get-started

**Microsoft Graph PowerShell installation:**  
https://learn.microsoft.com/powershell/microsoftgraph/installation

**Find Graph commands:**  
https://learn.microsoft.com/powershell/microsoftgraph/find-mg-graph-command

**Find Graph permissions:**  
https://learn.microsoft.com/powershell/microsoftgraph/find-mg-graph-permission

**Microsoft Graph permissions reference:**  
https://learn.microsoft.com/graph/permissions-reference

**Microsoft Graph API documentation:**  
https://learn.microsoft.com/graph/

---

# Quick Reminder

You do **not** need to memorize Microsoft Graph PowerShell.

Remember:

```text
Get-Command
     ↓
Get-Help
     ↓
Find-MgGraphCommand
     ↓
Find-MgGraphPermission
     ↓
Connect-MgGraph
     ↓
Get-MgContext
     ↓
Get-Mg...
```

If you can discover the command, understand its permissions, verify your context, and safely work with the returned objects, you can continue learning Microsoft Graph PowerShell as the platform changes.
