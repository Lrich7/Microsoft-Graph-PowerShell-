# Lab 10 --- Devices in Microsoft Entra ID

## Lab Objective

Build a read-only Microsoft Entra device inventory. Use only a tenant
you are authorized to query.

------------------------------------------------------------------------

# Exercise 1 --- Discover the Command

``` powershell
Get-Command Get-MgDevice
Get-Help Get-MgDevice -Examples
Find-MgGraphCommand -Command Get-MgDevice
```

Record an appropriate read permission for your scenario:

``` text
________________________________________
```

------------------------------------------------------------------------

# Exercise 2 --- Retrieve a Sample

After an authorized connection:

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

# Exercise 3 --- Inspect a Device

``` powershell
$device = Get-MgDevice -Top 1
$device | Get-Member
```

Explain the difference between `Id` and `DeviceId`:

``` text
____________________________________________________
```

------------------------------------------------------------------------

# Exercise 4 --- Filter Windows Devices

Store an authorized device collection in `$devices`.

Use PowerShell to return only Windows devices:

``` powershell
# Your solution
```

Then sort by display name.

------------------------------------------------------------------------

# Exercise 5 --- Find Disabled Device Objects

Use:

``` powershell
# Your solution using AccountEnabled
```

Do not enable, disable, or delete devices in this lab.

------------------------------------------------------------------------

# Exercise 6 --- Registered Owner Discovery

Find commands related to device registered owners:

``` powershell
Get-Command '*MgDevice*RegisteredOwner*'
```

Use Help on the command you find.

------------------------------------------------------------------------

# Exercise 7 --- Export Inventory

Create a CSV with:

``` text
DisplayName
DeviceId
AccountEnabled
OperatingSystem
OperatingSystemVersion
TrustType
ApproximateLastSignInDateTime
```

------------------------------------------------------------------------

# Knowledge Check

1.  Which cmdlet retrieves Entra device objects?\
    A. `Get-MgDevice`\
    B. `Get-MgComputer`\
    C. `Get-Device`\
    D. `Get-MgUser`

2.  Are `Id` and `DeviceId` necessarily the same value?\
    A. No\
    B. Yes

3.  Is an Entra device object identical to an Intune managed-device
    object?\
    A. No\
    B. Yes

------------------------------------------------------------------------

# Lab Complete

Continue to:

[Lesson 11 --- Applications and Service
Principals](../lessons/lesson-11-applications-and-service-principals.md)
