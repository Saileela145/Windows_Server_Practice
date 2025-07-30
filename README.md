## 📘 Day 3: Disk Management in Windows Server 2022 (Server Core)
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

