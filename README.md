[README.md](https://github.com/user-attachments/files/31531614/README.md)
# 🔷 Microsoft Graph PowerShell Fundamentals

# 🔷 Microsoft Graph PowerShell Fundamentals

![Microsoft Graph PowerShell Training](images/graph%20powershell.png)

> A hands-on training guide for learning Microsoft Graph PowerShell and using it for modern Microsoft 365 administration.

Microsoft Graph PowerShell allows administrators to automate and manage Microsoft 365 and Microsoft Entra services through the Microsoft Graph API.

It provides access to users, groups, licensing, devices, applications, Teams, SharePoint, OneDrive, directory roles, and many other Microsoft 365 resources from PowerShell.

Microsoft Graph PowerShell is an important skill for modern Microsoft administrators and provides a path away from many older administrative modules and APIs.

This repository is designed to take you from your **first Microsoft Graph connection** through **real-world administrative reporting and automation**.

---

# 🎯 What You'll Learn

By completing this training, you will learn how to:

- Install and configure Microsoft Graph PowerShell
- Connect securely to Microsoft Graph
- Understand Graph permissions and scopes
- Find Graph commands and documentation
- Manage and report on Microsoft Entra users
- Work with groups and memberships
- Audit Microsoft 365 licensing
- Query Microsoft Entra devices
- Understand applications and service principals
- Review Microsoft Entra directory roles
- Work with Microsoft Teams
- Query SharePoint and OneDrive
- Build efficient Graph queries
- Handle pagination and large result sets
- Add error handling and logging
- Understand app-only authentication
- Build practical Microsoft 365 administration tools

---

# 🧭 Learning Path

The course follows a simple progression:

```text
LEARN
  ↓
Lesson
  ↓
PRACTICE
  ↓
Lab
  ↓
APPLY
  ↓
Project
  ↓
AUTOMATE
  ↓
Capstone
```

Lessons explain the concepts.

Labs give you guided hands-on practice.

Projects require you to combine several skills to solve a larger IT administration problem.

---

# 📚 Course Lessons

## Fundamentals

- [Lesson 01 — Introduction to Microsoft Graph PowerShell](lessons/lesson-01-introduction.md)
- [Lesson 02 — Installing Microsoft Graph PowerShell](lessons/lesson-02-installing-microsoft-graph.md)
- [Lesson 03 — Connecting to Microsoft Graph](lessons/lesson-03-connecting-to-microsoft-graph.md)
- [Lesson 04 — Permissions and Scopes](lessons/lesson-04-permissions-and-scopes.md)
- [Lesson 05 — Finding Microsoft Graph Commands](lessons/lesson-05-finding-commands.md)

## Identity Administration

- [Lesson 06 — Working with Users](lessons/lesson-06-working-with-users.md)
- [Lesson 07 — Managing Users](lessons/lesson-07-managing-users.md)
- [Lesson 08 — Groups and Membership](lessons/lesson-08-groups-and-membership.md)
- [Lesson 09 — Microsoft 365 Licensing](lessons/lesson-09-microsoft-365-licensing.md)

## Microsoft Entra Administration

- [Lesson 10 — Devices in Microsoft Entra ID](lessons/lesson-10-devices-in-microsoft-entra-id.md)
- [Lesson 11 — Applications and Service Principals](lessons/lesson-11-applications-and-service-principals.md)
- [Lesson 12 — Directory Roles](lessons/lesson-12-directory-roles.md)

## Microsoft 365 Workloads

- [Lesson 13 — Microsoft 365 and Microsoft Graph](lessons/lesson-13-microsoft-365-and-microsoft-graph.md)
- [Lesson 14 — Microsoft Teams with Graph](lessons/lesson-14-microsoft-teams-with-graph.md)
- [Lesson 15 — SharePoint and OneDrive with Graph](lessons/lesson-15-sharepoint-and-onedrive-with-graph.md)

## Advanced Graph PowerShell

- [Lesson 16 — Advanced Queries and Pagination](lessons/lesson-16-advanced-queries-and-pagination.md)
- [Lesson 17 — Error Handling and Reliable Automation](lessons/lesson-17-error-handling-and-reliable-automation.md)
- [Lesson 18 — App-Only Authentication and Automation](lessons/lesson-18-app-only-authentication-and-automation.md)

---

# 🧪 Hands-On Labs

Most lessons include a corresponding lab.

Labs are designed to reinforce the lesson using practical Microsoft Graph PowerShell commands.

You will practice tasks such as:

```text
Connecting to Microsoft Graph
        ↓
Finding commands
        ↓
Inspecting permissions
        ↓
Querying users and groups
        ↓
Auditing licenses
        ↓
Inventorying devices
        ↓
Reviewing applications
        ↓
Inspecting directory roles
        ↓
Querying Microsoft 365 workloads
        ↓
Building reliable Graph scripts
```

📁 [View All Labs](labs/)

> Most labs begin with read-only operations so you can learn Graph safely before working with administrative changes.

---

# 🛠️ Projects

The projects combine several lessons into practical Microsoft administration exercises.

## Project 01 — Microsoft Graph Environment Explorer

Build a tool that inspects your Graph environment, modules, connection context, and available commands.

📁 [Project 01 — Graph Environment Explorer](projects/project-01-graph-environment-explorer.md)

## Project 02 — User, Group & License Audit

Create a Microsoft 365 identity audit covering users, groups, and licensing.

📁 [Project 02 — User, Group & License Audit](projects/project-02-user-group-license-audit.md)

## Project 03 — Microsoft Entra Security Inventory

Build an inventory of devices, applications, service principals, and directory roles.

📁 [Project 03 — Entra Security Inventory](projects/project-03-entra-security-inventory.md)

## Project 04 — Microsoft 365 Collaboration Audit

Audit Microsoft Teams, SharePoint sites, document libraries, and selected file metadata.

📁 [Project 04 — Microsoft 365 Collaboration Audit](projects/project-04-microsoft-365-collaboration-audit.md)

## Project 05 — Microsoft Graph Automation Capstone

Bring the entire course together by building a production-style Microsoft Graph IT audit and reporting tool.

📁 [Project 05 — Graph Automation Capstone](projects/project-05-graph-automation-capstone.md)

---

# ⚡ Quick Reference

Need a command without going back through an entire lesson?

📘 [Microsoft Graph PowerShell Cheat Sheet](CheatSheet/cheatsheet.md)

The cheat sheet includes quick references for:

- Authentication
- Permissions
- Users
- Groups
- Licensing
- Devices
- Applications
- Service principals
- Directory roles
- Teams
- SharePoint
- OneDrive
- Filtering
- Pagination
- Error handling
- App-only authentication

---

# 📖 Resources

A collection of Microsoft Graph documentation and learning resources is available here:

📚 [Microsoft Graph PowerShell Resources](resources/resources.md)

Resources include:

- Microsoft Graph PowerShell documentation
- Microsoft Graph API documentation
- Graph Explorer
- Permissions reference
- Authentication documentation
- Users and groups
- Licensing
- Devices
- Applications and service principals
- Teams
- SharePoint and OneDrive
- Advanced queries
- Pagination
- Throttling
- App-only authentication

---

# 💻 Requirements

To complete the course, you should have:

- Windows 10 or Windows 11
- PowerShell
- Internet access
- A Microsoft account or Microsoft 365 account
- Access to a Microsoft Entra tenant for administrative exercises

PowerShell 7 is recommended for modern PowerShell development.

---

# 🚀 Quick Start

Install Microsoft Graph PowerShell:

```powershell
Install-Module Microsoft.Graph -Scope CurrentUser
```

Connect:

```powershell
Connect-MgGraph -Scopes "User.Read"
```

Check your connection:

```powershell
Get-MgContext
```

Run your first Graph command:

```powershell
Get-MgUser -Top 5
```

When finished:

```powershell
Disconnect-MgGraph
```

Then begin:

➡️ **[Lesson 01 — Introduction to Microsoft Graph PowerShell](lessons/lesson-01-introduction.md)**

---

# 🔐 A Note About Permissions

Microsoft Graph uses permissions to control what scripts and applications can access.

Throughout this training, follow the principle of:

> **Least Privilege — only request the permissions required for the task.**

Whenever possible, begin with read-only permissions.

Before performing administrative changes:

```text
Verify Tenant
     ↓
Verify Account
     ↓
Verify Permissions
     ↓
Verify Target
     ↓
Preview Change
     ↓
Perform Change
     ↓
Verify Result
```

---

# ⚠️ Lab Safety

Some Microsoft Graph commands can modify or delete Microsoft 365 resources.

When learning:

- Prefer `Get-Mg...` commands first
- Use test accounts when possible
- Verify the tenant before running scripts
- Verify object IDs and UPNs
- Preview bulk operations
- Never store passwords or secrets in scripts
- Never commit client secrets or access tokens to GitHub
- Use least-privileged permissions
- Test administrative automation in a controlled environment

---

# 📈 Course Progress

Use this checklist to track your progress.

## Fundamentals

- [ ] Lesson 01
- [ ] Lesson 02
- [ ] Lesson 03
- [ ] Lesson 04
- [ ] Lesson 05

## Identity Administration

- [ ] Lesson 06
- [ ] Lesson 07
- [ ] Lesson 08
- [ ] Lesson 09

## Microsoft Entra Administration

- [ ] Lesson 10
- [ ] Lesson 11
- [ ] Lesson 12

## Microsoft 365 Workloads

- [ ] Lesson 13
- [ ] Lesson 14
- [ ] Lesson 15

## Advanced Graph PowerShell

- [ ] Lesson 16
- [ ] Lesson 17
- [ ] Lesson 18

## Projects

- [ ] Project 01
- [ ] Project 02
- [ ] Project 03
- [ ] Project 04
- [ ] Project 05 — Capstone

---

# 🌐 Official Documentation

**Microsoft Graph PowerShell:**  
https://learn.microsoft.com/powershell/microsoftgraph/

**Microsoft Graph:**  
https://learn.microsoft.com/graph/

**Microsoft Graph Explorer:**  
https://developer.microsoft.com/graph/graph-explorer

**Microsoft Graph Permissions Reference:**  
https://learn.microsoft.com/graph/permissions-reference

**PowerShell:**  
https://learn.microsoft.com/powershell/

---

# 🎓 The Goal

The goal of this repository is not to memorize hundreds of Microsoft Graph commands.

The goal is to learn how to:

```text
Find the command
      ↓
Understand the object
      ↓
Determine the permission
      ↓
Connect safely
      ↓
Retrieve the data
      ↓
Process the results
      ↓
Automate the task
```

Once you understand that workflow, Microsoft Graph PowerShell becomes a powerful tool for modern Microsoft 365 administration.

---

**Ready to start?**

➡️ **[Begin Lesson 01 — Introduction to Microsoft Graph PowerShell](lessons/lesson-01-introduction.md)**
