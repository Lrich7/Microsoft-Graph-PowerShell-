# Lesson 01 --- Introduction to Microsoft Graph PowerShell

## Learning Objectives

By the end of this lesson, you will be able to:

-   Explain what Microsoft Graph is.
-   Explain what the Microsoft Graph PowerShell SDK does.
-   Describe the relationship between Microsoft Graph, Microsoft Entra
    ID, and Microsoft 365.
-   Recognize common Microsoft Graph PowerShell command naming.
-   Explain why permissions are central to Graph administration.
-   Understand the difference between read and write operations.
-   Identify safe first-use scenarios for Microsoft Graph PowerShell.

------------------------------------------------------------------------

# What Is Microsoft Graph?

Microsoft Graph is an API platform for accessing data and services
across the Microsoft cloud.

It provides a common way to work with resources such as:

``` text
Users
Groups
Devices
Applications
Microsoft Teams
SharePoint
OneDrive
Outlook
Microsoft 365
Microsoft Entra ID
```

Instead of every Microsoft cloud service requiring a completely separate
automation approach, Microsoft Graph provides a unified API surface for
many Microsoft services.

------------------------------------------------------------------------

# What Is the Microsoft Graph PowerShell SDK?

The Microsoft Graph PowerShell SDK provides PowerShell cmdlets that
interact with Microsoft Graph.

For example, a Microsoft Graph API request for users can be represented
by a PowerShell command such as:

``` powershell
Get-MgUser
```

The `Mg` in Graph PowerShell cmdlets identifies Microsoft Graph.

Other examples include:

``` powershell
Get-MgGroup
Get-MgDevice
Get-MgApplication
```

Later in the course you will learn how to discover commands rather than
memorize them.

------------------------------------------------------------------------

# Why Use PowerShell with Microsoft Graph?

PowerShell is useful when administrative work needs to be:

``` text
Repeated
Filtered
Reported
Performed in bulk
Documented
Automated
```

For example, instead of manually reviewing users one at a time in an
admin portal, PowerShell can retrieve user objects and build a report.

A simplified example is:

``` powershell
Get-MgUser -All |
    Select-Object DisplayName, UserPrincipalName
```

Do not worry about running this command yet. Authentication and
permissions come first.

------------------------------------------------------------------------

# Microsoft Graph and Microsoft Entra ID

Microsoft Entra ID contains identity and directory resources such as:

``` text
Users
Groups
Devices
Applications
Service principals
Directory roles
```

Many of these resources can be accessed through Microsoft Graph.

This means Microsoft Graph PowerShell is an important administration and
automation tool for Microsoft Entra environments.

------------------------------------------------------------------------

# Microsoft Graph and Microsoft 365

Microsoft Graph reaches beyond identity.

Depending on the API and permissions, Graph can work with resources from
services such as:

``` text
Microsoft Teams
SharePoint
OneDrive
Outlook
Microsoft 365
```

Not every Microsoft 365 administrative task is performed through Graph
PowerShell. Specialized PowerShell modules, such as Exchange Online
PowerShell, are still important.

A good administrator learns which tool fits the task.

------------------------------------------------------------------------

# Graph PowerShell Is Object-Based

Microsoft Graph PowerShell returns PowerShell objects.

That means the PowerShell skills you already learned still apply:

``` powershell
Select-Object
Where-Object
Sort-Object
ForEach-Object
Get-Member
Export-Csv
```

Conceptually:

``` text
Microsoft Graph
      ↓
Graph PowerShell cmdlet
      ↓
PowerShell objects
      ↓
Filter / Sort / Select
      ↓
Report or action
```

------------------------------------------------------------------------

# Command Naming

Microsoft Graph PowerShell commands generally follow normal PowerShell
naming:

``` text
Verb-MgNoun
```

Examples:

``` powershell
Get-MgUser
Get-MgGroup
New-MgGroup
Update-MgUser
Remove-MgGroup
```

The verb matters.

Commands beginning with:

``` text
Get
```

normally retrieve information.

Commands beginning with:

``` text
New
Update
Remove
```

can change the environment.

------------------------------------------------------------------------

# Read Before Write

This course will begin with read-only administration.

A useful learning progression is:

``` text
Connect
   ↓
Verify
   ↓
Get
   ↓
Inspect
   ↓
Filter
   ↓
Report
   ↓
Only then consider changes
```

This is especially important in cloud administration because a single
command can affect organizational resources.

------------------------------------------------------------------------

# Authentication

Before Microsoft Graph returns protected organizational data, PowerShell
must authenticate.

The primary command is:

``` powershell
Connect-MgGraph
```

You will learn this in Lesson 03.

Authentication answers:

``` text
Who or what is connecting?
```

------------------------------------------------------------------------

# Authorization and Permissions

Authentication alone is not enough.

Microsoft Graph also needs to determine:

``` text
What is this connection allowed to do?
```

Graph permissions are a major part of the platform.

Examples of permission names include:

``` text
User.Read
User.Read.All
Group.Read.All
```

You will study permissions and scopes in Lesson 04.

------------------------------------------------------------------------

# Least Privilege

A core security principle is:

> Request only the permissions required for the task.

If a script only needs to read information, it should not request write
permissions without a valid reason.

For example:

``` text
Read-only report
        ↓
Request read permissions

Account-management automation
        ↓
May require write permissions
```

The second scenario carries more risk.

------------------------------------------------------------------------

# Delegated and App-Only Access

Microsoft Graph supports two major access models.

## Delegated Access

An interactive user signs in.

Conceptually:

``` text
Administrator
     ↓
PowerShell
     ↓
Microsoft Graph
```

The application acts on behalf of the signed-in user.

This is where we will begin.

## App-Only Access

An application authenticates without an interactive signed-in user.

Conceptually:

``` text
Automation
    ↓
Application identity
    ↓
Microsoft Graph
```

This is useful for unattended automation but requires additional
security planning.

It will be covered much later in the course.

------------------------------------------------------------------------

# Microsoft Graph v1.0 and Beta

Microsoft Graph has:

``` text
v1.0
beta
```

For training and production scripting, prefer the stable `v1.0`
functionality when it meets the requirement.

Beta functionality can change and should not automatically be treated as
production-ready.

------------------------------------------------------------------------

# Azure AD and MSOnline PowerShell

You may encounter older scripts using modules such as:

``` text
AzureAD
MSOnline
```

Microsoft Graph PowerShell is the modern Microsoft-recommended direction
for Microsoft Entra ID automation.

Do not assume an old script should simply be copied into a new
environment.

Understand what it does, what permissions it requires, and how its
commands map to modern tooling.

------------------------------------------------------------------------

# A Typical Graph PowerShell Workflow

A common administrative workflow will eventually look like:

``` text
Install required module
        ↓
Connect-MgGraph
        ↓
Verify context
        ↓
Run Get-Mg... commands
        ↓
Inspect objects
        ↓
Filter / Sort / Select
        ↓
Export or report
        ↓
Disconnect
```

You will build this workflow gradually.

------------------------------------------------------------------------

# Common Beginner Mistakes

## Running a Command Before Understanding Its Verb

Always distinguish:

``` text
Get
```

from:

``` text
New
Update
Remove
```

------------------------------------------------------------------------

## Requesting Too Many Permissions

Do not request broad permissions simply because they make examples
easier.

Use least privilege.

------------------------------------------------------------------------

## Connecting to the Wrong Tenant

Cloud administrators may have access to more than one tenant.

Later you will use:

``` powershell
Get-MgContext
```

to verify your current connection.

------------------------------------------------------------------------

## Treating Graph PowerShell Like Plain Text

Graph commands return objects.

Use PowerShell's object tools instead of trying to parse screen output.

------------------------------------------------------------------------

# Key Takeaways

-   Microsoft Graph provides access to many Microsoft cloud resources.
-   Microsoft Graph PowerShell wraps Graph APIs in PowerShell cmdlets.
-   Graph PowerShell commands commonly use the `Mg` prefix.
-   Graph works with PowerShell objects.
-   Authentication identifies who or what is connecting.
-   Permissions determine what the connection can do.
-   Least privilege is essential.
-   Begin with read-only operations.
-   Delegated access uses a signed-in user.
-   App-only access is designed for unattended scenarios.
-   Prefer stable v1.0 functionality when possible.
-   Microsoft Graph PowerShell is the modern replacement direction for
    Azure AD and MSOnline PowerShell scenarios.

------------------------------------------------------------------------

# Lab

Continue to:

[Lab 01 --- Introduction to Microsoft
Graph](../labs/lesson-01-lab-01-introduction-to-microsoft-graph.md)

------------------------------------------------------------------------

## Additional Resources

-   [Microsoft Graph PowerShell
    overview](https://learn.microsoft.com/powershell/microsoftgraph/overview)
-   [Microsoft Graph PowerShell
    documentation](https://learn.microsoft.com/powershell/microsoftgraph/)
-   [Microsoft Graph permissions
    overview](https://learn.microsoft.com/graph/permissions-overview)
