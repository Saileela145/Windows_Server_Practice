# 🖥️ File & Storage Management + Sharing & Permissions (Windows Server Core)

## 🎯 Goal
Learn how to manage disks, volumes, and shared folders in **Windows Server Core**,  
set correct permissions, and recover if something goes wrong.

## 📚 Why This is Important
A SysAdmin must:
- Manage **server storage** without breaking data.
- Share folders **securely** with correct access.
- **Restrict users** so only authorized people can access files.
- **Recover** quickly if a command fails or is misconfigured.
- 
## 📋 Step-by-Step Guide

### 1️⃣ Check Available Disks
```
 Get-Disk
 
/
# Purpose: Lists all connected physical disks.

Expected Output:

Disk Number

Operational Status (Online / Offline)

Partition Style (RAW, MBR, GPT)

Size

Example Output:

javascript
Copy
Edit
Number Friendly Name   OperationalStatus Size     PartitionStyle
0      Virtual HD      Online            60 GB    MBR
1      Virtual HD      Online            20 GB    RAW
Possible Errors:

Get-Disk : Access is denied → You’re not running as Administrator.

No disks found → No extra disks are attached.

Recovery:

Run PowerShell as Administrator.

Attach another virtual disk in Hyper-V/VMware and recheck.

2️⃣ Initialize a New Disk

Initialize-Disk -Number 1 -PartitionStyle MBR
Purpose: Prepares the disk so Windows can use it.

Expected Output:

No error → Disk is now initialized (PartitionStyle will change from RAW to MBR or GPT).

Possible Errors:

The disk is already initialized → Skip to step 3.

Access denied → Run as Administrator.

Disk number not found → Check disk number with Get-Disk.

Recovery:

Use correct disk number from Get-Disk.

If already initialized, skip.

3️⃣ Create a New Partition
powershell
Copy
Edit
New-Partition -DiskNumber 1 -UseMaximumSize -AssignDriveLetter
Purpose: Creates a partition on the initialized disk.

Expected Output:

Drive letter assigned automatically (e.g., E:).

Possible Errors:

Not enough space → Disk already partitioned or too small.

Access denied → Run as Administrator.

Recovery:

If partitions exist:

powershell
Copy
Edit
Get-Partition -DiskNumber 1 | Remove-Partition
Then retry.

4️⃣ Format the Partition
powershell
Copy
Edit
Format-Volume -DriveLetter E -FileSystem NTFS -NewFileSystemLabel "DataDisk"
Purpose: Formats partition with NTFS for Windows use.

Expected Output:

Progress bar showing formatting.

Drive ready for use.

Possible Errors:

The volume is in use → Close any open files/folders.

Invalid drive letter → Check drive letters with:

powershell
Copy
Edit
Get-Volume
Recovery:

Use correct drive letter.

If in use, unmount or stop using the drive before formatting.

5️⃣ Create a Shared Folder
powershell
Copy
Edit
New-Item -Path "E:\HR_Data" -ItemType Directory
New-SmbShare -Name "HRShare" -Path "E:\HR_Data" -FullAccess "HRGroup"
Purpose:

Creates a folder E:\HR_Data.

Shares it as \\ServerName\HRShare for HRGroup.

Expected Output:

No error → Folder is shared successfully.

Possible Errors:

Access denied → Run as Administrator.

Group HRGroup not found → Create group first:

powershell
Copy
Edit
net localgroup HRGroup /add
Recovery:

Ensure the group exists.

Ensure path exists before sharing.

6️⃣ Set NTFS Permissions
powershell
Copy
Edit
icacls "E:\HR_Data" /grant "HRGroup:(OI)(CI)F"
Purpose:

(OI) = Object Inherit → Files inside inherit permissions.

(CI) = Container Inherit → Subfolders inherit permissions.

(F) = Full control.

Expected Output:

nginx
Copy
Edit
processed file: E:\HR_Data
Successfully processed 1 files; Failed processing 0 files
Possible Errors:

No mapping between account names and security IDs → Group/user name incorrect.

Access denied → Run as Administrator.

Recovery:

Use correct group name.

Check permissions with:

powershell
Copy
Edit
icacls "E:\HR_Data"
7️⃣ Restrict Other Users
powershell
Copy
Edit
icacls "E:\HR_Data" /remove "Domain Users"
Purpose:

Removes default access for everyone in the domain.

Expected Output:

No error → Domain Users removed.

Possible Errors:

No mapping between account names and security IDs → Name incorrect.

Access denied → Run as Administrator.

Recovery:

Check current permissions:

powershell
Copy
Edit
icacls "E:\HR_Data"
Remove correct group name.

8️⃣ Test from a Client
From another PC:

Copy
Edit
\\ServerName\HRShare
Expected Results:

HR user → ✅ Can access and edit files.

Non-HR user → ❌ Access denied.

If HR user cannot access:

Check they are in HRGroup:

powershell
Copy
Edit
net user <username> /domain
Run on server:

powershell
Copy
Edit
gpupdate /force
