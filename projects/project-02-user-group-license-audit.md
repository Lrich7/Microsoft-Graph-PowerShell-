# Project 02 --- User, Group, and License Audit

## Lessons Used

This project reinforces approximately Lessons **06--09**:

``` text
Working with users
Managing-user safety
Groups and membership
Microsoft 365 licensing
```

------------------------------------------------------------------------

# Project Goal

Build a read-only audit script that creates useful Microsoft 365
identity reports.

The script should produce separate CSV reports for:

``` text
Users
Groups
License inventory
```

Optional advanced output can include selected group membership.

------------------------------------------------------------------------

# User Report

Include useful properties such as:

``` text
DisplayName
UserPrincipalName
Department
AccountEnabled
```

Identify:

``` text
Disabled accounts
Blank departments
```

------------------------------------------------------------------------

# Group Report

Include:

``` text
Id
DisplayName
Mail
MailEnabled
SecurityEnabled
GroupTypes
```

Optional:

``` text
Member count
```

Be aware that member counts may require additional requests.

------------------------------------------------------------------------

# License Report

Include:

``` text
SkuPartNumber
SkuId
Enabled
Consumed
Available
```

Flag low-availability SKUs.

For example:

``` text
Available < 10
```

Make the threshold configurable.

------------------------------------------------------------------------

# Requirements

Your script should:

1.  Verify Graph context.
2.  Use read-only permissions.
3.  Retrieve required user properties.
4.  Retrieve groups.
5.  Retrieve subscribed SKUs.
6.  Calculate available license units.
7.  Export separate CSV files.
8.  Create an execution summary.

------------------------------------------------------------------------

# Suggested Folder Output

``` text
Graph-Audit/
│
├── users.csv
├── groups.csv
├── licenses.csv
└── audit-summary.txt
```

------------------------------------------------------------------------

# Challenge Tasks

Add:

-   Timestamped output folders.
-   Counts of enabled/disabled users.
-   Counts of groups by type.
-   A list of users missing departments.
-   A low-license warning.
-   Error handling and logging.

------------------------------------------------------------------------

# Safety Rules

This project should not:

``` text
Create users
Modify users
Delete users
Change group membership
Assign licenses
Remove licenses
```

It is an audit project.

------------------------------------------------------------------------

# Completion Checklist

``` text
[ ] User report created
[ ] Group report created
[ ] License report created
[ ] License availability calculated
[ ] Missing user data identified
[ ] Graph context verified
[ ] Read-only permissions used
[ ] No secrets committed
```

------------------------------------------------------------------------

# What You Practiced

This project combines the most common Microsoft 365 identity inventory
tasks into one useful IT audit.
