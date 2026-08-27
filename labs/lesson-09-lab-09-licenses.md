# Lab 09 --- Microsoft 365 Licenses with Microsoft Graph

## Lab Objective

Create a read-only Microsoft 365 license inventory and plan safe
license-management workflows.

------------------------------------------------------------------------

# Exercise 1 --- Discover Commands

Run:

``` powershell
Get-Command Get-MgSubscribedSku
Get-Command Get-MgUserLicenseDetail
Get-Command Set-MgUserLicense
```

Then:

``` powershell
Find-MgGraphCommand -Command Get-MgSubscribedSku
Find-MgGraphCommand -Command Get-MgUserLicenseDetail
Find-MgGraphCommand -Command Set-MgUserLicense
```

Which command is the write operation?

``` text
________________________________________
```

------------------------------------------------------------------------

# Exercise 2 --- Retrieve Tenant SKUs

With an authorized read connection:

``` powershell
Get-MgSubscribedSku |
    Select-Object SkuPartNumber,
                  SkuId,
                  ConsumedUnits
```

How many SKUs are returned?

``` text
________________________________________
```

------------------------------------------------------------------------

# Exercise 3 --- Inspect a SKU

Run:

``` powershell
$sku = Get-MgSubscribedSku |
    Select-Object -First 1
```

Then:

``` powershell
$sku | Get-Member
```

Inspect:

``` powershell
$sku.PrepaidUnits
```

and:

``` powershell
$sku.ServicePlans
```

------------------------------------------------------------------------

# Exercise 4 --- Calculate Available Units

Use:

``` text
Enabled - Consumed = Available
```

Create an object containing:

``` text
SkuPartNumber
Enabled
Consumed
Available
```

``` powershell
# Your solution here
```

------------------------------------------------------------------------

# Exercise 5 --- User License Detail

For an authorized user:

``` powershell
Get-MgUserLicenseDetail `
    -UserId '<authorized-user-upn>'
```

Do not place real organizational identifiers into a public training
repository.

------------------------------------------------------------------------

# Exercise 6 --- Export the Inventory

Export a license report to:

``` text
license-inventory.csv
```

Sort it by SKU part number.

``` powershell
# Your solution here
```

------------------------------------------------------------------------

# Exercise 7 --- Plan a License Assignment

Scenario:

> An approved employee needs a Microsoft 365 license.

Complete:

``` text
1. Verify __________________________________

2. Verify __________________________________

3. Verify __________________________________

4. Verify __________________________________

5. Preview _________________________________

6. Receive _________________________________

7. Change and ______________________________
```

Do not perform the change merely for this exercise.

------------------------------------------------------------------------

# Exercise 8 --- Group-Based Licensing

Why should you determine whether your organization uses group-based
licensing before scripting direct license assignments?

``` text
____________________________________________________

____________________________________________________
```

------------------------------------------------------------------------

# Offline Practice Option

If you cannot access a tenant:

``` powershell
$licenses = @(
    [pscustomobject]@{
        SkuPartNumber='TRAINING_A'
        Enabled=100
        Consumed=72
    }
    [pscustomobject]@{
        SkuPartNumber='TRAINING_B'
        Enabled=50
        Consumed=49
    }
)
```

Calculate an `Available` value.

Then identify SKUs with fewer than 10 available licenses.

------------------------------------------------------------------------

# Knowledge Check

1.  Which command retrieves subscribed SKUs?

    A. `Get-MgSubscribedSku`\
    B. `Get-MgLicense`\
    C. `Get-MgProduct`\
    D. `Find-MgSku`

2.  Which command can change direct user license assignments?

    A. `Set-MgUserLicense`\
    B. `Get-MgSubscribedSku`\
    C. `Get-MgUser`\
    D. `Get-MgContext`

3.  Should a SKU GUID from another tenant be blindly hard-coded?

    A. No\
    B. Yes

4.  Is direct assignment the only licensing model you may encounter?

    A. No\
    B. Yes

------------------------------------------------------------------------

# Lab Complete

------------------------------------------------------------------------

# 🛠️ Project 02 — User, Group & License Audit

You have completed the Identity Administration section of the course.

Now apply the skills from Lessons 06–09 by completing Project 02.

➡️ **[Project 02 — User, Group & License Audit](../projects/project-02-user-group-license-audit.md)**

In this project, you will combine your Microsoft Graph PowerShell skills to audit users, groups, group membership, and Microsoft 365 licensing.

------------------------------------------------------------------------
**Continue to:**

[Lesson 10 --- Devices in Microsoft Entra
ID](../lessons/lesson-10-devices-in-microsoft-entra-id.md)
