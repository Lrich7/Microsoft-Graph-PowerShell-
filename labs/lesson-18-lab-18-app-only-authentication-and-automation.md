# Lab 18 --- App-Only Authentication and Automation

## Lab Objective

Design an app-only Microsoft Graph automation identity and, if you have
an authorized lab environment, test a read-only application connection.

> Do not create production credentials or grant application permissions
> merely to complete this training lab.

------------------------------------------------------------------------

# Exercise 1 --- Compare Authentication Models

Complete:

  Feature                              Delegated   App-Only
  ------------------------------------ ----------- ----------
  Interactive user present                         
  Uses delegated permissions                       
  Uses application permissions                     
  Good fit for unattended automation               

------------------------------------------------------------------------

# Exercise 2 --- Design an Automation

Scenario:

> Every morning, a script exports a read-only inventory of enabled
> Microsoft Entra users.

Document:

``` text
Purpose:
________________________________________

Owner:
________________________________________

Required data:
________________________________________

Write access required?
________________________________________

Likely permission category:
________________________________________
```

------------------------------------------------------------------------

# Exercise 3 --- Credential Choice

Compare:

``` text
Certificate
Client secret
```

Write two reasons a certificate may be preferable for production
automation:

``` text
1. ____________________________________

2. ____________________________________
```

------------------------------------------------------------------------

# Exercise 4 --- Security Checklist

Complete:

``` text
[ ] Least-privileged permissions
[ ] Named owner
[ ] Credential stored securely
[ ] Credential expiration documented
[ ] ____________________________________
[ ] ____________________________________
```

------------------------------------------------------------------------

# Exercise 5 --- Connection Planning

A certificate-based connection can use a pattern such as:

``` powershell
Connect-MgGraph `
    -ClientId '<application-id>' `
    -TenantId '<tenant-id>' `
    -CertificateThumbprint '<certificate-thumbprint>'
```

Identify what each value represents:

``` text
ClientId:
________________________________________

TenantId:
________________________________________

CertificateThumbprint:
________________________________________
```

------------------------------------------------------------------------

# Exercise 6 --- Optional Authorized Lab-Tenant Connection

Only if you already have or are authorized to create a dedicated test
application with read-only permissions:

1.  Configure the application according to your tenant's policy.
2.  Grant only the required read-only application permission.
3.  Configure an approved certificate credential.
4.  Connect with `Connect-MgGraph`.
5.  Run:

``` powershell
Get-MgContext
```

6.  Verify the tenant and authentication type.
7.  Run only the read-only test query authorized for the application.
8.  Disconnect when finished.

Do not grant broad write permissions for this exercise.

------------------------------------------------------------------------

# Exercise 7 --- Rotation Plan

Write a simple credential lifecycle:

``` text
Credential created:
________________________________________

Expiration tracked in:
________________________________________

Owner notified:
________________________________________

Rotation tested:
________________________________________
```

------------------------------------------------------------------------

# Exercise 8 --- Automation Design

Create a flow:

``` text
Scheduled trigger
      ↓
Authenticate
      ↓
Verify context
      ↓
Run read-only query
      ↓
Process results
      ↓
Export/report
      ↓
Log outcome
      ↓
Disconnect/cleanup
```

Add where error handling from Lesson 17 belongs.

------------------------------------------------------------------------

# Knowledge Check

1.  Which authentication model is designed for an application acting
    without an interactive user?

    A. App-only B. Delegated only

2.  Do application permissions commonly require administrator consent?

    A. Yes B. No

3.  Should a client secret be committed to GitHub?

    A. No B. Yes

4.  Should a read-only report receive write permissions simply for
    convenience?

    A. No B. Yes

------------------------------------------------------------------------

# Lab Complete


------------------------------------------------------------------------

# 🏆 Final Project — Microsoft Graph Automation Capstone

You have completed all 18 lessons and labs in the Microsoft Graph PowerShell course.

Now it's time to bring everything together in the final capstone project.

➡️ **[Project 05 — Microsoft Graph Automation Capstone](../projects/project-05-graph-automation-capstone.md)**

In this project, you will combine the skills developed throughout the course to build a practical Microsoft Graph PowerShell automation and reporting solution.

You will apply concepts including:

- Microsoft Graph authentication
- Permissions and scopes
- Command discovery
- Users and groups
- Microsoft 365 licensing
- Devices
- Applications and service principals
- Directory roles
- Microsoft 365 workloads
- Advanced queries
- Error handling
- Reliable automation
- App-only authentication

This project is designed to demonstrate that you can move beyond individual commands and build a complete Microsoft Graph PowerShell solution.

------------------------------------------------------------------------

# 🎯 Finish Strong

Complete the capstone without immediately returning to the lesson instructions whenever possible.

Use the same tools you would use in a real environment:

```text
Get-Command
      ↓
Get-Help
      ↓
Find-MgGraphCommand
      ↓
Find-MgGraphPermission
      ↓
Microsoft Learn
      ↓
Test
      ↓
Troubleshoot
      ↓
Improve

------------------------------------------------------------------------

# 🎓 Course Complete!

Congratulations — you have completed the **Microsoft Graph PowerShell Fundamentals** training course.

You have progressed from making your first Microsoft Graph connection to building a complete Microsoft Graph PowerShell automation solution.

## Where to Go Next

Continue practicing by:

- Building your own Microsoft 365 administration scripts
- Automating repetitive IT tasks
- Creating user, group, license, and device reports
- Improving scripts with logging and error handling
- Exploring additional Microsoft Graph APIs
- Practicing app-only authentication
- Reviewing the cheat sheet and course resources
- Turning useful scripts into reusable IT administration tools

---

# 📚 Course Resources

➡️ **[Microsoft Graph PowerShell Cheat Sheet](../CheatSheet/cheatsheet.md)**

➡️ **[Microsoft Graph PowerShell Resources](../resources/resources.md)**

➡️ **[Return to Course Home](../README.md)**

---

> The goal was never to memorize every Microsoft Graph command.  
> The goal was to learn how to **find, understand, safely use, and automate them.**


