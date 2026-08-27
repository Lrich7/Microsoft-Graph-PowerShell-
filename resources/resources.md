# Microsoft Graph PowerShell Resources

A curated collection of official Microsoft resources for learning, troubleshooting, and working with Microsoft Graph PowerShell.

> **Recommendation:** Start with the Microsoft Learn and Microsoft Graph documentation links below. Use community examples only after you understand the command, permissions, and effect of the operation.

---

# Start Here

## Microsoft Graph PowerShell Documentation

Official Microsoft Graph PowerShell documentation:

https://learn.microsoft.com/powershell/microsoftgraph/

Use this for:

```text
Installation
Getting started
Authentication
Command discovery
App-only authentication
Migration guidance
Troubleshooting
Cmdlet reference
```

---

## Microsoft Graph PowerShell Overview

https://learn.microsoft.com/powershell/microsoftgraph/overview

This is a good introduction to:

```text
What the SDK is
How it relates to Microsoft Graph
Why Microsoft recommends it
Supported PowerShell versions
Migration from Azure AD / MSOnline
```

---

## Microsoft Graph Overview

https://learn.microsoft.com/graph/overview

Use this when you want to understand Microsoft Graph itself rather than only the PowerShell SDK.

Topics include:

```text
Microsoft Entra ID
Microsoft 365
Users
Groups
Devices
Applications
Teams
SharePoint
OneDrive
Outlook
APIs
```

---

# Installation and Setup

## Install Microsoft Graph PowerShell

https://learn.microsoft.com/powershell/microsoftgraph/installation

Microsoft currently recommends PowerShell 7 or later for Microsoft Graph PowerShell.

Typical installation:

```powershell
Install-Module Microsoft.Graph `
    -Scope CurrentUser `
    -Repository PSGallery
```

Check installed modules:

```powershell
Get-Module Microsoft.Graph* -ListAvailable
```

---

## PowerShell Gallery — Microsoft.Graph

https://www.powershellgallery.com/packages/Microsoft.Graph

Use the PowerShell Gallery to review:

```text
Current SDK version
Published versions
Dependencies
Module information
```

---

# Getting Started

## Microsoft Graph PowerShell Get Started

https://learn.microsoft.com/powershell/microsoftgraph/get-started

A good next step after installing the SDK.

Use it for:

```text
Connecting
Permissions
Basic Graph commands
Reading objects
Working with Graph PowerShell
```

---

# Authentication

## Authentication Commands

https://learn.microsoft.com/powershell/microsoftgraph/authentication-commands

Covers:

```text
Connect-MgGraph
Disconnect-MgGraph
Get-MgContext
Get-MgEnvironment
Invoke-MgGraphRequest
Delegated authentication
Device authentication
App-only authentication
```

Useful commands:

```powershell
Connect-MgGraph
Get-MgContext
Disconnect-MgGraph
```

---

## App-Only Authentication

https://learn.microsoft.com/powershell/microsoftgraph/app-only

Use this when learning unattended Graph automation.

Topics include:

```text
Application registrations
Service principals
Application permissions
Certificates
Admin consent
Unattended PowerShell scripts
```

> App-only access can provide broad tenant access. Use least privilege and a controlled test environment while learning.

---

# Permissions

## Microsoft Graph Permissions Overview

https://learn.microsoft.com/graph/permissions-overview

Explains:

```text
Delegated permissions
Application permissions
Consent
Admin consent
Least privilege
```

---

## Microsoft Graph Permissions Reference

https://learn.microsoft.com/graph/permissions-reference

Use this when researching the actual permission required for a Graph operation.

Examples:

```text
User.Read
User.Read.All
Group.Read.All
Device.Read.All
Directory.Read.All
```

---

## Find Permissions with PowerShell

Microsoft Graph PowerShell includes:

```powershell
Find-MgGraphPermission
```

Documentation:

https://learn.microsoft.com/powershell/microsoftgraph/find-mg-graph-permission

Example:

```powershell
Find-MgGraphPermission 'User.Read'
```

---

# Finding Microsoft Graph Commands

## Find-MgGraphCommand

Documentation:

https://learn.microsoft.com/powershell/microsoftgraph/find-mg-graph-command

Example:

```powershell
Find-MgGraphCommand -Command Get-MgUser
```

This can help identify:

```text
Graph command
Module
API operation
HTTP method
Permissions
```

---

## PowerShell Command Discovery

Do not forget standard PowerShell discovery tools:

```powershell
Get-Command
Get-Help
Get-Member
```

Examples:

```powershell
Get-Command '*MgUser*'
```

```powershell
Get-Help Get-MgUser -Examples
```

```powershell
Get-MgUser -Top 1 |
    Get-Member
```

---

# Microsoft Graph Explorer

## Graph Explorer

https://developer.microsoft.com/graph/graph-explorer

Graph Explorer lets you test Microsoft Graph API requests in a browser.

Use it to:

```text
Explore Graph endpoints
Test GET requests
Inspect JSON responses
Review required permissions
Learn Graph API paths
```

> Verify the account and tenant before signing in and granting permissions.

Graph Explorer is especially useful for understanding what Graph PowerShell is doing underneath the cmdlets.

---

# Microsoft Graph API Reference

https://learn.microsoft.com/graph/api/overview

Use the API reference when:

```text
A PowerShell cmdlet behaves unexpectedly
You need to understand the underlying resource
You need supported query options
You need request/response examples
You are using Invoke-MgGraphRequest
```

---

# Users

## User Resource

https://learn.microsoft.com/graph/api/resources/user

## Get-MgUser

https://learn.microsoft.com/powershell/module/microsoft.graph.users/get-mguser

Common examples:

```powershell
Get-MgUser -Top 10
```

```powershell
Get-MgUser -All
```

```powershell
Get-MgUser -UserId 'user@contoso.com'
```

---

# Groups

## Group Resource

https://learn.microsoft.com/graph/api/resources/group

## Get-MgGroup

https://learn.microsoft.com/powershell/module/microsoft.graph.groups/get-mggroup

## Get-MgGroupMember

https://learn.microsoft.com/powershell/module/microsoft.graph.groups/get-mggroupmember

Use these resources for:

```text
Group inventory
Group types
Membership
Owners
Microsoft 365 groups
Security groups
```

---

# Licensing

## Microsoft 365 License and Service Details

https://learn.microsoft.com/microsoft-365/enterprise/view-account-license-and-service-details-with-microsoft-365-powershell

Useful Graph commands include:

```powershell
Get-MgSubscribedSku
Get-MgUserLicenseDetail
Set-MgUserLicense
```

---

## subscribedSku Resource

https://learn.microsoft.com/graph/api/resources/subscribedsku

Useful for understanding:

```text
SkuId
SkuPartNumber
ConsumedUnits
PrepaidUnits
ServicePlans
```

---

# Devices

## Device Resource

https://learn.microsoft.com/graph/api/resources/device

## Get-MgDevice

https://learn.microsoft.com/powershell/module/microsoft.graph.identity.directorymanagement/get-mgdevice

Useful for:

```text
Microsoft Entra device inventory
Operating system information
Enabled/disabled state
Trust type
Device identifiers
```

---

# Applications and Service Principals

## Application Resource

https://learn.microsoft.com/graph/api/resources/application

## Service Principal Resource

https://learn.microsoft.com/graph/api/resources/serviceprincipal

## Application and Service Principal Concepts

https://learn.microsoft.com/entra/identity-platform/app-objects-and-service-principals

Important distinction:

```text
Application object
        ≠
Service principal
```

Related commands:

```powershell
Get-MgApplication
Get-MgServicePrincipal
```

---

# Microsoft Entra Directory Roles

## Microsoft Entra Role-Based Access Control

https://learn.microsoft.com/entra/identity/role-based-access-control/

Use this to understand:

```text
Directory roles
Role definitions
Role assignments
Administrative privileges
Least privilege
```

Graph PowerShell discovery:

```powershell
Get-Command '*MgRoleManagementDirectory*'
```

---

# Microsoft Teams

## Microsoft Graph Teams Overview

https://learn.microsoft.com/graph/teams-concept-overview

## Team Resource

https://learn.microsoft.com/graph/api/resources/team

Use this for:

```text
Teams
Channels
Members
Owners
Teams-related Graph resources
```

---

## Microsoft Teams PowerShell

https://learn.microsoft.com/microsoftteams/teams-powershell-overview

Remember:

> Microsoft Graph is not the only administration interface for Microsoft Teams.

Always choose the supported tool that best fits the task.

---

# SharePoint and OneDrive

## Site Resource

https://learn.microsoft.com/graph/api/resources/site

## Drive Resource

https://learn.microsoft.com/graph/api/resources/drive

## DriveItem Resource

https://learn.microsoft.com/graph/api/resources/driveitem

Useful mental model:

```text
Site
  ↓
Drive / document library
  ↓
DriveItem
  ↓
File or folder
```

---

# Advanced Queries

## Advanced Query Capabilities

https://learn.microsoft.com/graph/aad-advanced-queries

Covers Graph directory queries involving concepts such as:

```text
$filter
$count
$search
$orderby
ConsistencyLevel eventual
```

Graph PowerShell may expose these through parameters such as:

```powershell
-Filter
-ConsistencyLevel
-CountVariable
```

---

# Pagination

## Microsoft Graph Paging

https://learn.microsoft.com/graph/paging

Use this to understand why Graph returns data in multiple pages.

In Graph PowerShell, many cmdlets support:

```powershell
-All
```

Example:

```powershell
Get-MgUser -All
```

---

# Throttling

## Microsoft Graph Throttling Guidance

https://learn.microsoft.com/graph/throttling

Read this before building large or frequently scheduled Graph scripts.

Common causes of excessive request volume include:

```text
Large loops
One Graph request per object
Repeatedly retrieving the same data
Large recursive queries
Polling too frequently
```

---

# What's New

## Microsoft Graph — What's New

https://learn.microsoft.com/graph/whats-new-overview

Microsoft Graph changes regularly.

Use this resource to monitor:

```text
New generally available APIs
Preview features
API changes
SDK changes
New Microsoft 365 capabilities
```

> Preview functionality can change. Prefer stable v1.0 functionality for production scripts whenever it meets the requirement.

---

# Migration from Azure AD and MSOnline

## Microsoft Graph PowerShell Overview

https://learn.microsoft.com/powershell/microsoftgraph/overview

Microsoft recommends Microsoft Graph PowerShell as the replacement direction for older:

```text
AzureAD
MSOnline
```

PowerShell modules.

If you encounter older scripts, do not simply replace command names.

Review:

```text
Command behavior
Permissions
Authentication
Object properties
Output
Error handling
```

---

# Microsoft Entra PowerShell

Microsoft also provides the Microsoft Entra PowerShell module.

Overview:

https://learn.microsoft.com/powershell/entra-powershell/overview

It is built on Microsoft Graph and is interoperable with Graph PowerShell cmdlets.

This course focuses primarily on:

```text
Microsoft.Graph
```

but Microsoft Entra PowerShell is worth knowing about when working with identity administration.

---

# Recommended Learning Order

If you are new to Microsoft Graph PowerShell, use these resources in this order:

```text
1. Microsoft Graph Overview
        ↓
2. Graph PowerShell Overview
        ↓
3. Installation
        ↓
4. Get Started
        ↓
5. Authentication
        ↓
6. Permissions Overview
        ↓
7. Find-MgGraphCommand
        ↓
8. Find-MgGraphPermission
        ↓
9. Resource-specific documentation
        ↓
10. Advanced Queries / Pagination / Throttling
        ↓
11. App-Only Authentication
```

---

# Useful PowerShell Commands to Remember

```powershell
Get-Module Microsoft.Graph* -ListAvailable

Connect-MgGraph

Get-MgContext

Disconnect-MgGraph

Get-Command '*Mg*'

Get-Help <command> -Examples

Find-MgGraphCommand -Command <command>

Find-MgGraphPermission '<permission>'

Get-MgUser

Get-MgGroup

Get-MgSubscribedSku

Get-MgDevice

Get-MgApplication

Get-MgServicePrincipal
```

---

# Safety Resources

Before running administrative Graph scripts:

```text
Verify the tenant
Verify the signed-in account
Verify the requested permissions
Verify the target
Understand whether the operation is read or write
Use least privilege
Test with small result sets
Avoid committing secrets
Use controlled test identities for write exercises
```

---

# Bookmark These

If you only bookmark a few resources, start with:

**Microsoft Graph PowerShell:**  
https://learn.microsoft.com/powershell/microsoftgraph/

**Microsoft Graph:**  
https://learn.microsoft.com/graph/

**Graph Explorer:**  
https://developer.microsoft.com/graph/graph-explorer

**Permissions Reference:**  
https://learn.microsoft.com/graph/permissions-reference

**Graph PowerShell Installation:**  
https://learn.microsoft.com/powershell/microsoftgraph/installation

**Authentication:**  
https://learn.microsoft.com/powershell/microsoftgraph/authentication-commands

**Command Discovery:**  
https://learn.microsoft.com/powershell/microsoftgraph/find-mg-graph-command

**Permission Discovery:**  
https://learn.microsoft.com/powershell/microsoftgraph/find-mg-graph-permission

---

# Final Note

Microsoft Graph evolves regularly.

Rather than relying on an old blog post or copied command forever, build the habit of checking:

```text
Microsoft Learn
Microsoft Graph API documentation
PowerShell Help
Find-MgGraphCommand
Find-MgGraphPermission
Graph Explorer
```

Knowing how to find the current answer is one of the most valuable Microsoft Graph PowerShell skills you can develop.
