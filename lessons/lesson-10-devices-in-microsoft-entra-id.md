# Lesson 10 --- Devices in Microsoft Entra ID

## Learning Objectives

By the end of this lesson, you will be able to:

-   Explain what a Microsoft Entra device object represents.
-   Retrieve device objects with `Get-MgDevice`.
-   Request and inspect useful device properties.
-   Filter and sort device inventory data.
-   Understand registered owners as a separate relationship.
-   Distinguish Entra device information from full Intune
    device-management data.
-   Build a read-only device inventory.

------------------------------------------------------------------------

# Device Objects

Microsoft Entra ID can contain device objects representing devices
registered or joined with the organization.

A Graph device object can contain information such as:

``` text
Id
DeviceId
DisplayName
AccountEnabled
OperatingSystem
OperatingSystemVersion
TrustType
ApproximateLastSignInDateTime
```

The exact properties available and returned depend on the API and query.

------------------------------------------------------------------------

# Retrieve Devices

Use:

``` powershell
Get-MgDevice
```

Retrieve a small sample:

``` powershell
Get-MgDevice -Top 10
```

Retrieve all result pages when required:

``` powershell
Get-MgDevice -All
```

------------------------------------------------------------------------

# Request Useful Properties

As with users, request the properties needed by your report.

Example:

``` powershell
Get-MgDevice -Top 10 `
    -Property Id,DeviceId,DisplayName,AccountEnabled,OperatingSystem,OperatingSystemVersion,TrustType,ApproximateLastSignInDateTime |
    Select-Object DisplayName,
                  DeviceId,
                  AccountEnabled,
                  OperatingSystem,
                  OperatingSystemVersion,
                  TrustType,
                  ApproximateLastSignInDateTime
```

------------------------------------------------------------------------

# Id vs. DeviceId

You may encounter both:

``` text
Id
DeviceId
```

`Id` identifies the directory object in Microsoft Graph.

`DeviceId` is the device identifier associated with the registered
device.

Do not assume they are interchangeable.

------------------------------------------------------------------------

# Filter Device Data

Standard PowerShell filtering works with returned objects.

Example:

``` powershell
$devices |
    Where-Object OperatingSystem -eq 'Windows'
```

Sort:

``` powershell
$devices |
    Sort-Object DisplayName
```

------------------------------------------------------------------------

# Registered Owners

A device's owner is represented through a relationship rather than
simply assuming that the display name tells you who uses it.

Graph provides commands for retrieving registered owners.

Discover them:

``` powershell
Get-Command '*MgDevice*RegisteredOwner*'
```

Then use `Get-Help` and `Find-MgGraphCommand` before querying your
environment.

------------------------------------------------------------------------

# Entra Devices vs. Intune Managed Devices

Do not assume a Microsoft Entra device object contains every piece of
endpoint-management information.

Conceptually:

``` text
Microsoft Entra device
        ↓
Identity / directory representation

Intune managed device
        ↓
Endpoint-management information
```

There can be overlap, but they are not the same resource.

------------------------------------------------------------------------

# Useful IT Questions

A device inventory can help answer questions such as:

``` text
Which devices are registered?
Which devices are Windows devices?
Which device objects are disabled?
Which devices have older operating-system information?
Which devices have not shown recent activity?
```

Be cautious when interpreting activity timestamps. Understand what the
property represents before using it for cleanup decisions.

------------------------------------------------------------------------

# Device Cleanup

Finding an apparently old device is not enough reason to delete it.

Before removing device objects:

``` text
Verify the device
Verify ownership/use
Check organizational lifecycle policy
Check management systems
Confirm authorization
Understand downstream impact
```

This lesson remains read-only.

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

[Lab 10 --- Devices in Microsoft Entra
ID](../labs/lesson-10-lab-10-devices-in-microsoft-entra-id.md)

------------------------------------------------------------------------

## Additional Resources

-   [Get-MgDevice](https://learn.microsoft.com/powershell/module/microsoft.graph.identity.directorymanagement/get-mgdevice)
-   [Microsoft Graph device
    resource](https://learn.microsoft.com/graph/api/resources/device)
