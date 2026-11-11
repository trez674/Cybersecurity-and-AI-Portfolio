# Project 2 — Windows Access Control and Authentication

## 1. Project Overview

This project investigates how Microsoft Windows controls access to files and folders through user accounts, security groups, and permissions.

The practical investigation was performed on a Windows computer using the Security tab in a folder's Properties window.

**Project type:** Practical Windows security investigation  
**Tools used:** Windows File Explorer, Folder Properties, Security tab  
**Method:** Read-only inspection of existing permissions

## 2. Project Objectives

The objectives were to:

- Understand authentication and authorisation.
- Learn the principle of least privilege.
- Identify Windows user accounts and security groups.
- Examine Read, Modify, and Full control permissions.
- Understand the difference between Allow and Deny.
- Record security observations without changing system settings.

## 3. Key Cybersecurity Concepts

### Authentication

Authentication verifies a user's identity.

For example, signing in to Windows using a username and password.

### Authorisation

Authorisation determines what an authenticated user is permitted to access or change.

For example, Windows allowing a user to open one folder but denying access to another.

### Principle of Least Privilege

Least privilege means granting users only the permissions required to perform their tasks.

For example, an office receptionist should not automatically receive administrator access or permission to open confidential financial records.

## 4. Practical Investigation

### Folder Examined

The investigation examined the Windows Documents folder:

`C:\Users\gc\OneDrive\Documents`

The folder was opened in File Explorer, followed by:

**Right-click folder → Properties → Security**

The Security tab displayed the following accounts and groups:

- `gc` — the user account
- `Everyone` — a Windows security group
- `Administrators` — the local administrators group
- `SYSTEM` — a special Windows operating-system account

No folder permissions were changed during the investigation.

## 5. Permission Findings

| Account or Group | Permission Examined | Observation |
|---|---|---|
| gc | Full control | Allow ticked |
| gc | Modify | Allow ticked |
| gc | Read | Allow ticked |
| Everyone | Read | Neither Allow nor Deny ticked |
| Everyone | Modify | Neither Allow nor Deny ticked |
| Everyone | Full control | Neither Allow nor Deny ticked |
| Administrators | Full control | Allow ticked |
| SYSTEM | Full control | Allow ticked |

These findings describe the permissions displayed in the Windows Security tab during the investigation.

They do not represent a complete effective-permissions assessment of every user account.

## 6. Understanding the Results

### User Account — gc

The `gc` account had Full control of the Documents folder.

This allows extensive management of the folder, including reading, modifying, deleting, and managing permissions.

Full control is generally expected for a user's own Documents folder.

### Everyone Group

The Everyone group showed no Allow or Deny ticks for the permissions examined.

A blank checkbox is not the same as an explicit Deny.

Effective access can depend on other security group memberships, inherited permissions, and additional Windows security settings.

The presence of Everyone does not mean the folder is automatically accessible from the internet.

### Administrators Group

The Administrators group had Full control allowed.

Administrator privileges are important for managing a computer but should be used only when necessary.

### SYSTEM Account

The SYSTEM account had Full control allowed.

SYSTEM is used by Windows to perform operating-system tasks and manage resources.

This does not grant ordinary users the same level of access.

## 7. Security Considerations

This investigation demonstrated several important security principles:

1. Windows permissions control access to files and folders.
2. Authentication and authorisation perform different functions.
3. Excessive permissions can increase security risks.
4. The principle of least privilege helps limit unnecessary access.
5. Allow, Deny, and blank permission entries have different meanings.
6. Visible permission checkboxes alone may not reveal every user's effective access.

No confirmed security vulnerability was identified during this read-only investigation.

## 8. Skills Developed

Through this project, I practised:

- Navigating Windows security settings.
- Identifying user accounts and security groups.
- Inspecting file and folder permissions.
- Understanding administrator and SYSTEM privileges.
- Applying the principle of least privilege.
- Documenting practical cybersecurity observations.

## 9. Conclusion

This project improved my understanding of Windows access control and authentication.

I successfully inspected real folder permissions for my user account, Everyone, Administrators, and SYSTEM without modifying any settings.

The investigation demonstrated how Windows uses accounts, groups, and permissions to help protect files and folders.

This knowledge provides a foundation for further study of access control, user management, and cybersecurity.
