# Project 04 --- Microsoft 365 Collaboration Audit

## Lessons Used

This project reinforces approximately Lessons **13--15**:

``` text
Microsoft 365 and Graph
Microsoft Teams
SharePoint and OneDrive
```

------------------------------------------------------------------------

# Project Goal

Build a read-only collaboration inventory that demonstrates how
Microsoft Graph can report across Microsoft 365 workloads.

Create reports for:

``` text
Teams
Team channels
SharePoint sites
Document libraries / drives
Selected file/folder metadata
```

------------------------------------------------------------------------

# Part 1 --- Teams

Create a Teams inventory containing useful values such as:

``` text
Team ID
DisplayName
Description
```

For a small authorized sample, add:

``` text
Channel count
Channel names
```

Optional:

``` text
Member count
Owner count
```

Remember that additional relationships can create many Graph requests.

------------------------------------------------------------------------

# Part 2 --- SharePoint Sites

Retrieve authorized site metadata.

Include:

``` text
Site ID
DisplayName
WebUrl
```

Use the supported Graph site commands for your environment.

------------------------------------------------------------------------

# Part 3 --- Document Libraries

For selected sites, retrieve drives/document libraries.

Include:

``` text
Site
Drive ID
Drive name
Drive type
WebUrl
```

------------------------------------------------------------------------

# Part 4 --- File Metadata

For one small test library, retrieve a limited sample of drive-item
metadata.

Include:

``` text
Name
Size
CreatedDateTime
LastModifiedDateTime
Item type
WebUrl
```

Do not download file contents.

------------------------------------------------------------------------

# Requirements

Your script should:

1.  Use read-only permissions.
2.  Verify Graph context.
3.  Limit test samples while developing.
4.  Inventory Teams.
5.  Inventory selected sites.
6.  Inventory drives.
7.  Retrieve only a small file-metadata sample.
8.  Export separate reports.
9.  Document which Graph calls may become expensive at scale.

------------------------------------------------------------------------

# Suggested Output

``` text
M365-Collaboration-Audit/
│
├── teams.csv
├── channels.csv
├── sites.csv
├── drives.csv
└── file-metadata-sample.csv
```

------------------------------------------------------------------------

# Challenge Tasks

Add:

-   A configurable maximum number of teams/sites.
-   Channel counts.
-   Drive counts.
-   Large-file identification.
-   Recently modified file metadata.
-   Error handling per workload.
-   A combined summary.

------------------------------------------------------------------------

# Safety Rules

Do not:

``` text
Change Teams membership
Delete channels
Modify SharePoint sites
Download sensitive files unnecessarily
Delete files
Change file permissions
```

------------------------------------------------------------------------

# Completion Checklist

``` text
[ ] Teams inventoried
[ ] Channels inventoried
[ ] Sites inventoried
[ ] Drives inventoried
[ ] File metadata sampled
[ ] No content modified
[ ] Query volume considered
[ ] Reports exported
```

------------------------------------------------------------------------

# What You Practiced

This project demonstrates how Graph can combine Microsoft 365
collaboration information into one reporting workflow.
