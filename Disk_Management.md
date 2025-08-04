## Disk Management in Windows Server 2022 (Server Core)
##### 🧠 Objective:
To learn how to manage disks, partitions, volumes, and file systems without GUI using diskpart in Windows Server Core. This knowledge is essential for system administrators who work with headless servers or remote setups.

#### 🧾 What is Disk Management?
Disk Management is the process of :
1️⃣ Creating, deleting, and modifying partitions.

2️⃣ Formatting disks with file systems like NTFS.

3️⃣ Assigning drive letters or mounting volumes.

4️⃣ Organizing storage to efficiently manage data.

5️⃣ In Windows Server Core, this is done using Command Line Interface (CLI) via diskpart.

### 🔧 Why is Disk Management Important for Sysadmins?
💾  Allocate space for departments, databases, logs, and backups.

🖥️  Prepare disks during new server setups or reconfigurations.

🧱  Manage storage across RAID, SAN, or virtualized environments.

🔐  Securely format and delete sensitive data.

📊  Optimize system performance by managing disk layout and usage.

🛠️  Disk Management Tool: diskpart
diskpart is a built-in command-line utility for managing disks and partitions in Windows systems.

### 🔑  Basic Workflow:
📍 List all available disks.

📍 Select a disk.

📍 Create/delete/format partitions.

📍 Assign or remove drive letters.

📍 Exit.

### 📋 Common `diskpart` Commands
___________________________________________________________________________________________________________________
|                                     |                                                                            |
|           Command                   |             Descriptive                                                    |
|-------------------------------------|----------------------------------------------------------------------------|
| `diskpart`                          | Launches the Disk Partition command-line tool                              | 
| `list disk`                         | Lists all physical disks connected to the system                           |
| `select disk <number>`              | Selects the specified disk for operations                                  |
| `list partition`                    | Lists all partitions on the currently selected disk                        |
| `create partition primary size=<X>` | Creates a primary partition of size X MB                                   |
| `select partition <number>`         | Selects the specified partition                                            |
| `delete partition`                  | Deletes the selected partition                                             |
| `delete partition override`         | Force-deletes a partition even if it's protected                           |
| `format fs=ntfs quick`              | Formats the selected partition with NTFS (quick format)                    |
| `format fs=fat32 quick`             | Formats the partition using FAT32 file system (quick format)               |
| `assign letter=<X>`                 | Assigns a specific drive letter to the selected volume                     |
| `remove letter=<X>`                 | Removes a drive letter from the selected volume                            |
| `list volume`                       | Lists all existing volumes (including those with drive letters)            |
| `select volume <number>`            | Selects the volume for further operations                                  |
| `delete volume`                     | Deletes the selected volume                                                |
| `delete volume override`            | Force-deletes the selected volume                                          |
| `shrink desired=<X>`                | Shrinks the current partition by X MB                                      |
| `extend`                            | Extends the current volume into available unallocated space                |
| `exit`                              | Exits the diskpart utility                                                 |
|__________________________________________________________________________________________________________________|

### 📌 Real-Life Use Cases
🔸 Department Drives: Creating HR, Finance, and IT drives on the same server.

🔸 Database Storage: Separate partitions for database and transaction logs.

🔸 Server Backups: Dedicated partitions for storing backup snapshots.

🔸 Disk Cleanup: Reclaiming or deleting unused partitions.


## 🪟 Step-by-Step Guide for Disk Management (Windows Server Core)

⚠️ Since **Windows Server Core** has no GUI, all disk operations are done using the command-line tool `diskpart` in **Command Prompt** or **PowerShell**.

### 1. 🧭 Open `diskpart`
```cmd
diskpart
```
> Launches the disk partitioning utility.Opens the disk partitioning tool.

### 2. 💽 List all disks
```cmd
list disk
```
> Displays all physical disks connected to the system.Shows all physical disks attached to the system.

### 3. 🔍 Select the disk you want to manage
```cmd
select disk 0
```
> Replace `0` with the actual disk number (from the `list disk` command).

### 4. 📜 View partitions on the selected disk
```cmd
list partition
```
> Shows all partitions available on the selected disk.

### 5. ➕ Create a new partition
```cmd
create partition primary size=10240
```
> Creates a new partition of **10 GB** (10,240 MB). Change the size as needed.

### 6. ✅ Format the partition
```cmd
format fs=ntfs quick
```
> Formats the partition with the **NTFS** file system using a **quick** format.

### 7. 🔡 Assign a drive letter
```cmd
assign letter=E
```
> Assigns the drive letter **E:** to the new partition.

### 8. 🔁 Exit `diskpart`
```cmd
exit
```
> Closes the disk partitioning tool.

# 📘 Optional Commands

### 🔸 To delete a partition (⚠️ DANGER: this removes data)
```cmd
select partition 1
delete partition override
```
### 🔸 To view all volumes
```cmd
list volume
```
### 🔸 To select a specific volume
```cmd
select volume 2
```
> ✅ You can now manage disks efficiently in a Server Core environment without needing the GUI.

### 📌 Summary Table: 

Common `diskpart` Commands

| **Command**                          | **Description**                          |
|--------------------------------------|------------------------------------------|
| `diskpart`                           | Start disk partition tool                |
| `list disk`                          | Show all disks                           |
| `select disk #`                      | Choose disk to manage                    |
| `list partition`                     | Show all partitions on the disk          |
| `create partition primary size=#`    | Create new primary partition             |
| `format fs=ntfs quick`               | Format with NTFS file system             |
| `assign letter=X`                    | Assign drive letter to volume            |
| `list volume`                        | List all existing volumes                |



#                                                                                                              OR


# 🖥️ Day 5 - Disk Partitioning (SysAdmin Lab)

## 📌 Objective
The purpose of this exercise is to learn how to **partition disks** in Windows Server or Windows OS using PowerShell.  
A system administrator needs this skill to organize storage, improve performance, and manage data effectively.

---

## 💡 Why We Use Disk Partitioning
- **Organization:** Keep OS, software, and user data separate.  
- **Security:** Isolate sensitive data from other files.  
- **Backup efficiency:** Easier to back up specific partitions.  
- **Multi-boot systems:** Install different operating systems on the same physical drive.  
- **Performance:** Separate frequently used files from rarely used ones.

---

## 🛠️ Command Lines for Partitioning

> ⚠️ **Run all commands in an elevated (Run as Administrator) PowerShell** unless otherwise noted.

### 1️⃣ Check Available Disks and Volumes
```powershell
Get-Disk
Get-Volume
Purpose: Lists all disks and their current partitions.

Run in: PowerShell (Admin).

2️⃣ Create a New Partition
powershell
Copy
Edit
New-Partition -DiskNumber 0 -UseMaximumSize -AssignDriveLetter
Purpose: Creates a new partition on Disk 0 using all available unallocated space.

Run in: PowerShell (Admin).

Note: Replace 0 with the correct disk number.

3️⃣ Format a Partition
powershell
Copy
Edit
Format-Volume -DriveLetter E -FileSystem NTFS -NewFileSystemLabel "DataDrive"
Purpose: Formats the E: drive with NTFS and names it "DataDrive".

Run in: PowerShell (Admin).

Common Error:

Access Denied → Means you didn’t run as Administrator or the drive is in use.

Fix: Close all programs using the drive and retry.

4️⃣ Resize an Existing Partition
powershell
Copy
Edit
Resize-Partition -DriveLetter D -Size 50GB
Purpose: Resizes the D: drive to 50 GB.

Run in: PowerShell (Admin).

⚠️ Precautions Before Partitioning
Backup your data before making changes.

Move important files from the target partition to a safe location.

Ensure enough free space exists before resizing.

Never format a drive that still has data you need.

🧑‍💻 What a SysAdmin Does in Real Jobs
When a system administrator manages storage:

Creates separate partitions for:

Operating system

User profiles/data

Applications

Backups

Expands or shrinks partitions when storage needs change.

Migrates data from one disk to another.

Monitors disk health to prevent failures.

🔄 Different Ways to Partition Disks
Using PowerShell (what we are learning here).

Using Disk Management GUI

Press Win + R → diskmgmt.msc.

Using Command Prompt (diskpart)

cmd
Copy
Edit
diskpart
list disk
select disk 0
create partition primary size=50000
format fs=ntfs label="DataDrive" quick
Using Third-Party Tools (e.g., EaseUS, MiniTool).

📅 Real-Life Applications
Separate OS from personal data for easier OS reinstallation.

Create a partition for backups.

For dual-boot systems (Windows + Linux).

Allocate storage for specific projects or clients in workplaces.

🚫 Disadvantages of Partitioning
Wasted space if partitions are not sized properly.

Reduced flexibility — resizing later can be risky.

Data loss risk if done without backups.

Misconfiguration can make the system unbootable.

📝 Why We Are Doing This Process
In this lab:

We simulate what a sysadmin would do in a new server setup.

We learn both PowerShell automation and manual disk management.

We prepare for real-world tasks like storage upgrades and disk migrations.

yaml
Copy
Edit
