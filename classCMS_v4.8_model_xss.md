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
`/index.php/admin/model`

## Vulnerability Details
In the model management page, the `model_name` parameter does not properly sanitize and escape user inputs. This allows attackers to inject malicious scripts that are stored in the database and automatically executed when other users access the affected page. This vulnerability could lead to sensitive information leakage or user session hijacking.

## Proof of Vulnerability

1. On the model management page, in the "Add Model" functionality, inject the following payload into the `model_name` field:
   ```html
   <img src=x onerror=alert(1) />
