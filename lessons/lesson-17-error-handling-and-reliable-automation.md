# Lesson 17 --- Error Handling and Reliable Automation

## Learning Objectives

By the end of this lesson, you will be able to:

-   Explain why production Graph scripts need error handling.
-   Use `try`, `catch`, and `finally`.
-   Use `-ErrorAction Stop` when appropriate.
-   Validate Graph context and input before performing work.
-   Create useful log messages.
-   Distinguish validation failures from runtime failures.
-   Design retry logic carefully for transient failures.
-   Build automation that fails safely.

------------------------------------------------------------------------

# Scripts Fail

A script that works once is not automatically reliable automation.

Microsoft Graph scripts can fail because of:

``` text
Authentication
Expired sessions
Missing permissions
Invalid IDs
Deleted objects
Network problems
Throttling
Service interruptions
Bad input data
Unexpected null values
```

Your script should expect failure and handle it intentionally.

------------------------------------------------------------------------

# try and catch

PowerShell provides:

``` powershell
try {
    # Code that might fail
}
catch {
    # Handle the failure
}
```

Example:

``` powershell
try {
    $user = Get-MgUser `
        -UserId 'user@contoso.com' `
        -ErrorAction Stop
}
catch {
    Write-Warning "Unable to retrieve user: $($_.Exception.Message)"
}
```

------------------------------------------------------------------------

# Why -ErrorAction Stop Matters

Not every PowerShell error is terminating by default.

A `catch` block handles terminating errors.

For commands where you need the failure to enter `catch`, you may use:

``` powershell
-ErrorAction Stop
```

Do not add it blindly everywhere. Understand the command and desired
behavior.

------------------------------------------------------------------------

# finally

`finally` runs whether the `try` block succeeds or fails.

Example:

``` powershell
try {
    # Work
}
catch {
    # Error handling
}
finally {
    # Cleanup
}
```

This is useful for cleanup tasks.

------------------------------------------------------------------------

# Validate Before the Graph Call

Many errors should be prevented before Graph is contacted.

Example:

``` powershell
if ([string]::IsNullOrWhiteSpace($UserPrincipalName)) {
    throw 'UserPrincipalName cannot be blank.'
}
```

Validation can check:

``` text
Required input
File existence
Expected columns
Tenant context
Object identifiers
Allowed action
```

------------------------------------------------------------------------

# Validate Graph Context

Before administrative work:

``` powershell
$context = Get-MgContext
```

Then inspect values such as:

``` text
Account
TenantId
Scopes
AuthType
```

A production script can stop if the expected context is not present.

------------------------------------------------------------------------

# Fail Safely

Suppose a script receives 100 proposed user changes.

If item 12 is invalid, should the script:

``` text
Continue blindly?
Stop everything?
Log the item and continue?
```

There is no universal answer.

The correct behavior depends on the task.

For high-impact changes, stopping may be safer.

For a read-only report, logging a missing object and continuing may be
reasonable.

Design this behavior intentionally.

------------------------------------------------------------------------

# Logging

Useful logs answer:

``` text
When did it happen?
What operation was attempted?
Which object was involved?
Did it succeed?
If it failed, why?
```

Example:

``` powershell
$log = [pscustomobject]@{
    Time      = Get-Date
    Operation = 'Get User'
    Target    = $UserPrincipalName
    Status    = 'Failed'
    Message   = $_.Exception.Message
}
```

Avoid writing secrets or access tokens to logs.

------------------------------------------------------------------------

# Retry Logic

Some failures are transient.

Examples can include:

``` text
Temporary network problems
Service availability issues
Throttling
```

Retries should be:

``` text
Limited
Logged
Delayed appropriately
Used only for failures that make sense to retry
```

Do not retry permanent failures such as:

``` text
Invalid user ID
Missing required permission
Bad input format
```

------------------------------------------------------------------------

# Separate Validation from Execution

A strong automation pattern is:

``` text
Input
  ↓
Validation
  ↓
Preview
  ↓
Execution
  ↓
Verification
  ↓
Logging
```

This is much safer than:

``` text
Input
  ↓
Immediately change tenant
```

------------------------------------------------------------------------

# Common Beginner Mistakes

## Empty catch Blocks

Never hide failures without explanation.

Bad:

``` powershell
catch {
}
```

## Logging Secrets

Logs should not contain credentials, tokens, or client secrets.

## Retrying Every Error

Some failures require correction, not another attempt.

## No Verification

A command returning without an obvious error is not always enough. Read
back important changes when appropriate.

------------------------------------------------------------------------

# Key Takeaways

-   Expect Graph automation to encounter failures.
-   Use `try`, `catch`, and `finally` deliberately.
-   `-ErrorAction Stop` can make errors catchable when appropriate.
-   Validate inputs and Graph context before work begins.
-   Log useful information without logging secrets.
-   Retry only appropriate transient failures.
-   Separate validation, execution, verification, and logging.
-   Reliable automation should fail safely.

------------------------------------------------------------------------

# Lab

Continue to:

[Lab 17 --- Error Handling and Reliable
Automation](../labs/lesson-17-lab-17-error-handling-and-reliable-automation.md)

------------------------------------------------------------------------

## Additional Resources

-   [PowerShell about Try Catch
    Finally](https://learn.microsoft.com/powershell/module/microsoft.powershell.core/about/about_try_catch_finally)
-   [PowerShell about
    CommonParameters](https://learn.microsoft.com/powershell/module/microsoft.powershell.core/about/about_commonparameters)
-   [Microsoft Graph throttling
    guidance](https://learn.microsoft.com/graph/throttling)
