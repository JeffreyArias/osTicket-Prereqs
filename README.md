<p align="center">
<img src="https://github.com/user-attachments/assets/c46376f6-f693-497c-bce2-87110e834d6a" alt="osTicket logo"/>
</p>

# osTicket Prerequisites and Installation Guide: A Step-by-Step Walkthrough

This guide provides a comprehensive, one-of-a-kind approach to installing and configuring the open-source ticketing system, osTicket, on a Windows 10 Virtual Machine within Microsoft Azure. Follow these instructions carefully to ensure a smooth setup process.

---

## **Technologies & Tools Utilized**
- **Microsoft Azure** (Virtual Machine Deployment)
- **Remote Desktop Connection** (RDP)
- **Internet Information Services (IIS)** (Web Server Management)

## **Operating System Used**
- **Windows 10 Pro (Version 22H2)**

## **Essential Components for Installation**
Ensure the following components are readily available for a successful setup:
- Microsoft Azure Virtual Machine
- Internet Information Services (IIS)
- PHP Manager
- IIS Rewrite Module
- Visual C++ Redistributable (VC Redist)
- MySQL Database Server
- HeidiSQL Database Management Tool
- osTicket v1.15.8
- **[Download Required Files Here](https://drive.google.com/drive/u/0/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6)**

---

## **Installation and Configuration Steps**

### **Step 1: Setting Up the Virtual Machine**
Access the [Azure Portal](https://portal.azure.com/).
Create a new Virtual Machine (VM).
Select **Windows 10 Pro, Version 22H2** and allocate a minimum of **2 vCPUs** and **16 GB RAM** for optimal performance.
![Select Win10](https://github.com/user-attachments/assets/8e9dce51-4ff6-46ee-869a-eb9d11ad2dc0)
Once provisioned, locate the **public IP address** of your VM.
![Public IP Address](https://github.com/user-attachments/assets/172583ce-971c-4d52-b202-6e4cbf39d414)
Use **Remote Desktop Connection (RDP)** to connect to the VM.
![RDP](https://github.com/user-attachments/assets/82ee1949-1b4d-42e5-bb69-e85222f62b61)


---

### **Step 2: Enabling IIS on Windows 10**
Open **Control Panel** → **Programs** → **Turn Windows features on or off**.
Locate **Internet Information Services (IIS)** and enable the following components:
**World Wide Web Services** → **Application Development Features**:
[✔] CGI
![IIS - CGI](https://github.com/user-attachments/assets/574922e5-cbbf-4b79-a347-6ff0498bd3b8)
**Common HTTP Features** (Ensure all options are checked)
![Common HTTP Features](https://github.com/user-attachments/assets/2c569e90-6c24-4ea3-a5a5-58f13e30bd2b)
Apply changes and allow Windows to install IIS.
Verify installation by opening a browser and navigating to **127.0.0.1**—you should see the IIS default page.
![IIS Default Page](https://github.com/user-attachments/assets/92cc812e-cb14-4393-a4f8-92d90b490079)

---

### **Step 3: Installing Required IIS Modules**
Install **PHP Manager for IIS** (_PHPManagerForIIS_V1.5.0.msi_).
Install **IIS Rewrite Module** (_rewrite_amd64_en-US.msi_).
![PHP Manager - IIS Rewrite Module](https://github.com/user-attachments/assets/4c32cf54-ef11-469c-bb00-15e936f1dc22)


---

### **Step 4: Setting Up PHP**
Create a new folder **C:\PHP**.
Download and extract **PHP 7.3.8** (_php-7.3.8-nts-Win32-VC15-x86.zip_) into **C:\PHP**.
Install **VC_redist.x86.exe** (Visual C++ Redistributable).
![PHP Extract](https://github.com/user-attachments/assets/31aa6e3c-9c13-4a2b-a5dd-282aba57f849)

---

### **Step 5: Installing MySQL Database Server**
Download and install **MySQL 5.5.62** (_mysql-5.5.62-win32.msi_).
Follow the setup wizard:
**Select**: _Typical Setup_
![Typical Setup](https://github.com/user-attachments/assets/1fa7060d-f913-4da7-b7fe-1a3c66e8791e)
**Enable**: _Launch Configuration Wizard_
![Launch Config Wizard](https://github.com/user-attachments/assets/378f4fd2-be15-4c11-a61c-6a886d96a4f3)
**Choose**: _Standard Configuration_
![Standard Config](https://github.com/user-attachments/assets/3c7da65a-2249-4a53-8885-3c2c25386b8a)
**Set Root Password**: `Password1`
![Set Root Password](https://github.com/user-attachments/assets/54abe4cf-a96b-4656-8276-85cd2a0e73c5)
Complete the installation by executing the final setup step.

---

### **Step 6: Configuring PHP in IIS**
Open **IIS Manager** as an Administrator.
Navigate to **PHP Manager**.
![IIS PHP Manager](https://github.com/user-attachments/assets/47b4e1b9-97df-42d9-8ac7-1ad5b43fb9b3)
Select **Register new PHP version**, providing the path to **php-cgi.exe** inside **C:\PHP**.
![Register New PHP](https://github.com/user-attachments/assets/60394afb-323c-4dfb-b0e3-be4abc05aa4d)
Restart IIS to apply changes.

---

### **Step 7: Installing and Configuring osTicket**
Extract and copy the **osTicket v1.15.8** "upload" folder into **C:\inetpub\wwwroot**.
Rename the folder from **upload** to **osTicket**.
![INETPUB](https://github.com/user-attachments/assets/94938766-56f1-4d23-a59a-3278eeef066c)
Restart IIS and navigate to **Sites** → **Default Web Site** → **osTicket**.
Click **Browse *:80** to open the osTicket web installer.
![IIS - osTicket Browse 80](https://github.com/user-attachments/assets/f47571af-5bb8-4f05-9ccc-552ac955c5db)

---

### **Step 8: Enabling Required PHP Extensions**
In IIS, navigate to **Sites** → **Default Web Site** → **osTicket**.
Open **PHP Manager** → **Enable or Disable Extensions**.
![Open PHP Manager](https://github.com/user-attachments/assets/95264703-7dc8-4175-8576-d2580c0a11bf)
Enable the following extensions:
**php_imap.dll**
**php_intl.dll**
**php_opcache.dll**
![Enable 3 Extensions](https://github.com/user-attachments/assets/3c7ddb9b-cf20-458d-ba30-00ca50decbc8)
Restart IIS after applying changes.

---

### **Step 9: Configuring osTicket Files and Permissions**
Navigate to **C:\inetpub\wwwroot\osTicket\include**.
Rename **ost-sampleconfig.php** to **ost-config.php**.
![Rename ost-sampleconfig](https://github.com/user-attachments/assets/f855b26f-a07e-415c-b766-60e47a3b375f)
Adjust file permissions:
   - Right-click **ost-config.php** → **Properties** → **Security**.
![Right-Click ost-config - Properties](https://github.com/user-attachments/assets/68cead07-0017-420b-bc00-cd59db5349e7)
![Click Security - Advanced](https://github.com/user-attachments/assets/b32df2a0-acc2-467a-a2df-00b23313bc68)
   - Click **Advanced** → **Disable Inheritance**.
![Disable Inheritance](https://github.com/user-attachments/assets/7dc4c90c-d835-40db-ba07-a53cd5ee45ad)
   - Select **Remove all inherited permissions**.
![Remove all Inherited Permissions](https://github.com/user-attachments/assets/dfb9a59b-01e5-4abb-bcbe-af1ddd371952)
   - Add a new principal: **Everyone** with **Full Control**.
![Add New Principal](https://github.com/user-attachments/assets/e6427de8-cca9-4313-b7d4-9c3b8029c63f)
![Everyone with Full Control](https://github.com/user-attachments/assets/1b711de1-1e19-47fb-9eb8-67fae962a52e)
![Everyone with Full Control 2](https://github.com/user-attachments/assets/d2af5e2f-047d-4054-ab3f-050ba635122b)
   - Apply changes.

---

### **Step 10: Setting Up the osTicket Database**
Install **HeidiSQL**.
Open HeidiSQL and create a new session with:
   - **Username**: `root`
   - **Password**: `Password1`
![HeidiSQL user pass](https://github.com/user-attachments/assets/c444f4a4-eb13-4b67-9183-f44b712daca8)
Inside HeidiSQL:
   - Right-click on the left panel → **Create New** → **Database**.
   - Name it `osTicket`.
![Create New Database](https://github.com/user-attachments/assets/99c6bfb3-c180-45ff-93dc-772421a86d39)
Return to the osTicket web installer and enter the database details:
   - **Database Name**: `osTicket`
   - **Username**: `root`
   - **Password**: `Password1`
![osTicket Web Installer Name User Pass](https://github.com/user-attachments/assets/71ea2776-6c48-4465-ae14-10f400ae17d3)
Complete the osTicket installation.

---

### **Step 11: Finalizing the Installation**
Delete the **setup** directory located at:
   - `C:\inetpub\wwwroot\osTicket\setup`
Set **ost-config.php** to **Read-Only**.
Log in to osTicket from your browser and begin configuring your helpdesk system.

---

### **Congratulations!** 🎉
Your osTicket helpdesk is now fully installed and ready for use. You can now configure support tickets, manage users, and integrate with email systems to streamline customer support operations. Happy ticketing!

---
