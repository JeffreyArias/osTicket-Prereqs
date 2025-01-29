<p align="center">
<img src="https://github.com/user-attachments/assets/c46376f6-f693-497c-bce2-87110e834d6a" alt="osTicket logo"/>
</p>

# osTicket Installation Guide: A Step-by-Step Walkthrough

This guide provides a comprehensive, one-of-a-kind approach to installing and configuring the open-source ticketing system, osTicket, on a Windows 10 Virtual Machine within Microsoft Azure. Follow these instructions carefully to ensure a smooth setup process.

---

## **Technologies & Tools Utilized**
- **Microsoft Azure** (Virtual Machine Deployment)
- **Remote Desktop Connection** (RDP)
- **Internet Information Services (IIS)** (Web Server Management)

## **Operating System Used**
- **Windows 10 Pro (Version 21H2)**

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
1. Access the [Azure Portal](https://portal.azure.com/).
2. Create a new Virtual Machine (VM) using **Windows 10 Pro, Version 22H2**.
3. Allocate a minimum of **2 vCPUs** and **16 GB RAM** for optimal performance.
4. Once provisioned, locate the **public IP address** of your VM.
5. Use **Remote Desktop Connection (RDP)** to connect to the VM.

---

### **Step 2: Enabling IIS on Windows 10**
1. Open **Control Panel** → **Programs** → **Turn Windows features on or off**.
2. Locate **Internet Information Services (IIS)** and enable the following components:
   - **World Wide Web Services** → **Application Development Features**:
     - [✔] CGI
   - **Common HTTP Features** (Ensure all options are checked)
3. Apply changes and allow Windows to install IIS.
4. Verify installation by opening a browser and navigating to **127.0.0.1**—you should see the IIS default page.

---

### **Step 3: Installing Required IIS Modules**
1. Install **PHP Manager for IIS** (_PHPManagerForIIS_V1.5.0.msi_).
2. Install **IIS Rewrite Module** (_rewrite_amd64_en-US.msi_).

---

### **Step 4: Setting Up PHP**
1. Create a new folder **C:\PHP**.
2. Download and extract **PHP 7.3.8** (_php-7.3.8-nts-Win32-VC15-x86.zip_) into **C:\PHP**.
3. Install **VC_redist.x86.exe** (Visual C++ Redistributable).

---

### **Step 5: Installing MySQL Database Server**
1. Download and install **MySQL 5.5.62** (_mysql-5.5.62-win32.msi_).
2. Follow the setup wizard:
   - **Select**: _Typical Setup_
   - **Enable**: _Launch Configuration Wizard_
   - **Choose**: _Standard Configuration_
   - **Set Root Password**: `Password1`
3. Complete the installation by executing the final setup step.

---

### **Step 6: Configuring PHP in IIS**
1. Open **IIS Manager** as an Administrator.
2. Navigate to **PHP Manager**.
3. Select **Register new PHP version**, providing the path to **php-cgi.exe** inside **C:\PHP**.
4. Restart IIS to apply changes.

---

### **Step 7: Installing and Configuring osTicket**
1. Extract and copy the **osTicket v1.15.8** "upload" folder into **C:\inetpub\wwwroot**.
2. Rename the folder from **upload** to **osTicket**.
3. Restart IIS and navigate to **Sites** → **Default Web Site** → **osTicket**.
4. Click **Browse *:80** to open the osTicket web installer.

---

### **Step 8: Enabling Required PHP Extensions**
1. In IIS, navigate to **Sites** → **Default Web Site** → **osTicket**.
2. Open **PHP Manager** → **Enable or Disable Extensions**.
3. Enable the following extensions:
   - **php_imap.dll**
   - **php_intl.dll**
   - **php_opcache.dll**
4. Restart IIS after applying changes.

---

### **Step 9: Configuring osTicket Files and Permissions**
1. Navigate to **C:\inetpub\wwwroot\osTicket\include**.
2. Rename **ost-sampleconfig.php** to **ost-config.php**.
3. Adjust file permissions:
   - Right-click **ost-config.php** → **Properties** → **Security**.
   - Click **Advanced** → **Disable Inheritance**.
   - Select **Remove all inherited permissions**.
   - Add a new principal: **Everyone** with **Full Control**.
   - Apply changes.

---

### **Step 10: Setting Up the osTicket Database**
1. Install **HeidiSQL**.
2. Open HeidiSQL and create a new session with:
   - **Username**: `root`
   - **Password**: `Password1`
3. Inside HeidiSQL:
   - Right-click on the left panel → **Create New** → **Database**.
   - Name it `osTicket`.
4. Return to the osTicket web installer and enter the database details:
   - **Database Name**: `osTicket`
   - **Username**: `root`
   - **Password**: `Password1`
5. Complete the osTicket installation.

---

### **Step 11: Finalizing the Installation**
1. Delete the **setup** directory located at:
   - `C:\inetpub\wwwroot\osTicket\setup`
2. Set **ost-config.php** to **Read-Only**.
3. Log in to osTicket from your browser and begin configuring your helpdesk system.

---

### **Congratulations!** 🎉
Your osTicket helpdesk is now fully installed and ready for use. You can now configure support tickets, manage users, and integrate with email systems to streamline customer support operations. Happy ticketing!

---
