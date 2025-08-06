# 🖥️ File & Storage Management + Sharing & Permissions (Windows Server Core)

## 🎯 Goal
Learn how to manage disks, volumes, and shared folders in **Windows Server Core**,  
set correct permissions, and recover if something goes wrong.

## 📚 Why This is Important
A SysAdmin must:

- Manage **server storage** without breaking data.
- Share folders **securely** with correct access.
- Restrict users so only authorized people can access files.
- Recover quickly if a command fails or is misconfigured.

## 📋 Step-by-Step Guide

### **1️⃣ Check Available Disks**
```powershell
Get-Disk ```

Purpose: Lists all connected physical disks.

Expected Output:
Disk Number
Operational Status (Online / Offline)
Partition Style (RAW, MBR, GPT)
Size

Example:
Number Friendly Name   OperationalStatus Size     PartitionStyle
0      Virtual HD      Online            60 GB    MBR
1      Virtual HD      Online            20 GB    RAW

Possible Errors & Fixes:

Access is denied → Run PowerShell as Administrator.
No disks found → Attach another virtual disk in Hyper-V/VMware and re-run.

### 2️⃣ Initialize a New Disk

Initialize-Disk -Number 1 -PartitionStyle MBR
Purpose: Prepares the disk for use.

Expected Output:
PartitionStyle changes from RAW to MBR (or GPT).
Possible Errors & Fixes:
The disk is already initialized → Skip to Step 3.
Disk number not found → Check disk number with:

Get-Disk

### 3️⃣ Create a New Partition

New-Partition -DiskNumber 1 -UseMaximumSize -AssignDriveLetter

Purpose: Creates a partition and assigns a drive letter.

Expected Output:
Drive letter assigned automatically (e.g., E:).
Possible Errors & Fixes:
Not enough space → Disk already partitioned. Remove partitions:
```
Get-Partition -DiskNumber 1 | Remove-Partition

Access denied → Run as Administrator.

### 4️⃣ Format the Partition

Format-Volume -DriveLetter E -FileSystem NTFS -NewFileSystemLabel "DataDisk"

Purpose: Formats partition with NTFS.

Expected Output:
Formatting progress bar → Drive ready for use.

Possible Errors & Fixes:

The volume is in use → Close files/folders using it.
Invalid drive letter → Check available letters:

Get-Volume

### 5️⃣ Create a Shared Folder

New-Item -Path "E:\HR_Data" -ItemType Directory
New-SmbShare -Name "HRShare" -Path "E:\HR_Data" -FullAccess "HRGroup"

Purpose:

Creates folder E:\HR_Data
Shares it as \\ServerName\HRShare for HRGroup
Possible Errors & Fixes:
Access denied → Run as Administrator.
Group HRGroup not found → Create the group:

net localgroup HRGroup /add

### 6️⃣ Set NTFS Permissions

icacls "E:\HR_Data" /grant "HRGroup:(OI)(CI)F"

Purpose:

(OI) Object Inherit → Files inherit permissions
(CI) Container Inherit → Folders inherit permissions
(F) Full control

Expected Output:

processed file: E:\HR_Data
Successfully processed 1 files; Failed processing 0 files

Possible Errors & Fixes:

No mapping between account names and security IDs → Group name is wrong.
Access denied → Run as Administrator.

Check permissions:
icacls "E:\HR_Data"

### 7️⃣ Restrict Other Users

icacls "E:\HR_Data" /remove "Domain Users"
Purpose: Removes default access for all domain users.
Possible Errors & Fixes:
Name incorrect → Check current permissions:
icacls "E:\HR_Data"

8️⃣ Test from a Client
From another PC:
\\ServerName\HRShare

Expected Results:

HR user → ✅ Access and edit files
Non-HR user → ❌ Access denied
If HR user cannot access:
net user <username> /domain
gpupdate /force










                                    
