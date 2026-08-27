# Lesson 02 --- Installing the Microsoft Graph PowerShell SDK

## Learning Objectives

By the end of this lesson, you will be able to:

-   Check your PowerShell version.
-   Explain why PowerShell 7 is recommended.
-   Find Microsoft Graph modules in the PowerShell Gallery.
-   Install the Microsoft Graph PowerShell SDK for the current user.
-   Explain the difference between the main SDK and individual
    submodules.
-   Verify an installation.
-   Update an installed Graph module.
-   Understand the difference between Microsoft.Graph and
    Microsoft.Graph.Beta.
-   Avoid unnecessary module installation.

------------------------------------------------------------------------

# Before Installing Anything

Start by identifying your PowerShell environment.

Run:

``` powershell
$PSVersionTable
```

A focused view is:

``` powershell
$PSVersionTable.PSVersion
```

Microsoft recommends PowerShell 7 or later for the Microsoft Graph
PowerShell SDK.

Windows PowerShell 5.1 can also be used when its required prerequisites
are satisfied, but this course will favor modern PowerShell 7 examples.

------------------------------------------------------------------------

# Check Whether Graph Is Already Installed

Before installing a module, check first.

``` powershell
Get-Module Microsoft.Graph* -ListAvailable
```

This searches module locations for Graph modules that are already
available.

You can also use:

``` powershell
Get-InstalledModule Microsoft.Graph -ErrorAction SilentlyContinue
```

if PowerShellGet is available.

------------------------------------------------------------------------

# Find Microsoft Graph Modules

Search the PowerShell Gallery:

``` powershell
Find-Module Microsoft.Graph
```

You can also discover Graph submodules:

``` powershell
Find-Module Microsoft.Graph.*
```

The Microsoft Graph SDK is divided into many modules for different
resource areas.

Examples include modules for:

``` text
Authentication
Users
Groups
Applications
Devices
```

------------------------------------------------------------------------

# Installing the Main SDK

A common current-user installation is:

``` powershell
Install-Module Microsoft.Graph `
    -Scope CurrentUser `
    -Repository PSGallery
```

Microsoft's installation guidance may include `-Force` when appropriate.

Using:

``` powershell
-Scope CurrentUser
```

normally avoids requiring an all-users installation.

> On a managed company computer, follow your organization's software and
> PowerShell module policies before installing anything.

------------------------------------------------------------------------

# Main Module vs. Submodules

Installing:

``` powershell
Microsoft.Graph
```

installs a large collection of Graph submodules.

This is convenient for a training workstation because many Graph cmdlets
become available.

However, production automation may only need a small number of modules.

For example, a script focused on authentication and users may only need
relevant submodules rather than the entire SDK.

A smaller dependency set can make scripts easier to maintain.

------------------------------------------------------------------------

# Authentication Module

One particularly important module is:

``` text
Microsoft.Graph.Authentication
```

It provides important commands such as:

``` powershell
Connect-MgGraph
Disconnect-MgGraph
Get-MgContext
```

Authentication is required before accessing protected Microsoft Graph
resources.

------------------------------------------------------------------------

# Verify the Installation

After installation, verify:

``` powershell
Get-InstalledModule Microsoft.Graph
```

You can also inspect available Graph modules:

``` powershell
Get-Module Microsoft.Graph* -ListAvailable |
    Sort-Object Name |
    Select-Object Name, Version, Path
```

This gives you more detail about what PowerShell can find.

------------------------------------------------------------------------

# Importing Modules

PowerShell can automatically load modules when you call commands from
them.

You can also import explicitly:

``` powershell
Import-Module Microsoft.Graph.Authentication
```

Then verify:

``` powershell
Get-Module Microsoft.Graph.Authentication
```

Remember:

``` powershell
Get-Module
```

shows loaded modules.

``` powershell
Get-Module -ListAvailable
```

shows modules PowerShell can find.

------------------------------------------------------------------------

# Discover Installed Commands

Once modules are installed, try:

``` powershell
Get-Command -Module Microsoft.Graph.Authentication
```

You should see commands related to Graph authentication and context.

Do not worry about memorizing them.

Use command discovery.

------------------------------------------------------------------------

# Microsoft.Graph vs. Microsoft.Graph.Beta

The SDK has separate modules for:

``` text
Microsoft.Graph
Microsoft.Graph.Beta
```

Conceptually:

``` text
Microsoft.Graph
        ↓
Graph v1.0

Microsoft.Graph.Beta
        ↓
Graph beta
```

The beta API can expose functionality before it reaches v1.0, but beta
behavior can change.

For normal training and production-oriented scripts:

> Prefer Microsoft.Graph / v1.0 unless there is a specific reason to use
> beta.

------------------------------------------------------------------------

# Installing Beta

The beta module is installed separately.

Example:

``` powershell
Install-Module Microsoft.Graph.Beta `
    -Scope CurrentUser `
    -Repository PSGallery
```

You do **not** need beta merely to learn Graph PowerShell.

This course will favor v1.0.

------------------------------------------------------------------------

# Updating the SDK

To update an installed module:

``` powershell
Update-Module Microsoft.Graph
```

Before updating production automation dependencies, consider:

``` text
What version is currently installed?
Could a new version affect the script?
Has the update been tested?
```

"Newest" does not automatically mean "deploy immediately everywhere."

------------------------------------------------------------------------

# Inspect Versions

Use:

``` powershell
Get-Module Microsoft.Graph* -ListAvailable |
    Select-Object Name, Version, Path
```

If multiple versions exist, the output can help you identify them.

For repeatable production automation, module version awareness matters.

------------------------------------------------------------------------

# Execution Policy Is Not a Security Boundary

You may encounter installation guidance involving PowerShell execution
policy, particularly with Windows PowerShell.

Inspect your current setting:

``` powershell
Get-ExecutionPolicy -List
```

Do not change organization-managed policy simply to complete a lab.

Execution policy is intended to help control script execution behavior;
it should not be treated as the primary security boundary for
PowerShell.

------------------------------------------------------------------------

# PowerShell 5.1 vs. PowerShell 7

One easy source of confusion is installing a module in one PowerShell
environment and then opening another.

For example:

``` text
Windows PowerShell 5.1
```

and:

``` text
PowerShell 7
```

are separate environments.

Install and verify the SDK in the PowerShell version you actually intend
to use.

------------------------------------------------------------------------

# A Good Installation Workflow

Use this approach:

``` text
Check PowerShell version
        ↓
Check existing modules
        ↓
Find the official module
        ↓
Review scope / policy
        ↓
Install
        ↓
Verify
        ↓
Discover commands
```

------------------------------------------------------------------------

# Common Beginner Mistakes

## Installing Before Checking

First use:

``` powershell
Get-Module -ListAvailable
```

------------------------------------------------------------------------

## Installing Everything on Every Machine

A development or training workstation may use the full SDK.

A focused automation script may only need specific modules.

------------------------------------------------------------------------

## Assuming Beta Is Better

Beta means preview, not "newer and automatically preferable."

------------------------------------------------------------------------

## Installing in the Wrong PowerShell Version

Verify:

``` powershell
$PSVersionTable.PSVersion
```

before and after installation.

------------------------------------------------------------------------

## Ignoring Organizational Policy

Do not install modules on managed systems without considering company
policy and trust requirements.

------------------------------------------------------------------------

# Key Takeaways

-   PowerShell 7+ is recommended for Graph PowerShell.
-   Check whether modules are already installed before installing them.
-   The SDK is published through the PowerShell Gallery.
-   `Microsoft.Graph` installs the main v1.0 SDK collection.
-   The SDK is divided into submodules.
-   `Microsoft.Graph.Authentication` provides core authentication
    commands.
-   `Get-InstalledModule` and `Get-Module -ListAvailable` help verify
    installation.
-   Beta is separate and should not be your default for
    production-oriented work.
-   Install and verify the SDK in the PowerShell version you intend to
    use.
-   Follow organizational policy on managed systems.

------------------------------------------------------------------------

# Lab

Continue to:

[Lab 02 --- Installing the Microsoft Graph PowerShell
SDK](../labs/lesson-02-lab-02-installing-the-graph-sdk.md)

------------------------------------------------------------------------

## Additional Resources

-   [Install the Microsoft Graph PowerShell
    SDK](https://learn.microsoft.com/powershell/microsoftgraph/installation)
-   [Microsoft Graph PowerShell
    documentation](https://learn.microsoft.com/powershell/microsoftgraph/)
