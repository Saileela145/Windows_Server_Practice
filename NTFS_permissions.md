# 📂 Windows Folder Access Control using PowerShell & CMD

🎯 **Mini Project** – Managing user-specific folder access using NTFS permissions in Windows.

# AIM:
-  Create two local users: Manager1 and Employee1.
-  Give each user their own folder with full access.
-  Deny access to other users.
-  Test permissions by logging in as each user.

# TOOLS USED:

📍 Windows PowerShell - For automation and scripting
📍 CMD (Command Prompt) - For basic command-line tests
📍 New-LocalUser - Create local users
📍 icacls - Manage NTFS permissions (Integrity Control Access Control Lists)
📍 takeown - Take ownership of folders/files
📍 runas - Run programs as a different user
📍 Remove-Item - Delete files/folders
📍 New-Item - Create folders

# THEORY:
-  NTFS (New Technology File System) allows setting specific permissions for files/folders.
# Permissions can be:

;) (F)   Full Control
;) (RX)  Read & Execute
;) (R)   Read Only
;) (W)   Write
;) (OI)  Object Inherit - Applies to files inside folder
;) (CI)  Container Inherit - Applies to subfolders
;) Using icacls, we can grant or deny these permissions to users.

# 📝 Procedure & commands:

1️⃣ Create Users:
# Create Manager1 account with password Pass@123

``` New-LocalUser "Manager1" -Password (ConvertTo-SecureString "Pass@123" -AsPlainText -Force) ```

# Create Employee1 account with password Pass@123

New-LocalUser "Employee1" -Password (ConvertTo-SecureString "Pass@123" -AsPlainText -Force)

# Enable both accounts (in case they are disabled by default)

Enable-LocalUser -Name "Manager1"
Enable-LocalUser -Name "Employee1"

**Expected Output:**
Name      Enabled Description
----      ------- -----------
Manager1  True
Employee1 True

2️⃣ Create Folders:

# Create a folder for Manager1

New-Item -Path "D:\CompanyData\Manager1" -ItemType Directory

# Create a folder for Employee1

New-Item -Path "D:\CompanyData\Employee1" -ItemType Directory

**Expected Output:**
Directory: D:\CompanyData
d-----   <date-time>   Manager1
d-----   <date-time>   Employee1

3️⃣ Remove Inherited Permissions:

# Remove inherited permissions from Manager1's folder
icacls "D:\CompanyData\Manager1" /inheritance:r

# Remove inherited permissions from Employee1's folder
icacls "D:\CompanyData\Employee1" /inheritance:r

**Expected Output:**
processed file: D:\CompanyData\Manager1
Successfully processed 1 files; Failed processing 0 files

4️⃣ Grant Each User Full Control of Their Own Folder:
# Give Manager1 full control of their folder
icacls "D:\CompanyData\Manager1" /grant "Manager1:(OI)(CI)F"

# Give Employee1 full control of their folder
icacls "D:\CompanyData\Employee1" /grant "Employee1:(OI)(CI)F"

**Expected Output:**
processed file: D:\CompanyData\Manager1
Successfully processed 1 files; Failed processing 0 files

5️⃣ Deny Access to the Other User:
# Deny Employee1 from accessing Manager1's folder
icacls "D:\CompanyData\Manager1" /deny Employee1:RX

# Deny Manager1 from accessing Employee1's folder
icacls "D:\CompanyData\Employee1" /deny Manager1:RX

**Expected Output**
processed file: D:\CompanyData\Employee1
Successfully processed 1 files; Failed processing 0 files

6️⃣ Test Access:
# Run Command Prompt as Manager1
runas /user:DESKTOP-PCNAME\Manager1 cmd

# Run Command Prompt as Employee1
runas /user:DESKTOP-PCNAME\Employee1 cmd
