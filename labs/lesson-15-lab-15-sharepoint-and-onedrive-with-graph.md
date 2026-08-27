# Lab 15 --- SharePoint and OneDrive with Graph

## Lab Objective

Practice Microsoft Graph site, drive, and drive-item discovery using
read-only metadata. Do not modify or delete SharePoint/OneDrive content.

------------------------------------------------------------------------

# Exercise 1 --- Discover Site Commands

Run:

``` powershell
Get-Command '*MgSite*' |
    Sort-Object Name
```

Find a command used to retrieve sites.

Use:

``` powershell
Get-Help <command> -Examples
Find-MgGraphCommand -Command <command>
```

Research an appropriate read permission.

------------------------------------------------------------------------

# Exercise 2 --- Understand the Hierarchy

Fill in:

``` text
SharePoint __________
        ↓
Document library / __________
        ↓
File or folder / __________
```

------------------------------------------------------------------------

# Exercise 3 --- Retrieve an Authorized Site

Using an authorized test or organizational site, use the Graph site
cmdlets and current Help documentation to retrieve its site object.

Store it:

``` powershell
$site = # Your command
```

Display useful non-sensitive metadata.

------------------------------------------------------------------------

# Exercise 4 --- Discover Site Drives

Run:

``` powershell
Get-Command '*MgSiteDrive*'
```

Use Help to retrieve drives/document libraries for your selected site.

Display:

``` text
Id
Name
DriveType
WebUrl
```

------------------------------------------------------------------------

# Exercise 5 --- Drive Item Discovery

Use command discovery to find the cmdlet for retrieving drive
items/children from a drive.

``` powershell
Get-Command '*MgDrive*' |
    Sort-Object Name
```

Retrieve a small authorized sample of file/folder metadata.

Do not download file contents.

------------------------------------------------------------------------

# Exercise 6 --- Identify Files and Folders

Inspect the returned objects with:

``` powershell
Get-Member
```

Determine which properties help distinguish:

``` text
File
Folder
```

------------------------------------------------------------------------

# Exercise 7 --- Build a Metadata Report

For a small sample, create an output containing:

``` text
Name
Size
WebUrl
CreatedDateTime
LastModifiedDateTime
Item type
```

Export the metadata to CSV.

Do not include file contents.

------------------------------------------------------------------------

# Exercise 8 --- Permission Planning

For each task, decide whether it requires only metadata access or
potentially more sensitive access:

  Task                          Metadata / Content / Write
  ----------------------------- ----------------------------
  List document-library names   
  List filenames                
  Download a file               
  Delete a file                 
  Change a file                 

------------------------------------------------------------------------

# Knowledge Check

1.  What represents a SharePoint site in Graph?\
    A. Site\
    B. SKU\
    C. Device\
    D. Role assignment

2.  What commonly represents a document library or OneDrive?\
    A. Drive\
    B. User\
    C. Application\
    D. Tenant

3.  What represents a file or folder?\
    A. DriveItem\
    B. RoleDefinition\
    C. ServicePrincipal\
    D. Group

4.  Should you request file-content access when metadata alone meets the
    requirement?\
    A. No\
    B. Yes

------------------------------------------------------------------------

# Lab Complete

Continue to:

[Lesson 16 --- Advanced Queries and
Pagination](../lessons/lesson-16-advanced-queries-and-pagination.md)
