# Project 03 --- Microsoft Entra Security Inventory

## Lessons Used

This project reinforces approximately Lessons **10--12**:

``` text
Devices
Applications and service principals
Directory roles
```

------------------------------------------------------------------------

# Project Goal

Build a read-only Microsoft Entra security inventory.

The project should create reports for:

``` text
Devices
Application registrations
Service principals
Directory role definitions
Directory role assignments
```

------------------------------------------------------------------------

# Device Inventory

Include:

``` text
DisplayName
DeviceId
AccountEnabled
OperatingSystem
OperatingSystemVersion
TrustType
ApproximateLastSignInDateTime
```

Flag disabled device objects.

Optionally flag old activity dates for **review only**.

Do not automatically delete devices.

------------------------------------------------------------------------

# Application Inventory

Include:

``` text
DisplayName
AppId
Id
```

Optionally include non-secret credential-expiration metadata.

Never export credential secret values.

------------------------------------------------------------------------

# Service Principal Inventory

Include:

``` text
DisplayName
AppId
Id
ServicePrincipalType
AccountEnabled
```

------------------------------------------------------------------------

# Directory Role Inventory

Retrieve:

``` text
Role definitions
Role assignments
```

Resolve role-definition IDs into readable role names.

Your report should help answer:

``` text
Which roles are assigned?
Which principals have assignments?
Which roles appear highly privileged?
```

A complete PIM audit may require additional PIM-specific data and is
outside the minimum project.

------------------------------------------------------------------------

# Requirements

Your script should:

1.  Verify Graph context.
2.  Retrieve device inventory.
3.  Retrieve applications.
4.  Retrieve service principals.
5.  Retrieve directory role definitions.
6.  Retrieve role assignments.
7.  Join role IDs to readable names.
8.  Export reports.
9.  Log failures.

------------------------------------------------------------------------

# Suggested Output

``` text
Entra-Security-Inventory/
│
├── devices.csv
├── applications.csv
├── service-principals.csv
├── role-assignments.csv
└── execution-log.csv
```

------------------------------------------------------------------------

# Challenge Tasks

Add:

-   Credential-expiration warnings.
-   Disabled-device counts.
-   Disabled-service-principal counts.
-   A configurable list of high-impact roles to highlight.
-   HTML summary output.
-   A timestamped report folder.

------------------------------------------------------------------------

# Safety Rules

Do not:

``` text
Delete devices
Create secrets
Change app permissions
Disable service principals
Assign directory roles
Remove directory roles
```

This project is for inventory and review.

------------------------------------------------------------------------

# Completion Checklist

``` text
[ ] Device report created
[ ] Application report created
[ ] Service-principal report created
[ ] Role report created
[ ] Role names resolved
[ ] No secrets exported
[ ] No privileged changes performed
[ ] Errors logged
```

------------------------------------------------------------------------

# What You Practiced

This project turns Microsoft Graph into a practical Microsoft Entra
security-audit tool.
