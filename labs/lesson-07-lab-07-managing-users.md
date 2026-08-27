# Lab 07 --- Managing Users Safely

## Lab Objective

Practice planning and validating user changes.

**This lab does not require a real user modification.**

------------------------------------------------------------------------

# Exercise 1 --- Discover Write Commands

Run:

``` powershell
Get-Command New-MgUser
Get-Command Update-MgUser
Get-Command Remove-MgUser
```

Use:

``` powershell
Find-MgGraphCommand -Command New-MgUser
Find-MgGraphCommand -Command Update-MgUser
Find-MgGraphCommand -Command Remove-MgUser
```

Classify the commands:

  Command           Action
  ----------------- --------
  `New-MgUser`      
  `Update-MgUser`   
  `Remove-MgUser`   

------------------------------------------------------------------------

# Exercise 2 --- Read Help

Run:

``` powershell
Get-Help New-MgUser -Examples
```

Then:

``` powershell
Get-Help Update-MgUser -Examples
```

List three things you should validate before creating a user:

``` text
1. ____________________________________

2. ____________________________________

3. ____________________________________
```

------------------------------------------------------------------------

# Exercise 3 --- Create a Preview Object

Create a simulated request:

``` powershell
$request = [pscustomobject]@{
    UserPrincipalName = 'training.user@example.com'
    DisplayName       = 'Training User'
    Department        = 'IT'
    Action            = 'Create'
}
```

Display it:

``` powershell
$request | Format-List
```

Add a property named:

``` text
ValidationStatus
```

to your own version.

------------------------------------------------------------------------

# Exercise 4 --- Validate Input

Write conditions that identify:

``` text
Blank UPN
Blank display name
Blank department
```

Do not call a Graph write command.

``` powershell
# Your validation here
```

------------------------------------------------------------------------

# Exercise 5 --- Plan an Update

Scenario:

> A user's department should change from Operations to IT.

Write the safe sequence:

``` text
1. ____________________________________

2. ____________________________________

3. ____________________________________

4. ____________________________________

5. ____________________________________
```

------------------------------------------------------------------------

# Optional Test-Tenant Exercise

Only perform a real update if you have:

``` text
A dedicated test user
A controlled tenant
Authorization to make the change
The correct least-privileged permission
```

If all conditions are met:

1.  Verify `Get-MgContext`.
2.  Retrieve the exact test user.
3.  Record the existing value.
4.  Preview the intended change.
5.  Use `Update-MgUser` on a harmless test property.
6.  Retrieve the user again.
7.  Verify the result.
8.  Restore the original test value if appropriate.

Do not use a production employee account for practice.

------------------------------------------------------------------------

# Knowledge Check

1.  Which command creates a Graph user?

    A. `New-MgUser`\
    B. `Get-MgUser`\
    C. `Find-MgUser`\
    D. `Start-MgUser`

2.  What should happen before a bulk change?

    A. Preview and validation\
    B. Delete old records\
    C. Request every permission\
    D. Skip testing

3.  Should passwords be committed to Git?

    A. No\
    B. Yes

------------------------------------------------------------------------

# Lab Complete

Continue to:

[Lesson 08 --- Groups and
Membership](../lessons/lesson-08-groups-and-membership.md)
