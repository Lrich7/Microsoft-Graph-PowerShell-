# Lesson 09 --- Microsoft 365 Licenses with Microsoft Graph

## Learning Objectives

By the end of this lesson, you will be able to:

-   Retrieve subscribed license SKUs.
-   Understand SKU IDs and SKU part numbers.
-   Inspect service plans.
-   Review a user's license details.
-   Calculate basic license availability.
-   Build a read-only license inventory.
-   Discover the command used for direct license changes.
-   Explain why license changes require careful validation.

------------------------------------------------------------------------

# Licensing with Microsoft Graph

Microsoft Graph can report on Microsoft 365 subscriptions and user
license assignments.

A safe learning order is:

``` text
Inventory tenant SKUs
       ↓
Inspect service plans
       ↓
Inspect user assignments
       ↓
Calculate availability
       ↓
Study license changes
```

------------------------------------------------------------------------

# Retrieve Subscribed SKUs

Use:

``` powershell
Get-MgSubscribedSku
```

Useful properties include:

``` text
SkuId
SkuPartNumber
ConsumedUnits
PrepaidUnits
ServicePlans
```

Inspect the object:

``` powershell
Get-MgSubscribedSku |
    Get-Member
```

------------------------------------------------------------------------

# SKU ID

`SkuId` is the GUID identifier associated with the subscribed product
SKU.

Example conceptually:

``` text
SkuId
xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

Do not copy a SKU GUID from another organization and assume it applies
to your tenant.

Retrieve the SKU from the tenant you are administering.

------------------------------------------------------------------------

# SKU Part Number

`SkuPartNumber` is generally easier for an administrator to recognize.

A license inventory should usually include both:

``` text
SkuPartNumber
SkuId
```

------------------------------------------------------------------------

# Service Plans

A Microsoft 365 license SKU can contain multiple service plans.

Inspect:

``` powershell
$sku = Get-MgSubscribedSku |
    Select-Object -First 1

$sku.ServicePlans
```

This helps explain why one product license can enable multiple Microsoft
services.

------------------------------------------------------------------------

# User License Details

For a specific authorized user:

``` powershell
Get-MgUserLicenseDetail `
    -UserId 'user@contoso.com'
```

This can show license and service-plan information associated with that
user.

------------------------------------------------------------------------

# Calculate Available Licenses

A useful inventory calculation is:

``` text
Enabled units
    -
Consumed units
    =
Available units
```

Inspect the actual `PrepaidUnits` object returned in your environment
before building the calculation.

Conceptually:

``` powershell
$sku.PrepaidUnits.Enabled - $sku.ConsumedUnits
```

------------------------------------------------------------------------

# Build a License Inventory

A useful report might contain:

``` text
SKU part number
SKU ID
Enabled
Consumed
Available
```

This is useful for capacity planning without making changes.

------------------------------------------------------------------------

# Changing User Licenses

The Graph PowerShell command used for direct user license assignment
changes is:

``` powershell
Set-MgUserLicense
```

It can add and remove direct license assignments.

This is a write operation.

Do not run it merely to experiment in a production tenant.

------------------------------------------------------------------------

# Before Assigning a License

Verify:

``` text
Correct tenant
Correct user
Correct SKU
Available capacity
Business requirement
Licensing model
Required Graph permission
Authorization to make the change
```

Then preview the intended action.

------------------------------------------------------------------------

# Before Removing a License

License removal can affect access to Microsoft services.

Treat it as a meaningful production change.

Understand what services depend on the license before removing it.

------------------------------------------------------------------------

# Group-Based Licensing

Organizations may assign licenses through Microsoft Entra groups.

This means direct assignment is not always the correct automation
approach.

Before building license-management automation, determine whether your
organization uses:

``` text
Direct licensing
Group-based licensing
A combination
```

------------------------------------------------------------------------

# Least Privilege

License reporting and license assignment are different tasks.

A report should use appropriate read permissions.

A license change requires appropriate write permissions.

Do not request broad directory write access simply because it is
convenient.

------------------------------------------------------------------------

# Common Beginner Mistakes

## Guessing the SKU

Retrieve current tenant SKUs.

## Treating License Removal as Harmless

It can affect service access.

## Ignoring Available Capacity

Check availability before assigning.

## Assuming Direct Assignment Is the Only Model

Group-based licensing may be in use.

## Using Write Permissions for Reporting

Use least privilege.

------------------------------------------------------------------------

# Key Takeaways

-   `Get-MgSubscribedSku` retrieves tenant subscription SKU information.
-   SKU IDs and SKU part numbers serve different purposes.
-   A SKU can contain multiple service plans.
-   `Get-MgUserLicenseDetail` retrieves license details for a user.
-   License availability can be calculated from enabled and consumed
    units.
-   `Set-MgUserLicense` changes direct user license assignments.
-   License changes should be validated and authorized.
-   Group-based licensing may change how automation should be designed.
-   Start with read-only license inventory and reporting.

------------------------------------------------------------------------

# Lab

Continue to:

[Lab 09 --- Microsoft 365 Licenses with Microsoft
Graph](../labs/lesson-09-lab-09-licenses.md)

------------------------------------------------------------------------

## Additional Resources

-   [View Microsoft 365 license and service details with
    PowerShell](https://learn.microsoft.com/microsoft-365/enterprise/view-account-license-and-service-details-with-microsoft-365-powershell)
-   [Set-MgUserLicense](https://learn.microsoft.com/powershell/module/microsoft.graph.users.actions/set-mguserlicense)
-   [Microsoft Graph subscribedSku
    resource](https://learn.microsoft.com/graph/api/resources/subscribedsku)
