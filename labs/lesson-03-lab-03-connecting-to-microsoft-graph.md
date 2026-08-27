# Lab 03 --- Connecting to Microsoft Graph

## Lab Objective

In this lab, you will make a narrow delegated Graph connection, inspect
the context, and disconnect.

Use only a Microsoft account and tenant you are authorized to access.

------------------------------------------------------------------------

# Exercise 1 --- Confirm Authentication Commands

Run:

``` powershell
Get-Command Connect-MgGraph
Get-Command Get-MgContext
Get-Command Disconnect-MgGraph
```

If these are unavailable, return to Lesson/Lab 02 and verify the SDK
installation.

------------------------------------------------------------------------

# Exercise 2 --- Connect with a Narrow Scope

Use:

``` powershell
Connect-MgGraph -Scopes 'User.Read'
```

Complete the authentication prompt.

Do not request additional scopes for this exercise.

------------------------------------------------------------------------

# Exercise 3 --- Inspect Context

Run:

``` powershell
Get-MgContext
```

Record:

``` text
Account:
________________________________________

Tenant ID:
________________________________________

Authentication type:
________________________________________
```

------------------------------------------------------------------------

# Exercise 4 --- Inspect Scopes

Run:

``` powershell
(Get-MgContext).Scopes |
    Sort-Object
```

Is `User.Read` present?

``` text
Yes / No
```

You may also see standard OpenID-related scopes. Focus on understanding
why the Graph permission you requested appears in the session.

------------------------------------------------------------------------

# Exercise 5 --- Store Context as an Object

Run:

``` powershell
$context = Get-MgContext
```

Then:

``` powershell
$context | Get-Member
```

Retrieve:

``` powershell
$context.Account
$context.TenantId
$context.AuthType
```

This reinforces that Graph session information is a PowerShell object.

------------------------------------------------------------------------

# Exercise 6 --- Verify Before Acting

Answer:

``` text
Am I signed in with the intended account?
Yes / No

Am I in the intended tenant?
Yes / No

Do I understand the scope I requested?
Yes / No
```

If any answer is **No**, disconnect before continuing.

------------------------------------------------------------------------

# Exercise 7 --- Optional Device Authentication

If you want to observe the alternative sign-in flow, first disconnect:

``` powershell
Disconnect-MgGraph
```

Then:

``` powershell
Connect-MgGraph `
    -Scopes 'User.Read' `
    -UseDeviceAuthentication
```

Follow the displayed instructions.

Afterward:

``` powershell
Get-MgContext
```

Compare the authentication provider/context information with the earlier
connection.

This exercise is optional.

------------------------------------------------------------------------

# Exercise 8 --- Disconnect

Run:

``` powershell
Disconnect-MgGraph
```

Then:

``` powershell
Get-MgContext
```

What changed?

``` text
____________________________________________________
```

------------------------------------------------------------------------

# Exercise 9 --- Write the Safe Connection Workflow

Without looking back, fill in:

``` text
1. ______________________________
2. ______________________________
3. ______________________________
4. Perform intended work
5. ______________________________
```

The intended pattern is more important than memorizing exact formatting.

------------------------------------------------------------------------

# Knowledge Check

1.  Which command establishes a Graph PowerShell connection?

    A. `Start-MgGraph` B. `Connect-MgGraph` C. `Open-MgGraph` D.
    `Login-Graph`

2.  Which command shows the current Graph session context?

    A. `Get-MgContext` B. `Get-MgUser` C. `Show-MgLogin` D.
    `Get-GraphSession`

3.  What should you verify immediately after connecting?

    A. Account, tenant, and scopes B. Screen resolution C. Printer
    status D. Local disk space

4.  Which command ends the Graph connection?

    A. `Stop-MgGraph` B. `Exit-MgGraph` C. `Disconnect-MgGraph` D.
    `Remove-MgGraph`

------------------------------------------------------------------------

# Lab Complete

Continue to:

[Lesson 04 --- Permissions and
Scopes](../lessons/lesson-04-permissions-and-scopes.md)
