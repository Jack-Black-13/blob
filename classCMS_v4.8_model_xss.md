# Stored XSS Vulnerability Report

## Description
A stored XSS vulnerability exists in the model management module of Classcms. Attackers can inject malicious scripts, which are stored in the system. These scripts are executed when other users access the affected page, potentially leading to the execution of harmful code.

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
In the model management page, the `uri` parameter does not properly sanitize and escape user inputs. This allows attackers to inject malicious scripts that are stored in the database and automatically executed when other users access the affected page. This vulnerability could lead to sensitive information leakage or user session hijacking.

## Proof of Vulnerability

1. On the model management page, in the "Add Model" functionality, inject the following payload into the `uri` field:
   ```html
   /<img src=x onerror=alert(1) />

## Steps to Reproduce

1. Log in to the backend and navigate to the **Model Management** section, then click on the **Pages** option.
![image](https://github.com/user-attachments/assets/30b27402-773f-4baf-a6ca-fc1e520dabd0)
2. Select any identifier and click on the **Edit** button.
![image](https://github.com/user-attachments/assets/6b2206e8-6b04-40af-b243-4cb01eea8b65)
3. In the URL field, input the malicious payload:
   ```html
   /<img src=x onerror=alert(1) />
![image](https://github.com/user-attachments/assets/b494d4fb-f80a-40c7-9145-0860edcab7b3)
4.Save the changes. When the model's page is accessed again, the XSS is triggered.
![image](https://github.com/user-attachments/assets/d2df1c82-caf7-46e3-894f-929a74632c2f)
![image](https://github.com/user-attachments/assets/5b4f650e-a4ee-4b16-bee7-b7d4e63905cd)



