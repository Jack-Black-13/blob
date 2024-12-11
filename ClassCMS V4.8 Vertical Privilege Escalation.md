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
