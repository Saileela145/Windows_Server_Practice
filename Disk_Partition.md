# 🖥️ Day 5 - Disk Partitioning (SysAdmin Lab)

## 📌 Objective
Learn how to **partition disks** in Windows Server or Windows OS using PowerShell.  
A system administrator needs this skill to organize storage, improve performance, and manage data effectively.

---

## 💡 Why We Use Disk Partitioning
- **Organization:** Keep OS, software, and user data separate.
- **Security:** Isolate sensitive data from other files.
- **Backup efficiency:** Easier to back up specific partitions.
- **Multi-boot systems:** Install different operating systems on the same physical drive.
- **Performance:** Separate frequently used files from rarely used ones.

---

## 🛠️ Commands for Partitioning

> ⚠️ **Run all commands in PowerShell as Administrator** (Right‑click → Run as Administrator).

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

Access Denied → You didn’t run as Administrator or the drive is in use.

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
1️⃣ Using PowerShell
(What we are learning here)

2️⃣ Using Disk Management GUI
text
Copy
Edit
Press Win + R → Type: diskmgmt.msc
3️⃣ Using Command Prompt (diskpart)
cmd
Copy
Edit
diskpart
list disk
select disk 0
create partition primary size=50000
format fs=ntfs label="DataDrive" quick
4️⃣ Using Third-Party Tools
EaseUS Partition Master

MiniTool Partition Wizard

AOMEI Partition Assistant

These tools provide:

Easier graphical interfaces

Data migration features

Partition recovery options

📅 Real-Life Applications
Separate OS from personal data for easier OS reinstallation.

Create a partition for backups to avoid mixing them with active files.

Dual-boot systems (e.g., Windows + Linux) on the same physical disk.

Allocate storage for specific projects or clients in workplaces.

🚫 Disadvantages of Partitioning
Wasted space if partitions are not sized properly.

Reduced flexibility — resizing later can be risky.

Data loss risk if done without backups.

Misconfiguration can make the system unbootable.

📝 Why We Are Doing This Process
In this lab:

We simulate what a system administrator would do in a new server setup.

We learn both PowerShell automation and manual disk management.

We prepare for real-world tasks like storage upgrades and disk migrations.

