# Project 05 --- Microsoft Graph Automation Capstone

## Lessons Used

This project reinforces **Lessons 01--18**, with special emphasis on:

``` text
Advanced queries
Pagination
Error handling
Logging
Least privilege
App-only authentication
Automation design
```

------------------------------------------------------------------------

# Project Goal

Build a production-style **read-only Microsoft Graph IT audit**.

The project should combine the strongest ideas from the course into one
maintainable script.

The script can run interactively first and should be designed so it
could later run unattended with an approved app-only identity.

------------------------------------------------------------------------

# Scenario

Your IT team wants a recurring Microsoft 365 environment report.

The report should summarize:

``` text
Users
Groups
License capacity
Devices
Applications/service principals
Directory role assignments
Teams
```

You do not need to retrieve every possible property.

Choose useful IT fields and document why you chose them.

------------------------------------------------------------------------

# Required Architecture

Use a structure similar to:

``` text
Configuration
      ↓
Authentication / context verification
      ↓
Input and permission validation
      ↓
Data collection
      ↓
Processing
      ↓
Report generation
      ↓
Logging
      ↓
Summary
      ↓
Cleanup
```

------------------------------------------------------------------------

# Requirement 1 --- Configuration

Avoid scattering configuration throughout the script.

Create a configuration section or object containing values such as:

``` text
Output path
Low-license threshold
Maximum test results
Expected tenant ID
Report date
```

Do not store secrets in the configuration file.

------------------------------------------------------------------------

# Requirement 2 --- Context Verification

Before collecting data:

``` powershell
Get-MgContext
```

Validate the expected tenant and authentication state.

If the context is wrong:

``` text
Stop safely
Log the problem
Do not continue
```

------------------------------------------------------------------------

# Requirement 3 --- Efficient Queries

Use lessons from advanced queries:

``` text
Request only needed properties
Use -Top during testing
Use -All only when required
Use server-side filtering where supported
Avoid repeated calls for static data
```

------------------------------------------------------------------------

# Requirement 4 --- User Report

Include useful fields such as:

``` text
DisplayName
UserPrincipalName
Department
AccountEnabled
```

Summarize:

``` text
Total users
Enabled users
Disabled users
Missing departments
```

------------------------------------------------------------------------

# Requirement 5 --- Group Report

Include:

``` text
DisplayName
MailEnabled
SecurityEnabled
GroupTypes
```

Optional:

``` text
Membership counts for a limited sample
```

------------------------------------------------------------------------

# Requirement 6 --- License Report

Include:

``` text
SkuPartNumber
Enabled
Consumed
Available
```

Flag SKUs below your configured availability threshold.

------------------------------------------------------------------------

# Requirement 7 --- Device Report

Include:

``` text
DisplayName
OperatingSystem
OperatingSystemVersion
AccountEnabled
ApproximateLastSignInDateTime
```

Flag records for review rather than automatically changing them.

------------------------------------------------------------------------

# Requirement 8 --- Application Report

Include application and service-principal inventory.

Do not output secrets.

Optional:

``` text
Credential expiration warnings
```

------------------------------------------------------------------------

# Requirement 9 --- Directory Role Report

Create a readable role-assignment report.

Resolve:

``` text
RoleDefinitionId
```

to:

``` text
Role display name
```

Do not modify assignments.

------------------------------------------------------------------------

# Requirement 10 --- Teams Report

Create a basic Teams inventory.

Keep relationship queries efficient.

Do not retrieve every member/channel for every Team unless your test
environment and requirement justify it.

------------------------------------------------------------------------

# Requirement 11 --- Error Handling

Use:

``` powershell
try
catch
finally
```

where appropriate.

Decide which failures should:

``` text
Stop the script
Log and continue
Retry
```

------------------------------------------------------------------------

# Requirement 12 --- Logging

Create a log containing:

``` text
Timestamp
Operation
Target/resource
Status
Message
```

Never log:

``` text
Access tokens
Client secrets
Private keys
Passwords
```

------------------------------------------------------------------------

# Requirement 13 --- Summary

At the end, display a readable summary such as:

``` text
MICROSOFT GRAPH IT AUDIT COMPLETE

Users: 120
Disabled users: 4
Groups: 35
License SKUs: 6
Low-capacity SKUs: 1
Devices: 94
Applications: 18
Service principals: 240
Role assignments: 12
Teams: 14

Reports:
C:\Reports\GraphAudit\2026-08-27
```

------------------------------------------------------------------------

# Requirement 14 --- Automation Design

Document how the script could later run unattended.

Include:

``` text
Application identity
Least-privileged application permissions
Credential or managed-identity strategy
Credential rotation if applicable
Schedule
Output destination
Ownership
Monitoring
Failure notification
```

You do not need to create a privileged production app merely to complete
the project.

------------------------------------------------------------------------

# Suggested Project Structure

``` text
graph-automation-capstone/
│
├── Invoke-GraphAudit.ps1
├── README.md
├── config.example.psd1
├── functions/
│   ├── Get-AuditUsers.ps1
│   ├── Get-AuditGroups.ps1
│   ├── Get-AuditLicenses.ps1
│   ├── Get-AuditDevices.ps1
│   ├── Get-AuditApplications.ps1
│   ├── Get-AuditRoles.ps1
│   └── Get-AuditTeams.ps1
└── output/
```

Do not put real secrets or production report data into a public
repository.

------------------------------------------------------------------------

# Challenge Tasks

Add one or more:

-   HTML executive summary.
-   CSV and JSON output.
-   Credential-expiration warnings.
-   Configurable report sections.
-   Transcript/log retention.
-   Retry logic for appropriate transient failures.
-   Runtime measurement.
-   A `-WhatIf`-style preview architecture for future write operations.
-   Pester tests for validation functions.
-   Scheduled execution in an approved automation platform.

------------------------------------------------------------------------

# Final Safety Review

Before calling the project complete:

``` text
[ ] No secrets in Git
[ ] No write permissions unless truly required
[ ] No destructive Graph commands
[ ] Tenant context validated
[ ] Inputs validated
[ ] Errors handled
[ ] Logs created
[ ] Reports use only required data
[ ] Query volume considered
[ ] Ownership documented
[ ] Automation identity designed with least privilege
```

------------------------------------------------------------------------

# Capstone Complete

You have now built a Microsoft Graph PowerShell workflow that resembles
a real IT reporting and automation project rather than a collection of
isolated commands.

The next step is to customize the capstone for a controlled lab or your
organization's approved administrative requirements.
