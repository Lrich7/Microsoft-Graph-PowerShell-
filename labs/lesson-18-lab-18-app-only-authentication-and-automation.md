[lab-18-app-only-authentication-and-automation-remade.md](https://github.com/user-attachments/files/31532027/lab-18-app-only-authentication-and-automation-remade.md)
# Lab 18 — App-Only Authentication and Automation

## Lab Objective

Practice the concepts behind **app-only authentication** for Microsoft Graph PowerShell and prepare a safe structure for unattended automation.

By the end of this lab, you will be able to:

- Explain the difference between delegated and app-only authentication.
- Identify the Microsoft Entra objects involved in app-only authentication.
- Understand application permissions and admin consent.
- Recognize why certificates are preferred for many unattended automation scenarios.
- Connect to Microsoft Graph using a certificate-based app-only authentication pattern.
- Verify the Microsoft Graph authentication context.
- Build a reusable automation structure with validation, error handling, logging, and cleanup.
- Apply least-privilege principles to unattended Graph automation.

> **Important:** App-only authentication can provide broad access to Microsoft 365 data. Complete configuration exercises only in a tenant where you are authorized to create applications and grant permissions.

---

# Part 1 — Review Authentication Types

Microsoft Graph PowerShell commonly uses two authentication models.

## Delegated Authentication

A user signs in interactively.

Example:

```powershell
Connect-MgGraph -Scopes 'User.Read.All'
```

Conceptually:

```text
User
  ↓
Interactive Sign-In
  ↓
Delegated Permissions
  ↓
Microsoft Graph
```

## App-Only Authentication

An application authenticates without an interactive user session.

Conceptually:

```text
Application
     ↓
Credential / Certificate
     ↓
Application Permissions
     ↓
Microsoft Graph
```

Complete:

```text
Delegated authentication normally has a signed-in user:
Yes / No

App-only authentication is useful for unattended automation:
Yes / No
```

---

# Part 2 — Identify the Components

A typical certificate-based app-only configuration involves:

```text
Microsoft Entra Tenant
        ↓
App Registration
        ↓
Application / Client ID
        ↓
Service Principal
        ↓
Application Permissions
        ↓
Admin Consent
        ↓
Certificate
        ↓
PowerShell Automation
```

Write a short description of each item.

```text
Tenant ID:
____________________________________________________

Application / Client ID:
____________________________________________________

Service Principal:
____________________________________________________

Application Permission:
____________________________________________________

Admin Consent:
____________________________________________________

Certificate:
____________________________________________________
```

---

# Part 3 — Delegated vs. Application Permissions

Review the difference:

```text
Delegated Permission
    Used with a signed-in user

Application Permission
    Used by an application without a signed-in user
```

Answer:

```text
Which permission type is normally used for unattended app-only automation?

____________________________________________________
```

Why should app-only permissions be kept as narrow as possible?

```text
____________________________________________________

____________________________________________________
```

---

# Part 4 — Plan a Safe Automation Scenario

Imagine that you need a scheduled script that creates a daily report of Microsoft Entra users.

The script only needs to:

```text
Read users
Create a local CSV report
Exit
```

It does **not** need to:

```text
Create users
Delete users
Change passwords
Modify groups
Assign licenses
Modify directory roles
```

Before configuring the application, answer:

```text
Does this script require write permissions?
Yes / No

Should you request Directory.ReadWrite.All just because it would work?
Yes / No

Why?

____________________________________________________
```

The goal is to select the **least-privileged application permission** that supports the required operation.

---

# Part 5 — Discover Permissions

Microsoft Graph PowerShell can help you research permissions.

Run:

```powershell
Find-MgGraphCommand -Command Get-MgUser
```

Then inspect permission information:

```powershell
Find-MgGraphCommand -Command Get-MgUser |
    Select-Object -First 1 -ExpandProperty Permissions
```

You can also search:

```powershell
Find-MgGraphPermission 'User.Read.All'
```

Record:

```text
Permission researched:
____________________________________

Delegated available?
____________________________________

Application available?
____________________________________

Admin consent required?
____________________________________
```

> Always verify current permission requirements in Microsoft documentation before configuring production automation.

---

# Part 6 — App Registration

If you have permission to create applications in your training or administrative tenant, open the Microsoft Entra admin center:

https://entra.microsoft.com/

Navigate to:

```text
Identity
   ↓
Applications
   ↓
App registrations
```

Create or identify a test application for this lab.

Record:

```text
Application Name:
____________________________________

Application (Client) ID:
____________________________________

Directory (Tenant) ID:
____________________________________
```

> Do not publish real tenant identifiers from an organizational environment in a public GitHub repository.

If you are not authorized to create an app registration, review the steps conceptually and continue with the remaining read-only exercises.

---

# Part 7 — Review the Service Principal

An app registration and a service principal are related, but they are not the same object.

Conceptually:

```text
Application Object
        ↓
Defines the application

Service Principal
        ↓
Represents the application in a tenant
```

If connected with appropriate read permissions, discover service principal commands:

```powershell
Get-Command '*MgServicePrincipal*'
```

If authorized, locate the service principal associated with your test application.

Record:

```text
Service Principal Display Name:
____________________________________

Service Principal Object ID:
____________________________________
```

---

# Part 8 — Configure Application Permissions

In the Microsoft Entra admin center, open the test app registration.

Navigate to:

```text
API permissions
     ↓
Add a permission
     ↓
Microsoft Graph
     ↓
Application permissions
```

For the training scenario, research the least-privileged permission needed to read the required user information.

Before granting anything, verify:

```text
[ ] The application is the correct app
[ ] The permission is required for the task
[ ] Application permission is actually necessary
[ ] No broader write permission is being requested
[ ] You are authorized to grant or request consent
```

> Application permissions often require administrator consent.

---

# Part 9 — Certificates

Certificates are commonly used to authenticate unattended Graph PowerShell automation without placing a reusable client secret directly in a script.

Conceptually:

```text
Private key
    stays protected

Public certificate
    associated with app registration

PowerShell
    proves possession of private key
```

Important rules:

```text
Never commit a private key to GitHub.
Never publish a certificate containing its private key.
Protect certificate stores and exported PFX files.
Track certificate expiration.
Plan certificate rotation.
```

---

# Part 10 — Review Certificates in PowerShell

On Windows, inspect certificates available to your user:

```powershell
Get-ChildItem Cert:\CurrentUser\My
```

Useful properties include:

```text
Subject
Thumbprint
NotBefore
NotAfter
HasPrivateKey
```

Create a clean view:

```powershell
Get-ChildItem Cert:\CurrentUser\My |
    Select-Object Subject,
        Thumbprint,
        NotBefore,
        NotAfter,
        HasPrivateKey
```

Do **not** paste a real private key into your lab notes.

---

# Part 11 — App-Only Connection Pattern

A certificate-based Graph PowerShell connection can follow this pattern:

```powershell
$TenantId = '<tenant-id>'
$ClientId = '<application-id>'
$Thumbprint = '<certificate-thumbprint>'

Connect-MgGraph `
    -TenantId $TenantId `
    -ClientId $ClientId `
    -CertificateThumbprint $Thumbprint
```

Do not paste real production values into this public training file.

If your test application and certificate are fully configured and you are authorized to use them, substitute your lab values locally.

---

# Part 12 — Verify the Context

After connecting, run:

```powershell
Get-MgContext
```

Or:

```powershell
$context = Get-MgContext

$context |
    Select-Object Account,
        TenantId,
        ClientId,
        AuthType,
        Scopes
```

Record:

```text
Tenant verified?
Yes / No

Client/Application verified?
Yes / No

Authentication type:
____________________________________
```

Never assume a successful connection means you connected to the intended tenant or application.

---

# Part 13 — Test a Read-Only Operation

If your application has the required permission and consent, test a small read-only request first.

Example:

```powershell
Get-MgUser -Top 5 |
    Select-Object DisplayName,
        UserPrincipalName
```

Use:

```powershell
-Top 5
```

while testing instead of immediately retrieving the entire directory.

Record:

```text
Request successful?
Yes / No

Number of results:
____________________________________
```

---

# Part 14 — Build a Basic Unattended Script

Create:

```text
graph-user-report.ps1
```

Start with:

```powershell
$TenantId = '<tenant-id>'
$ClientId = '<application-id>'
$Thumbprint = '<certificate-thumbprint>'

Connect-MgGraph `
    -TenantId $TenantId `
    -ClientId $ClientId `
    -CertificateThumbprint $Thumbprint

Get-MgUser -All `
    -Property DisplayName,
        UserPrincipalName,
        AccountEnabled |
    Select-Object DisplayName,
        UserPrincipalName,
        AccountEnabled |
    Export-Csv .\graph-users.csv `
        -NoTypeInformation

Disconnect-MgGraph
```

This demonstrates the basic automation flow:

```text
Authenticate
    ↓
Retrieve
    ↓
Process
    ↓
Export
    ↓
Disconnect
```

---

# Part 15 — Add Context Validation

Improve the script:

```powershell
$context = Get-MgContext

if ($null -eq $context) {
    throw 'Microsoft Graph connection was not established.'
}

if ($context.TenantId -ne $TenantId) {
    throw 'Connected to an unexpected Microsoft Graph tenant.'
}
```

Why is context validation useful for unattended automation?

```text
____________________________________________________

____________________________________________________
```

---

# Part 16 — Add Error Handling

Use:

```powershell
try {

    Connect-MgGraph `
        -TenantId $TenantId `
        -ClientId $ClientId `
        -CertificateThumbprint $Thumbprint `
        -ErrorAction Stop

    $context = Get-MgContext

    if ($null -eq $context) {
        throw 'Microsoft Graph connection was not established.'
    }

    if ($context.TenantId -ne $TenantId) {
        throw 'Connected to an unexpected tenant.'
    }

    $users = Get-MgUser `
        -All `
        -Property DisplayName,
            UserPrincipalName,
            AccountEnabled `
        -ErrorAction Stop

    $users |
        Select-Object DisplayName,
            UserPrincipalName,
            AccountEnabled |
        Export-Csv .\graph-users.csv `
            -NoTypeInformation
}
catch {
    Write-Error "Automation failed: $($_.Exception.Message)"
}
finally {
    Disconnect-MgGraph -ErrorAction SilentlyContinue
}
```

The structure is now:

```text
TRY
 ↓
Connect
 ↓
Validate
 ↓
Retrieve
 ↓
Export
 ↓
CATCH errors
 ↓
FINALLY disconnect
```

---

# Part 17 — Add Logging

Create a simple log path:

```powershell
$LogPath = '.\graph-automation.log'
```

Add:

```powershell
"$(Get-Date -Format s) - Automation started" |
    Add-Content $LogPath
```

After success:

```powershell
"$(Get-Date -Format s) - User report completed successfully" |
    Add-Content $LogPath
```

In the catch block:

```powershell
"$(Get-Date -Format s) - ERROR: $($_.Exception.Message)" |
    Add-Content $LogPath
```

In the finally block:

```powershell
"$(Get-Date -Format s) - Automation finished" |
    Add-Content $LogPath
```

A scheduled script should leave enough information behind to determine whether it ran successfully.

---

# Part 18 — Avoid Hard-Coded Secrets

Which of these should **never** be placed directly into a public script?

```text
[ ] Password
[ ] Client secret
[ ] Access token
[ ] Private key
[ ] UserPrincipalName
[ ] Display name
```

For automation credentials, prefer secure mechanisms appropriate to the environment.

Examples may include:

```text
Certificates
Managed identities where supported
Secure secret stores
Platform-managed credentials
```

---

# Part 19 — Certificate Expiration Check

Certificates expire.

Inspect expiration:

```powershell
Get-ChildItem Cert:\CurrentUser\My |
    Select-Object Subject,
        Thumbprint,
        NotAfter
```

Example warning logic:

```powershell
$WarningDate = (Get-Date).AddDays(30)

Get-ChildItem Cert:\CurrentUser\My |
    Where-Object {
        $_.NotAfter -le $WarningDate
    } |
    Select-Object Subject,
        Thumbprint,
        NotAfter
```

Why should certificate expiration be monitored?

```text
____________________________________________________

____________________________________________________
```

---

# Part 20 — Automation Design Exercise

Design an unattended Graph automation job.

Choose one:

```text
User inventory
License inventory
Device inventory
Group membership report
Application inventory
Directory role audit
```

Complete:

```text
Automation Purpose:
____________________________________________________

Graph Resource:
____________________________________________________

Graph Command(s):
____________________________________________________

Required Permission(s):
____________________________________________________

Delegated or Application:
____________________________________________________

Authentication Method:
____________________________________________________

Output:
____________________________________________________

Logging Method:
____________________________________________________

Failure Handling:
____________________________________________________

Schedule:
____________________________________________________
```

---

# Part 21 — Production Readiness Checklist

Before calling a Graph script production-ready, verify:

```text
[ ] Purpose is documented
[ ] Tenant is validated
[ ] Application ID is validated
[ ] Permissions use least privilege
[ ] Admin consent is documented
[ ] Certificate/private key is protected
[ ] Certificate expiration is monitored
[ ] No secrets are stored in source code
[ ] Errors are handled
[ ] Activity is logged
[ ] Output location is protected
[ ] Bulk operations are tested safely
[ ] Script disconnects cleanly
[ ] Ownership is documented
[ ] Recovery / rollback is considered for write operations
```

---

# Knowledge Check

## Question 1

Which permission type is normally used for app-only Microsoft Graph authentication?

A. Delegated  
B. Application  
C. Local administrator  
D. NTFS

## Question 2

Which command shows the current Microsoft Graph PowerShell context?

A. `Get-MgContext`  
B. `Get-MgUser`  
C. `Get-Module`  
D. `Get-Credential`

## Question 3

Why is least privilege especially important for app-only automation?

A. Applications may run unattended with persistent access  
B. It makes CSV files smaller  
C. It changes the tenant ID  
D. It disables PowerShell

## Question 4

Should a private certificate key be committed to GitHub?

A. Yes  
B. No

## Question 5

Which block is useful for cleanup such as disconnecting even when an error occurs?

A. `foreach`  
B. `switch`  
C. `finally`  
D. `Where-Object`

## Question 6

What should an unattended script verify after connecting?

A. Only the PowerShell window title  
B. Tenant and authentication context  
C. Desktop wallpaper  
D. File extension

## Question 7

Why should certificate expiration be monitored?

A. An expired authentication certificate can cause automation to fail  
B. It changes user licenses  
C. It creates new users  
D. It increases Graph pagination

---

# Challenge — Build a Reliable Graph Automation Template

Create:

```text
graph-automation-template.ps1
```

Your template should contain:

```text
Configuration variables
        ↓
Authentication
        ↓
Context validation
        ↓
Graph operation
        ↓
Data processing
        ↓
Export
        ↓
Logging
        ↓
Error handling
        ↓
Cleanup
```

Use placeholder values rather than committing real tenant credentials or secrets.

Your finished template should be reusable for future Graph automation projects.

---

# Lab Completion Checklist

- [ ] Reviewed delegated vs. app-only authentication
- [ ] Identified app-only authentication components
- [ ] Reviewed application permissions
- [ ] Practiced permission discovery
- [ ] Reviewed app registration concepts
- [ ] Reviewed service principal concepts
- [ ] Reviewed certificate authentication
- [ ] Inspected local certificates
- [ ] Reviewed the app-only connection pattern
- [ ] Verified Graph context
- [ ] Tested a read-only Graph request if authorized
- [ ] Built an unattended script structure
- [ ] Added context validation
- [ ] Added error handling
- [ ] Added logging
- [ ] Reviewed secret-handling rules
- [ ] Reviewed certificate expiration
- [ ] Completed the automation design exercise
- [ ] Completed the knowledge check
- [ ] Built the reusable automation template

---

# Lab Complete

You have completed **Lab 18 — App-Only Authentication and Automation**.

You have also completed all 18 lessons and labs in the Microsoft Graph PowerShell course.

Now bring the course together with the final capstone project.

---

# 🏆 Final Project — Microsoft Graph Automation Capstone

➡️ **[Project 05 — Microsoft Graph Automation Capstone](../projects/project-05-graph-automation-capstone.md)**

In the capstone, you will combine skills from across the course to build a practical Microsoft Graph PowerShell automation and reporting solution.

Use the same discovery and troubleshooting workflow you would use in a real administrative environment:

```text
Get-Command
      ↓
Get-Help
      ↓
Find-MgGraphCommand
      ↓
Find-MgGraphPermission
      ↓
Microsoft Learn
      ↓
Test
      ↓
Troubleshoot
      ↓
Improve
```

➡️ **[Begin Project 05 — Microsoft Graph Automation Capstone](../projects/project-05-graph-automation-capstone.md)**
