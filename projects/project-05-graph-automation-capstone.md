[project-05-graph-automation-capstone-remade.md](https://github.com/user-attachments/files/31532087/project-05-graph-automation-capstone-remade.md)
# Project 05 — Microsoft Graph Automation Capstone

## 🏆 Final Capstone Project

You have reached the final project of the **Microsoft Graph PowerShell Fundamentals** course.

This capstone brings together the skills developed throughout the entire training path.

Instead of practicing one command or Microsoft Graph resource at a time, you will design and build a reusable **Microsoft Graph PowerShell administration and reporting tool**.

The goal is to work through the project like a real Microsoft administrator:

```text
Define the requirement
        ↓
Identify Graph resources
        ↓
Research commands
        ↓
Determine permissions
        ↓
Authenticate safely
        ↓
Collect data
        ↓
Process results
        ↓
Export reports
        ↓
Handle errors
        ↓
Log activity
        ↓
Verify results
```

---

# 🎯 Project Objectives

By completing this project, you will demonstrate that you can:

- Connect to Microsoft Graph safely
- Verify Microsoft Graph context
- Work with delegated or app-only authentication
- Identify required Graph permissions
- Follow least-privilege principles
- Query multiple Microsoft Graph resources
- Work with users and groups
- Audit Microsoft 365 licensing
- Inventory Microsoft Entra devices
- Review applications and service principals
- Review directory roles
- Work with Microsoft 365 collaboration information
- Use filtering, sorting, and selected properties
- Handle pagination and larger result sets
- Export useful reports
- Add error handling
- Add logging
- Structure reusable PowerShell automation
- Protect credentials and sensitive information

---

# 🧠 Skills Used

This project combines concepts from across the course.

```text
Graph PowerShell setup
Authentication
Permissions and scopes
Command discovery
Users
Groups
Licensing
Devices
Applications
Service principals
Directory roles
Microsoft 365 workloads
Advanced queries
Pagination
Error handling
Logging
App-only authentication
Automation
```

You are not expected to memorize every command.

Use:

```powershell
Get-Command
```

```powershell
Get-Help
```

```powershell
Find-MgGraphCommand
```

```powershell
Find-MgGraphPermission
```

along with Microsoft Learn when needed.

---

# 📋 Scenario

Your IT team wants a reusable Microsoft Graph PowerShell tool that can generate a basic Microsoft 365 environment audit.

The tool should collect useful administrative information and save the results as reports.

Management may later use these reports to help answer questions such as:

```text
How many users exist?

Which users are enabled or disabled?

Which groups exist?

What Microsoft 365 licenses are available?

Which devices are registered?

Which applications exist?

Which service principals exist?

Which directory roles are assigned?
```

Your task is to build the first version of this tool.

---

# ⚠️ Safety Requirements

This project should primarily use **read-only operations**.

Do not add write operations simply to make the project more advanced.

Before running the tool:

```text
[ ] Verify the tenant
[ ] Verify the account or application
[ ] Verify permissions
[ ] Verify output location
[ ] Confirm reports do not expose sensitive data publicly
```

Never commit:

```text
Passwords
Client secrets
Access tokens
Private keys
Private organizational reports
Sensitive tenant information
```

to a public GitHub repository.

---

# 📁 Recommended Project Structure

Create a folder such as:

```text
Graph-Audit/
│
├── Graph-Audit.ps1
│
├── README.md
│
├── Output/
│
└── Logs/
```

Your script will be:

```text
Graph-Audit.ps1
```

Generated reports will go into:

```text
Output/
```

Logs will go into:

```text
Logs/
```

---

# Part 1 — Define Configuration

Start your script with configuration values.

Example:

```powershell
$OutputPath = Join-Path $PSScriptRoot 'Output'
$LogPath = Join-Path $PSScriptRoot 'Logs'

$Timestamp = Get-Date -Format 'yyyyMMdd-HHmmss'
```

Create the folders if they do not exist:

```powershell
foreach ($Path in @($OutputPath, $LogPath)) {

    if (-not (Test-Path $Path)) {
        New-Item `
            -ItemType Directory `
            -Path $Path |
        Out-Null
    }
}
```

---

# Part 2 — Create Logging

Create a log file:

```powershell
$LogFile = Join-Path `
    $LogPath `
    "Graph-Audit-$Timestamp.log"
```

Create a simple logging function:

```powershell
function Write-Log {

    param(
        [Parameter(Mandatory)]
        [string]$Message
    )

    $Entry = "$(Get-Date -Format s) - $Message"

    $Entry |
        Tee-Object `
            -FilePath $LogFile `
            -Append
}
```

Test:

```powershell
Write-Log 'Microsoft Graph audit started.'
```

---

# Part 3 — Authentication

Choose one authentication method.

## Option A — Delegated Authentication

For an interactive training environment:

```powershell
Connect-MgGraph -Scopes `
    'User.Read.All',
    'Group.Read.All',
    'Device.Read.All',
    'Application.Read.All',
    'RoleManagement.Read.Directory',
    'Organization.Read.All'
```

The exact permissions required may vary based on the reports you build.

Research each permission before requesting it.

---

## Option B — App-Only Authentication

If you completed the app-only setup from Lesson and Lab 18, you may use a certificate-based connection.

Example pattern:

```powershell
$TenantId = '<tenant-id>'
$ClientId = '<application-id>'
$Thumbprint = '<certificate-thumbprint>'

Connect-MgGraph `
    -TenantId $TenantId `
    -ClientId $ClientId `
    -CertificateThumbprint $Thumbprint
```

Do not place private keys, passwords, or client secrets in the script.

---

# Part 4 — Verify Graph Context

Immediately after connecting:

```powershell
$Context = Get-MgContext
```

Verify that a context exists:

```powershell
if ($null -eq $Context) {
    throw 'Microsoft Graph connection was not established.'
}
```

Display useful information:

```powershell
$Context |
    Select-Object Account,
        TenantId,
        ClientId,
        AuthType,
        Scopes
```

Add:

```powershell
Write-Log "Connected to Microsoft Graph tenant $($Context.TenantId)."
```

If you know the expected tenant ID, validate it before continuing.

Example:

```powershell
if ($Context.TenantId -ne $ExpectedTenantId) {
    throw 'Connected to an unexpected Microsoft Graph tenant.'
}
```

---

# Part 5 — User Inventory

Retrieve users.

Example:

```powershell
$Users = Get-MgUser `
    -All `
    -Property Id,
        DisplayName,
        UserPrincipalName,
        AccountEnabled,
        Department
```

Create a clean report:

```powershell
$UserReport = $Users |
    Select-Object DisplayName,
        UserPrincipalName,
        AccountEnabled,
        Department |
    Sort-Object DisplayName
```

Export:

```powershell
$UserReport |
    Export-Csv `
        (Join-Path $OutputPath "Users-$Timestamp.csv") `
        -NoTypeInformation
```

Log:

```powershell
Write-Log "User report created. Users found: $($Users.Count)"
```

---

# Part 6 — Group Inventory

Retrieve groups:

```powershell
$Groups = Get-MgGroup -All
```

Create a report:

```powershell
$GroupReport = $Groups |
    Select-Object DisplayName,
        Mail,
        MailEnabled,
        SecurityEnabled,
        GroupTypes |
    Sort-Object DisplayName
```

Export:

```powershell
$GroupReport |
    Export-Csv `
        (Join-Path $OutputPath "Groups-$Timestamp.csv") `
        -NoTypeInformation
```

Log:

```powershell
Write-Log "Group report created. Groups found: $($Groups.Count)"
```

---

# Part 7 — License Inventory

Retrieve tenant subscriptions:

```powershell
$Skus = Get-MgSubscribedSku
```

Build a useful report:

```powershell
$LicenseReport = $Skus |
    ForEach-Object {

        [pscustomobject]@{
            SkuPartNumber = $_.SkuPartNumber
            SkuId         = $_.SkuId
            Enabled       = $_.PrepaidUnits.Enabled
            Consumed      = $_.ConsumedUnits
            Available     = $_.PrepaidUnits.Enabled - $_.ConsumedUnits
        }
    }
```

Export:

```powershell
$LicenseReport |
    Export-Csv `
        (Join-Path $OutputPath "Licenses-$Timestamp.csv") `
        -NoTypeInformation
```

---

# Part 8 — Device Inventory

Retrieve Microsoft Entra devices:

```powershell
$Devices = Get-MgDevice `
    -All `
    -Property Id,
        DeviceId,
        DisplayName,
        AccountEnabled,
        OperatingSystem,
        OperatingSystemVersion,
        TrustType,
        ApproximateLastSignInDateTime
```

Create:

```powershell
$DeviceReport = $Devices |
    Select-Object DisplayName,
        DeviceId,
        AccountEnabled,
        OperatingSystem,
        OperatingSystemVersion,
        TrustType,
        ApproximateLastSignInDateTime |
    Sort-Object DisplayName
```

Export:

```powershell
$DeviceReport |
    Export-Csv `
        (Join-Path $OutputPath "Devices-$Timestamp.csv") `
        -NoTypeInformation
```

---

# Part 9 — Application Inventory

Retrieve application registrations:

```powershell
$Applications = Get-MgApplication -All
```

Create:

```powershell
$ApplicationReport = $Applications |
    Select-Object DisplayName,
        AppId,
        Id |
    Sort-Object DisplayName
```

Export:

```powershell
$ApplicationReport |
    Export-Csv `
        (Join-Path $OutputPath "Applications-$Timestamp.csv") `
        -NoTypeInformation
```

Remember:

```text
Id
```

and:

```text
AppId
```

are different identifiers.

---

# Part 10 — Service Principal Inventory

Retrieve:

```powershell
$ServicePrincipals = Get-MgServicePrincipal -All
```

Create:

```powershell
$ServicePrincipalReport = $ServicePrincipals |
    Select-Object DisplayName,
        AppId,
        Id,
        ServicePrincipalType,
        AccountEnabled |
    Sort-Object DisplayName
```

Export:

```powershell
$ServicePrincipalReport |
    Export-Csv `
        (Join-Path $OutputPath "ServicePrincipals-$Timestamp.csv") `
        -NoTypeInformation
```

---

# Part 11 — Directory Role Inventory

Retrieve role definitions:

```powershell
$RoleDefinitions =
    Get-MgRoleManagementDirectoryRoleDefinition
```

Retrieve assignments:

```powershell
$RoleAssignments =
    Get-MgRoleManagementDirectoryRoleAssignment -All
```

Create a basic assignment report:

```powershell
$RoleAssignmentReport = $RoleAssignments |
    Select-Object PrincipalId,
        RoleDefinitionId,
        DirectoryScopeId
```

Export:

```powershell
$RoleAssignmentReport |
    Export-Csv `
        (Join-Path $OutputPath "DirectoryRoles-$Timestamp.csv") `
        -NoTypeInformation
```

---

# Part 12 — Create a Summary

Build an audit summary.

```powershell
$Summary = [pscustomobject]@{

    Generated = Get-Date

    Users = $Users.Count

    EnabledUsers = (
        $Users |
        Where-Object AccountEnabled -eq $true
    ).Count

    DisabledUsers = (
        $Users |
        Where-Object AccountEnabled -eq $false
    ).Count

    Groups = $Groups.Count

    Devices = $Devices.Count

    Applications = $Applications.Count

    ServicePrincipals = $ServicePrincipals.Count

    DirectoryRoleAssignments = $RoleAssignments.Count
}
```

Display it:

```powershell
$Summary |
    Format-List
```

Export:

```powershell
$Summary |
    Export-Csv `
        (Join-Path $OutputPath "Summary-$Timestamp.csv") `
        -NoTypeInformation
```

---

# Part 13 — Improve Error Handling

Do not allow one failed report to make the entire script impossible to troubleshoot.

A basic project structure might be:

```powershell
try {

    Write-Log 'Connecting to Microsoft Graph.'

    # Connect

    # Validate context

    # Collect data

    # Export reports

    Write-Log 'Microsoft Graph audit completed successfully.'
}
catch {

    Write-Log "ERROR: $($_.Exception.Message)"

    Write-Error $_
}
finally {

    Disconnect-MgGraph `
        -ErrorAction SilentlyContinue

    Write-Log 'Microsoft Graph session closed.'
}
```

For a more advanced version, use separate functions and error handling for each report.

---

# Part 14 — Convert the Script into Functions

Improve the design by creating functions.

Suggested functions:

```text
Write-Log
Connect-GraphAudit
Test-GraphContext
Get-GraphUserReport
Get-GraphGroupReport
Get-GraphLicenseReport
Get-GraphDeviceReport
Get-GraphApplicationReport
Get-GraphServicePrincipalReport
Get-GraphRoleReport
New-GraphAuditSummary
```

Example:

```powershell
function Get-GraphUserReport {

    param(
        [Parameter(Mandatory)]
        [string]$OutputPath,

        [Parameter(Mandatory)]
        [string]$Timestamp
    )

    $Users = Get-MgUser `
        -All `
        -Property DisplayName,
            UserPrincipalName,
            AccountEnabled,
            Department

    $Users |
        Select-Object DisplayName,
            UserPrincipalName,
            AccountEnabled,
            Department |
        Sort-Object DisplayName |
        Export-Csv `
            (Join-Path $OutputPath "Users-$Timestamp.csv") `
            -NoTypeInformation

    return $Users
}
```

---

# Part 15 — Add Parameters

Make the script reusable.

Example:

```powershell
param(

    [string]$OutputPath =
        (Join-Path $PSScriptRoot 'Output'),

    [switch]$Users,

    [switch]$Groups,

    [switch]$Licenses,

    [switch]$Devices,

    [switch]$Applications,

    [switch]$Roles,

    [switch]$All
)
```

Eventually you could run:

```powershell
.\Graph-Audit.ps1 -Users
```

or:

```powershell
.\Graph-Audit.ps1 -Users -Groups -Licenses
```

or:

```powershell
.\Graph-Audit.ps1 -All
```

---

# Part 16 — Add Progress Messages

Make the tool easier to use.

Example:

```powershell
Write-Host 'Collecting users...'
```

```powershell
Write-Host 'Collecting groups...'
```

```powershell
Write-Host 'Collecting devices...'
```

For reusable scripts, consider using:

```powershell
Write-Verbose
```

so detailed output can be enabled when needed.

---

# Part 17 — Review Efficiency

Review your script for unnecessary Graph calls.

Look for patterns like:

```powershell
foreach ($User in $Users) {

    Get-MgUser ...
}
```

Ask:

```text
Can the information be retrieved once?

Can I use -All instead?

Can I use a server-side filter?

Can I request fewer properties?

Can I cache lookup information?
```

Graph automation should avoid unnecessary API traffic.

---

# Part 18 — Review Permissions

Create a permission inventory for the project.

Example:

```text
Resource             Permission
---------------------------------------------
Users                ________________________
Groups               ________________________
Licenses             ________________________
Devices              ________________________
Applications         ________________________
Service Principals   ________________________
Directory Roles      ________________________
```

Research commands using:

```powershell
Find-MgGraphCommand
```

and permissions using:

```powershell
Find-MgGraphPermission
```

Do not request broad write permissions for a read-only audit.

---

# Part 19 — Validate Output

Open every generated CSV.

Verify:

```text
[ ] File exists
[ ] Headers are readable
[ ] Expected records exist
[ ] No unnecessary object formatting appears
[ ] No sensitive data is accidentally exposed
[ ] Timestamp is correct
[ ] Report can be opened in Excel
```

A script is not finished simply because it ran without an error.

The output must also be useful.

---

# Part 20 — Test Failure Scenarios

A reliable automation tool should fail predictably.

Test safe scenarios such as:

```text
Invalid output path
Missing Graph connection
Insufficient permission
Unexpected tenant
Missing certificate
Expired certificate
Graph request failure
```

Do not intentionally damage tenant resources to test error handling.

Record:

```text
Failure tested:
____________________________________

Expected behavior:
____________________________________

Actual behavior:
____________________________________

Improvement needed:
____________________________________
```

---

# Part 21 — Add a README for Your Tool

Create:

```text
Graph-Audit/README.md
```

Include:

```text
Tool name
Purpose
Requirements
Required modules
Permissions
Authentication method
Usage examples
Generated reports
Known limitations
Security considerations
Troubleshooting
```

Example usage:

```powershell
.\Graph-Audit.ps1 -All
```

---

# Part 22 — Final Project Structure

Your finished project might resemble:

```text
Graph-Audit/
│
├── Graph-Audit.ps1
├── README.md
│
├── Output/
│   ├── Users-YYYYMMDD-HHMMSS.csv
│   ├── Groups-YYYYMMDD-HHMMSS.csv
│   ├── Licenses-YYYYMMDD-HHMMSS.csv
│   ├── Devices-YYYYMMDD-HHMMSS.csv
│   ├── Applications-YYYYMMDD-HHMMSS.csv
│   ├── ServicePrincipals-YYYYMMDD-HHMMSS.csv
│   ├── DirectoryRoles-YYYYMMDD-HHMMSS.csv
│   └── Summary-YYYYMMDD-HHMMSS.csv
│
└── Logs/
    └── Graph-Audit-YYYYMMDD-HHMMSS.log
```

---

# 🌟 Optional Advanced Challenges

Once the base project works, choose one or more improvements.

## Challenge 1 — HTML Dashboard

Convert the summary into an HTML report using:

```powershell
ConvertTo-Html
```

Include:

```text
User count
Group count
Device count
License availability
Application count
Role assignment count
```

---

## Challenge 2 — Stale Device Report

Create a report identifying devices whose available sign-in information is older than a threshold you define.

Research the limitations of the property before treating it as authoritative.

---

## Challenge 3 — Unlicensed User Report

Create a report showing users without assigned licenses.

Research the Graph properties or commands required rather than guessing.

---

## Challenge 4 — Group Membership Report

Allow the administrator to provide a group ID and export its members.

Example design:

```powershell
.\Graph-Audit.ps1 `
    -GroupMembers `
    -GroupId '<group-id>'
```

---

## Challenge 5 — Certificate Expiration Monitoring

If using app-only authentication, check the local authentication certificate and warn when it approaches expiration.

Example:

```text
Certificate expires in fewer than 30 days
        ↓
Write warning
        ↓
Log warning
```

---

## Challenge 6 — Scheduled Automation

After the script is reliable, research an appropriate automation platform such as:

```text
Windows Task Scheduler
Azure Automation
Azure Functions
Other approved enterprise automation platform
```

Choose an authentication model appropriate to that platform.

---

# 🧪 Final Validation

Before considering the project complete:

```text
[ ] Script connects successfully
[ ] Correct tenant is verified
[ ] Permissions are documented
[ ] Least privilege is used
[ ] Users report works
[ ] Groups report works
[ ] License report works
[ ] Device report works
[ ] Application report works
[ ] Service principal report works
[ ] Directory role report works
[ ] Summary report works
[ ] CSV output is readable
[ ] Errors are handled
[ ] Activity is logged
[ ] Graph disconnects cleanly
[ ] No credentials are hard-coded
[ ] No secrets are committed
[ ] README is complete
[ ] Failure scenarios were tested safely
```

---

# 📝 Capstone Reflection

Answer these after completing the project.

## 1. Which part of Microsoft Graph PowerShell was easiest for you?

```text
____________________________________________________

____________________________________________________
```

## 2. Which part was most difficult?

```text
____________________________________________________

____________________________________________________
```

## 3. Which report would be most useful in a real IT environment?

```text
____________________________________________________

____________________________________________________
```

## 4. What would you add to version 2 of the tool?

```text
____________________________________________________

____________________________________________________
```

## 5. Which permissions did your final tool require?

```text
____________________________________________________

____________________________________________________
```

## 6. How did you protect authentication credentials?

```text
____________________________________________________

____________________________________________________
```

## 7. What did you do to make the script reliable?

```text
____________________________________________________

____________________________________________________
```

---

# 🏆 Capstone Complete

You have built a Microsoft Graph PowerShell administration and reporting tool that combines concepts from across the course.

More importantly, you have practiced the workflow used to solve new Microsoft Graph problems:

```text
Understand the requirement
        ↓
Find the resource
        ↓
Find the command
        ↓
Find the permission
        ↓
Authenticate safely
        ↓
Retrieve the data
        ↓
Process the objects
        ↓
Export useful information
        ↓
Handle failures
        ↓
Automate responsibly
```

---

# 🎓 Course Complete!

Congratulations — you have completed the **Microsoft Graph PowerShell Fundamentals** training course.

You progressed from learning how Microsoft Graph PowerShell works to building a complete administration and automation project.

Throughout the course, you practiced:

- Microsoft Graph authentication
- Permissions and scopes
- Command discovery
- User administration
- Groups and membership
- Microsoft 365 licensing
- Microsoft Entra device inventory
- Applications and service principals
- Directory roles
- Microsoft Teams
- SharePoint and OneDrive
- Advanced queries and pagination
- Error handling
- Reliable automation
- App-only authentication

---

# 🚀 Where to Go Next

Continue developing your skills by building tools that solve real administrative problems.

Ideas include:

- Automated user audit reports
- License utilization reports
- Device inventory reports
- Group membership audits
- Directory role audits
- Application and service principal inventories
- Microsoft 365 administration dashboards
- Scheduled Graph reports
- Joiner, mover, and leaver reporting
- Security and configuration audits

When you encounter a new Graph task, do not worry about memorizing the exact cmdlet.

Use the discovery process you practiced throughout this course.

---

# 📚 Course Resources

➡️ **[Microsoft Graph PowerShell Cheat Sheet](../CheatSheet/cheatsheet.md)**

➡️ **[Microsoft Graph PowerShell Resources](../resources/resources.md)**

➡️ **[Return to Course Home](../README.md)**

---

# 🎯 Final Reminder

The goal was never to memorize every Microsoft Graph command.

The goal was to learn how to:

```text
Find the command
      ↓
Understand the object
      ↓
Determine the permission
      ↓
Connect safely
      ↓
Retrieve the data
      ↓
Process the results
      ↓
Automate the task
      ↓
Troubleshoot
      ↓
Improve
```

You now have a foundation for building real-world Microsoft Graph PowerShell administration and automation tools.
