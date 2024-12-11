# Vertical Privilege Escalation Vulnerability Report

## Description
A privilege escalation vulnerability exists in the model management module of Classcms. This allows accounts belonging to non-admin user groups to modify admin group users and change their group memberships to other user groups. If all users in the admin group are changed to other groups, the system will no longer have the ability to configure accounts for the admin group.

## Download URL
[https://github.com/ClassCMS/ClassCMS/releases/tag/v4.8](https://github.com/ClassCMS/ClassCMS/releases/tag/v4.8)

## Version
V4.8

## Tested Environment
- PHP
- Apache
- MySQL

## Affected Page
`/index.php/admin`

## Vulnerability Details
In the user management page, the username, hash, and rolehash[0] parameters are vulnerable to vertical privilege escalation. Accounts with non-admin permissions can modify the roles of members in the admin user group, even though they cannot view admin users. While the system prevents non-admin users from elevating their own roles to the admin group, it fails to account for vertical privilege escalation that allows non-admin users to downgrade the permissions of admin group members. This oversight can result in a scenario where admin users lose their admin group membership, effectively locking all admin users out of the admin group.

## Steps to Reproduce

markdown
复制代码
1. To test this vulnerability, you need two roles with different permissions. 
   - The default role is `admin`.
   - The other role can have any name; I named it `aaa`.
2. The `aaa` role only requires the following permissions:
   - "Modify User Account" in **User Management**.
   - Access to the **Role Management** feature.
3. The setup should look as shown in the figure:
![image](https://github.com/user-attachments/assets/21785bd1-9e0e-4001-bb67-4ccd45c23428)
