# Lesson 13 --- Microsoft 365 and Microsoft Graph

## Learning Objectives

By the end of this lesson, you will be able to:

-   Explain where Microsoft Graph fits into Microsoft 365
    administration.
-   Recognize when a workload-specific PowerShell module may still be
    the better tool.
-   Identify common Graph-accessible Microsoft 365 resources.
-   Understand that one administration workflow can use multiple
    PowerShell modules.
-   Plan a tool choice before writing automation.
-   Avoid assuming Microsoft Graph replaces every Microsoft 365
    administrative interface.

------------------------------------------------------------------------

# Microsoft Graph Is Broad, Not Universal

Microsoft Graph provides access to a large set of Microsoft 365 and
Microsoft Entra resources.

Examples include:

``` text
Users
Groups
Teams
SharePoint sites
OneDrive drives/files
Mail and calendars
Applications
Devices
Reports
```

However, Microsoft Graph PowerShell does not automatically replace every
workload-specific administrative module.

------------------------------------------------------------------------

# Workload-Specific PowerShell

Microsoft 365 administration may also use modules such as:

``` text
ExchangeOnlineManagement
MicrosoftTeams
PnP.PowerShell
```

The exact tool depends on the administrative task.

For example, some Exchange administrative configuration is best handled
with Exchange Online PowerShell rather than trying to force the task
through Graph.

------------------------------------------------------------------------

# Choose the Tool by Requirement

Start with:

``` text
What am I trying to administer?
```

Then ask:

``` text
Does Microsoft Graph expose the resource/action?
Is the Graph API suitable for this task?
Is there a supported workload-specific PowerShell cmdlet?
Which option is clearer and safer?
Which permissions/roles are required?
```

------------------------------------------------------------------------

# Graph Resource Examples

Graph is especially useful when a workflow crosses service boundaries.

Example:

``` text
Retrieve user
   ↓
Check group membership
   ↓
Review license information
   ↓
Review Teams membership
   ↓
Produce one report
```

A unified API can make cross-service reporting easier.

------------------------------------------------------------------------

# Exchange Example

Suppose your requirement is:

> Configure a mailbox-specific Exchange setting.

Do not assume that because the user exists in Graph, Graph is
automatically the correct management surface.

Research:

``` text
Microsoft Graph support
Exchange Online PowerShell support
Required permissions
Supported production approach
```

------------------------------------------------------------------------

# Teams Example

Microsoft Graph can access many Teams resources.

The Microsoft Teams PowerShell module also provides administrative
cmdlets.

The correct choice depends on the operation.

------------------------------------------------------------------------

# SharePoint Example

Microsoft Graph provides APIs for sites, drives, lists, and files.

SharePoint administration can also involve SharePoint-specific tools and
APIs.

Again:

> Choose the tool based on the supported administrative operation, not
> because one module is your favorite.

------------------------------------------------------------------------

# Multi-Module Scripts

A real Microsoft 365 administration script may use multiple modules.

Conceptually:

``` text
Microsoft.Graph
      +
ExchangeOnlineManagement
      +
MicrosoftTeams
      ↓
Administrative workflow
```

If you do this:

``` text
Document dependencies
Authenticate intentionally
Use least privilege
Handle errors per service
Disconnect sessions when finished
```

------------------------------------------------------------------------

# Reporting vs. Configuration

Graph is extremely useful for inventory and reporting.

Configuration support varies by resource and workload.

Always check current Microsoft documentation before designing production
automation.

------------------------------------------------------------------------

# Common Beginner Mistakes

## Assuming Graph Replaces Everything

It does not.

## Using Multiple Modules Without Documenting Them

Production scripts should clearly state dependencies.

## Assuming Permissions Transfer Between Modules

Each service and connection can have its own authorization model.

## Choosing a Tool Before Defining the Requirement

Start with the task.

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

[Lab 13 --- Microsoft 365 and Microsoft
Graph](../labs/lesson-13-lab-13-microsoft-365-and-microsoft-graph.md)

------------------------------------------------------------------------

## Additional Resources

-   [Microsoft Graph
    overview](https://learn.microsoft.com/graph/overview)
-   [Microsoft Graph PowerShell
    overview](https://learn.microsoft.com/powershell/microsoftgraph/overview)
-   [Exchange Online
    PowerShell](https://learn.microsoft.com/powershell/exchange/exchange-online-powershell)
