# Lab 17 --- Error Handling and Reliable Automation

## Lab Objective

Add validation, error handling, and logging to a read-only Microsoft
Graph script.

------------------------------------------------------------------------

# Exercise 1 --- Create a Safe Function

Start with:

``` powershell
function Get-GraphUserSafe {
    param(
        [Parameter(Mandatory)]
        [string]$UserId
    )

    # Add your code
}
```

Add validation for a blank value.

------------------------------------------------------------------------

# Exercise 2 --- Add try/catch

Inside the function, use:

``` powershell
try {
    Get-MgUser -UserId $UserId -ErrorAction Stop
}
catch {
    Write-Warning "Unable to retrieve $UserId"
    Write-Warning $_.Exception.Message
}
```

Test only with identifiers you are authorized to query.

------------------------------------------------------------------------

# Exercise 3 --- Test a Failure

Use a deliberately nonexistent **training-style** identifier rather than
a real person's information.

Observe the error.

What information is useful to an administrator?

``` text
____________________________________________________
```

------------------------------------------------------------------------

# Exercise 4 --- Validate Graph Context

Retrieve:

``` powershell
$context = Get-MgContext
```

Write logic that stops if there is no Graph context.

``` powershell
# Your solution
```

Optional: validate an expected tenant ID supplied as a parameter or
configuration value.

------------------------------------------------------------------------

# Exercise 5 --- Create a Log Object

For each lookup, create an object containing:

``` text
Time
Operation
Target
Status
Message
```

Example output:

``` text
2026-08-27  GetUser  training@example.com  Success
```

Do not include tokens or secrets.

------------------------------------------------------------------------

# Exercise 6 --- Export the Log

Store log objects in an array or collection.

Export them:

``` powershell
Export-Csv .\graph-script-log.csv -NoTypeInformation
```

------------------------------------------------------------------------

# Exercise 7 --- Decide What to Retry

Mark each as:

``` text
Retry / Do Not Retry
```

  Failure                     Decision
  --------------------------- ----------
  Temporary network failure   
  Invalid user ID             
  Missing permission          
  Throttling response         
  Blank CSV field             

Explain your choices.

------------------------------------------------------------------------

# Exercise 8 --- Build a Reliable Read-Only Script

Create a script that:

``` text
Checks Graph context
Accepts a small list of test UPNs
Validates each input
Attempts Get-MgUser
Logs success/failure
Continues safely
Exports results
Exports log
```

Do not make tenant changes.

------------------------------------------------------------------------

# Knowledge Check

1.  Which block handles a terminating error?

    A. `catch` B. `foreach` C. `switch` D. `param`

2.  What can `-ErrorAction Stop` help do?

    A. Turn an applicable error into a terminating error for handling B.
    Disconnect Graph C. Delete an object D. Grant permission

3.  Should access tokens be written to logs?

    A. No B. Yes

4.  Should every failure automatically be retried?

    A. No B. Yes

------------------------------------------------------------------------

# Lab Complete

Continue to:

[Lesson 18 --- App-Only Authentication and
Automation](../lessons/lesson-18-app-only-authentication-and-automation.md)
