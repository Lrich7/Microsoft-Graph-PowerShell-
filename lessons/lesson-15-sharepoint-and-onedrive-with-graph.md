# Lesson 15 --- SharePoint and OneDrive with Graph

## Learning Objectives

By the end of this lesson, you will be able to:

-   Explain the Graph concepts of sites, drives, and drive items.
-   Discover SharePoint sites through Microsoft Graph.
-   Retrieve drives associated with a site.
-   Understand how OneDrive and document libraries map to drive
    resources.
-   Retrieve file and folder metadata in a read-only manner.
-   Build a basic SharePoint/OneDrive inventory.
-   Explain why file-content and permission operations require
    additional care.

------------------------------------------------------------------------

# Graph Storage Concepts

Microsoft Graph represents SharePoint and OneDrive content using several
important resources:

``` text
Site
Drive
DriveItem
```

A useful mental model is:

``` text
SharePoint site
      ↓
Drive / document library
      ↓
DriveItem
      ↓
File or folder
```

OneDrive also uses the drive and driveItem resource model.

------------------------------------------------------------------------

# Sites

A Graph `site` represents a SharePoint site.

Discover commands:

``` powershell
Get-Command '*MgSite*'
```

A common command is:

``` powershell
Get-MgSite
```

Use `Get-Help` and `Find-MgGraphCommand` to determine supported syntax
and permissions for the query you need.

------------------------------------------------------------------------

# Drives

A SharePoint site can contain drives representing document libraries.

For a known site, Graph provides commands to retrieve drives.

Discover:

``` powershell
Get-Command '*MgSiteDrive*'
```

A drive can expose information such as:

``` text
Id
Name
DriveType
WebUrl
```

------------------------------------------------------------------------

# Drive Items

Files and folders are represented as drive items.

A drive item's metadata can include:

``` text
Id
Name
Size
WebUrl
CreatedDateTime
LastModifiedDateTime
File
Folder
```

This lets you build inventories without downloading file content.

------------------------------------------------------------------------

# OneDrive

A user's OneDrive is also represented as a drive.

Graph can work with OneDrive files and folders using the same general
drive/driveItem concepts.

The exact command path depends on whether you are starting from:

``` text
User
Site
Drive
Drive item
```

------------------------------------------------------------------------

# Metadata vs. Content

There is an important difference between:

``` text
Reading file metadata
Downloading file content
Changing file content
Changing permissions
Deleting files
```

These operations have different risk and permission requirements.

This lesson and lab focus on metadata inventory.

------------------------------------------------------------------------

# Site and File Permissions

SharePoint and OneDrive data can be highly sensitive.

Do not request broad file permissions simply to make a training command
work.

Research whether the task requires:

``` text
Site metadata
File metadata
File content
Write access
```

and choose permissions accordingly.

------------------------------------------------------------------------

# Inventory Ideas

Useful read-only reports include:

``` text
Sites
Document libraries
File/folder counts
Large files
Recently modified files
Library names and URLs
```

Large-scale file inventories can generate many API calls, so production
scripts should be designed carefully.

------------------------------------------------------------------------

# Graph vs. SharePoint-Specific Tools

Microsoft Graph is useful for many SharePoint and OneDrive scenarios.

Other SharePoint tooling may be more appropriate for some administrative
tasks.

Choose the tool based on the supported operation.

------------------------------------------------------------------------

# Common Beginner Mistakes

## Confusing Site, Drive, and DriveItem

Understand the hierarchy.

## Requesting File Content When Metadata Is Enough

Use the least access required.

## Recursing Through Huge Libraries Without Planning

Large inventories can generate significant request volume.

## Assuming OneDrive Uses a Completely Different Model

Graph uses the drive/driveItem model for OneDrive content too.

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

[Lab 15 --- SharePoint and OneDrive with
Graph](../labs/lesson-15-lab-15-sharepoint-and-onedrive-with-graph.md)

------------------------------------------------------------------------

## Additional Resources

-   [Microsoft Graph site
    resource](https://learn.microsoft.com/graph/api/resources/site)
-   [Microsoft Graph drive
    resource](https://learn.microsoft.com/graph/api/resources/drive)
-   [Microsoft Graph driveItem
    resource](https://learn.microsoft.com/graph/api/resources/driveitem)
