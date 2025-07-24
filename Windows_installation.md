# 🧑‍💻 Windows Server 2022 Installation Steps (Full GUI Version)

#### --> ✅ Before You Start
          Make sure you have:
## ✅ VirtualBox or VMware installed [<img width="960" height="1020" alt="Screenshot 2025-07-22 000231" src="https://github.com/user-attachments/assets/c057c809-799c-4ebf-a8c1-bcd23192e3c9" />]should be installed like this.

## ✅ Windows Server 2022 ISO file (already with you)[<img width="996" height="693" alt="Screenshot 2025-07-21 235600" src="https://github.com/user-attachments/assets/31f5fac7-7db8-4650-88ec-676f7eb06359" />] after giving name as Windows Server 2022.The following step to do....

## 🔧 Step-by-Step Installation (with GUI):
# 1.📌 Step 1: Start Virtual Machine
Open VirtualBox
Click New → Name it: Windows Server 2022
Choose:
Type: Microsoft Windows
Version: Windows 2022 (64-bit)
Click Next

# 2.📌 Step 2: Set Memory & CPU
RAM: At least 2048 MB (4 GB recommended)
CPU: 2 cores (Go to → Settings > System > Processor)
#### Select all the things as shown in figure.
[<img width="996" height="693" alt="Screenshot 2025-07-21 235600" src="https://github.com/user-attachments/assets/aab15a58-8a51-4d16-b5aa-f56f81d9ffda" />]

# 3.📌 Step 3: Create Virtual Hard Disk
Choose: Create a virtual hard disk now
Size: 50 GB or more
Type: VDI, Dynamically Allocated

# 4.📌 Step 4: Attach ISO File
Go to VM → Settings
Click Storage
Under “Controller: IDE” click the Empty disc
On the right, click the CD icon → Choose “Choose a disk file...”
Select your Windows Server 2022 ISO 
### If u dont install iso then it shown image like this.[<img width="722" height="493" alt="Screenshot 2025-07-21 231101" src="https://github.com/user-attachments/assets/e66227e9-f44f-4ed6-8210-eca70c7d6e28" />] . You definitely need to install iso in vm box.


###### Do the things as shown in figure.
[<img width="962" height="597" alt="Screenshot 2025-07-22 000003" src="https://github.com/user-attachments/assets/82d098c5-5675-42dc-8d34-0f58d5291db8" />]

# 5.🖥️ Step 5: Start the VM
Click Start
Wait for the Windows Setup screen

# 6.📌 Step 6: Installation Begins
Select:
Language: English
Time: India or preferred
Keyboard: US
Click Next
Click Install Now

# 7.📌 Step 7: Choose Server Version
🔵 Very Important:
Choose this option:
✅ Windows Server 2022 Standard (Desktop Experience)

❗ Don’t choose “Server Core” – it has no GUI.

# 8.📌 Step 8: Accept License
Check I accept the license terms
Click Next

# 9.📌 Step 9: Select Installation Type
Choose: Custom: Install Windows only

# 10.📌 Step 10: Select Partition
You'll see your 50GB disk
Click it → Press Next

# 11.📌 Step 11: Let It Install
Wait while Windows installs (may take 5–10 mins).
-->After completing that we will get sconfig box with 15 options,in that we will select exit and commandline option to go to set password.  

# 12.📌 Step 12: Set Admin Password
Enter a strong password:
👉 Example: Admin@123
Press Finish. [<img width="1920" height="1020" alt="Screenshot 2025-07-22 152514" src="https://github.com/user-attachments/assets/1268fae7-5720-48b9-bca3-108437f7b615" />].

#### You need to set password not directly in the user keyboard if you click on input[top left] in the VM box.there we can see keyboard ,in that choode ctrl+alt+del].Then set your vm password. 

✅ Step 13: First Login
On the lock screen, press Ctrl + Alt + Del
Enter the password → You’ll now enter Windows GUI!

# 🎉 Done! You Have Installed Windows Server 2022 (Desktop Version)😊😊😊✅
You’re ready to start Day 2: Active Directory Setup now!
