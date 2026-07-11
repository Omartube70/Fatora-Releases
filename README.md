# 📥 Installation Guide - Fatora POS System

## 🎯 Welcome to Fatora Point of Sale System

This guide will help you install and run the Fatora system step by step in an easy and clear way.

---

## 📋 Basic Requirements

### Minimum Requirements:
- 💻 **Operating System**: Windows 10 / Windows 11
- ⚙️ **Processor**: Intel Core i3 or equivalent
- 🧠 **Memory**: 4 GB RAM
- 💾 **Free Space**: 1 GB on hard disk
- 🌐 **Internet Connection**: Required for initial installation only

### Recommended:
- 💻 **Operating System**: Windows 10 Pro / Windows 11 Pro
- ⚙️ **Processor**: Intel Core i5 or better
- 🧠 **Memory**: 8 GB RAM
- 💾 **Free Space**: 2 GB
- 🖨️ **Thermal Printer**: For invoice printing (optional)
- 📟 **USB Barcode Scanner**: For barcode reading (optional)

---

## 📦 Installation Steps

### Step 1️⃣: Download Files

1. Go to the [Releases](https://github.com/Omartube70/Fatora/releases) page
2. Download the latest version files:
   - `Fatora-Setup-v1.0.0.zip` (Main installation file)
   - `Fatora-Database-Scripts.zip` (Database files)

### Step 2️⃣: Install Prerequisites

**a) Install .NET Framework 4.8**

1. Download .NET Framework 4.8 from:
   ```
   https://dotnet.microsoft.com/download/dotnet-framework/net48
   ```

2. Run the installation file
3. Follow the instructions until installation is complete
4. Restart your computer if prompted

**b) Install SQL Server 2019 Express**

1. Download SQL Server 2019 Express from:
   ```
   https://www.microsoft.com/sql-server/sql-server-downloads
   ```

2. Choose **Express Edition** (completely free)

3. In the installation screen:
   - Choose **Basic**
   - Accept the license terms
   - Choose installation folder (or leave default)
   - Wait until download and installation complete

4. **Very Important**: Save connection information:
   ```
   Server name: (local)\SQLEXPRESS
   or: localhost\SQLEXPRESS
   ```

5. Optional (but recommended): Download and install **SQL Server Management Studio (SSMS)**:
   ```
   https://aka.ms/ssmsfullsetup
   ```

### Step 3️⃣: Extract Files

1. Extract `Fatora-Setup-v1.0.0.zip` to a folder (e.g., `C:\Program Files\Fatora`)
2. Extract `Fatora-Database-Scripts.zip` to a temporary folder

### Step 4️⃣: Setup Database

**Method 1: Automatic Installation (Easiest) ⭐**

1. Copy file `Fatora.sql` from `Database Scripts` folder
2. Paste it in the program folder (same folder as `Fatora_UI.exe`)
3. Run the program `Fatora_UI.exe`
4. Database setup wizard will appear automatically
5. Enter connection information:
   ```
   Server: (local)\SQLEXPRESS
   Windows Authentication: ✓ (Enabled)
   ```
6. Click "Create Database"
7. Wait until the process completes

**Method 2: Manual Installation**

If you're familiar with SQL Server:

1. Open **SQL Server Management Studio (SSMS)**
2. Connect to: `(local)\SQLEXPRESS`
3. Open file `Fatora.sql`
4. Press F5 to execute the script
5. Verify that database `FatoraDB` appears in the list

### Step 5️⃣: Run the Program

1. Open the installation folder
2. Run `Fatora_UI.exe`
3. In the first login screen:
   ```
   Username: admin
   Password: admin123
   ```

4. **Very Important**: Change the password immediately!
   - Go to "User Management"
   - Select user `admin`
   - Change password to a strong one

### Step 6️⃣: Activation (If Required)

If activation is requested:

1. Activation window will appear
2. **For personal or trial use**:
   - Click "Skip" or "Trial Mode"
   - You can use without restrictions

3. **For commercial use**:
   - Contact support to get a license key
   - Enter the key in the activation window

---

## ✅ Verify Installation

To ensure everything works correctly:

### 1. Test Database Connection
- Program should open without errors
- If connection error appears, refer to "Troubleshooting" section below

### 2. Test Basic Functions
- ✅ Add new product
- ✅ Create test invoice
- ✅ View reports
- ✅ Manage users

### 3. Test Printer (If Available)
- Go to Settings
- Select printer
- Print test invoice

### 4. Test Barcode Scanner (If Available)
- Open Cashier screen
- Scan any product
- Should appear in purchase list

---

## 🔧 Troubleshooting

### ❌ Issue: "Cannot connect to database"

**Solution 1: Make sure SQL Server is running**
```
1. Press Windows + R
2. Type: services.msc
3. Search for: SQL Server (SQLEXPRESS)
4. Make sure Status: Running
5. If stopped, right-click > Start
```

**Solution 2: Check server name**
```
1. Open SQL Server Configuration Manager
2. Go to SQL Server Network Configuration
3. Make sure TCP/IP is enabled
```

**Solution 3: Recreate database**
```
1. Delete FatoraDB database if it exists
2. Run Fatora.sql script again
```

### ❌ Issue: "Access Denied" or Permission Error

**Solution:**
```sql
-- In SQL Server Management Studio, execute:

USE master;
GO

CREATE LOGIN [FatoraUser] 
WITH PASSWORD = 'YourStrongPassword123!';
GO

USE FatoraDB;
GO

CREATE USER [FatoraUser] FOR LOGIN [FatoraUser];
GO

ALTER ROLE db_datareader ADD MEMBER [FatoraUser];
ALTER ROLE db_datawriter ADD MEMBER [FatoraUser];
GRANT EXECUTE TO [FatoraUser];
GO
```

### ❌ Issue: "Missing .NET Framework"

**Solution:**
```
1. Download .NET Framework 4.8 from official link
2. Run the file and wait until installation completes
3. Restart computer
4. Try running the program again
```

### ❌ Issue: Barcode Scanner Not Working

**Solution:**
```
1. Make sure scanner is connected to USB port
2. Open Notepad and test scanner - should type numbers
3. In the program:
   - Place cursor on "Search by Barcode" field
   - Scan any product
4. If doesn't work, try another USB port
```

### ❌ Issue: Printer Doesn't Print

**Solution:**
```
1. Make sure printer driver is installed
2. In Windows:
   - Settings > Devices > Printers
   - Make sure printer is connected
3. In the program:
   - Settings > Print Settings
   - Select correct printer
   - Adjust paper size
4. Print test page from Windows first
```

### ❌ Issue: Program is Slow

**Solution:**
```
1. Make sure:
   - Enough disk space available
   - Other heavy programs closed
   - No viruses (use Windows Defender)

2. Database maintenance:
   - In SSMS, execute:
     DBCC CHECKDB (FatoraDB);
     ALTER INDEX ALL ON FatoraDB REBUILD;
```

---

## 🔄 Updates

### How to Update to Newer Version:

1. **Save database backup**:
   ```sql
   BACKUP DATABASE FatoraDB 
   TO DISK = 'C:\Backups\FatoraDB_Backup.bak'
   WITH FORMAT, COMPRESSION;
   ```

2. Download new version from Releases

3. Close old program

4. Extract new files over old ones

5. Run program - it will automatically update database if needed

6. Verify everything works correctly

---

## 💾 Backup and Restore

### Backup (Very Important! 🔴)

**Quick Method (From Inside Program)**:
```
1. Go to Settings
2. Select "Backup"
3. Specify path and name
4. Click "Create Backup"
```

**Professional Method (From SQL Server)**:
```sql
-- Full backup
BACKUP DATABASE FatoraDB 
TO DISK = 'C:\Backups\FatoraDB_Full_2026-07-11.bak'
WITH FORMAT, COMPRESSION, DESCRIPTION = 'Full backup';

-- Differential backup (faster)
BACKUP DATABASE FatoraDB 
TO DISK = 'C:\Backups\FatoraDB_Diff_2026-07-11.bak'
WITH DIFFERENTIAL, COMPRESSION;
```

**Schedule Automatic Backups**:
```
1. Open SQL Server Management Studio
2. Object Explorer > SQL Server Agent
3. Jobs > New Job
4. Add step executing BACKUP command
5. Schedule > Set schedule (e.g., daily at 11 PM)
```

### Restore

**From Inside Program**:
```
1. Settings > Restore Backup
2. Select .bak file
3. Click "Restore"
4. Restart program
```

**From SQL Server**:
```sql
-- Close all connections first
USE master;
ALTER DATABASE FatoraDB SET SINGLE_USER WITH ROLLBACK IMMEDIATE;

-- Restore backup
RESTORE DATABASE FatoraDB 
FROM DISK = 'C:\Backups\FatoraDB_Full_2026-07-11.bak'
WITH REPLACE, RECOVERY;

-- Reopen database
ALTER DATABASE FatoraDB SET MULTI_USER;
```

---

## 🛡️ Security Tips

### 🔒 Data Protection

1. **Change default password immediately**
   ```
   admin / admin123 → Strong password
   ```

2. **Use strong passwords**:
   - At least 8 characters
   - Upper and lower case letters
   - Numbers and symbols
   - Good example: `P@ssw0rd2026!`

3. **Regular backups**:
   - At least daily
   - Save in safe place (not on same device)
   - Use cloud service or external drive

4. **Network protection**:
   - Don't open SQL Server ports to internet
   - Use Firewall
   - Restrict access to authorized devices only

5. **User permissions**:
   - Give each employee limited permissions according to role
   - Example: Cashier = sales only, no financial reports

6. **Review logs**:
   - Review operation logs regularly
   - Check for any unusual activity

---

## 📞 Technical Support

### 🆘 Need Help?

**Available Support Options**:

1. **Full Documentation**
   - Review [README.md](./README_EN.md) for more details
   - Complete user guide (coming soon)

2. **FAQ**
   - Visit [Wiki](https://github.com/Omartube70/Fatora/wiki) page
   - Search for your question first

3. **Technical Issues**
   - Open [New Issue](https://github.com/Omartube70/Fatora/issues)
   - Explain problem in detail
   - Attach screenshots if possible

4. **Direct Contact**
   - 📧 Email: support@fatora.com
   - 💬 Forum: (coming soon)
   - 📱 WhatsApp: (for paid support)

### Before requesting support, prepare:

```
✅ Program version (from: About)
✅ Windows version (from: Settings > System > About)
✅ SQL Server version (from: SELECT @@VERSION)
✅ Detailed problem description
✅ Screenshots of error message
✅ Steps to reproduce problem
```

---

## 📚 Additional Resources

### Tutorial Videos (YouTube)
```
🎥 Coming soon:
   - Installation step by step
   - How to use cashier system
   - Inventory and supplier management
   - Creating reports
```

### Official Documentation
- [Complete User Guide](https://fatora.com/docs) (coming soon)
- [API Documentation](https://fatora.com/api) (for developers)
- [Best Practices Guide](https://fatora.com/best-practices)

### Community
- [Discord Server](https://discord.gg/fatora) (coming soon)
- [Telegram Group](https://t.me/fatora) (coming soon)
- [Facebook Page](https://fb.com/fatora) (coming soon)

---

## ✨ Additional Features (Optional)

### 🖨️ Setting Up Thermal Printer

**Supported Printers**:
- Epson TM-T20
- XPrinter XP-80
- Any printer supporting ESC/POS

**Setup Steps**:
1. Install printer driver from included disk
2. In Windows: Control Panel > Devices and Printers
3. Make sure printer appears
4. In Fatora:
   - Settings > Printing
   - Select printer
   - Select paper type (80mm or 58mm)
   - Test print

### 📟 Setting Up Barcode Scanner

**Supported Types**:
- USB Barcode Scanner (any type)
- Wireless (Bluetooth/Wireless)

**Setup Steps**:
1. Connect scanner to USB port
2. Windows will recognize it automatically (as keyboard)
3. No additional drivers needed
4. Test in Notepad first
5. In Fatora: Start selling and use scanner directly!

**Note**: Most barcode scanners don't need any setup, just plug and use!

### 🔌 Connect Customer Display

```
Coming soon - LCD and LED display support will be added
```

---

## 🎓 Quick Tutorials

### Tutorial 1: Your First Invoice

```
1. Run program and log in
2. Click "Cashier" from main menu
3. Add product (or scan barcode)
4. Enter quantity (if more than 1)
5. Click "Add to Cart"
6. Repeat for other products
7. Choose payment method (Cash/Visa)
8. Enter amount paid
9. Click "Complete Sale"
10. Print invoice!
```

### Tutorial 2: Add New Product

```
1. Menu > Products
2. Click "+ New Product"
3. Fill data:
   - Product name
   - Barcode (or will be auto-generated)
   - Buy price
   - Sell price
   - Initial quantity
   - Category
4. Click "Save"
5. Ready for sale!
```

### Tutorial 3: Create Sales Report

```
1. Menu > Reports
2. Select "Sales Report"
3. Set period (from - to)
4. Choose filters (optional):
   - Specific cashier
   - Payment method
   - Specific product
5. Click "Show Report"
6. Print or save as PDF
```

---

## 🚀 Quick Start (60 seconds!)

```
⚡ Try the system in less than a minute:

1. ✅ Install .NET Framework 4.8
2. ✅ Install SQL Server Express
3. ✅ Download Fatora and run it
4. ✅ Wizard will set up database automatically
5. ✅ Log in with admin / admin123
6. ✅ Start selling!

🎉 Congratulations! Ready now!
```

---

## 📊 Installation Statistics

### Average Installation Times:

| Phase | Expected Time |
|-------|--------------|
| Download Files | 5-10 minutes |
| Install .NET Framework | 2-5 minutes |
| Install SQL Server | 10-15 minutes |
| Setup Database | 2-3 minutes |
| Test System | 5 minutes |
| **Total** | **25-40 minutes** |

*Note: Times are approximate and depend on internet speed and computer*

---

## 📝 Final Checklist

Before starting actual use, make sure:

### ✅ Checklist:

- [ ] ✅ Windows 10/11 updated
- [ ] ✅ .NET Framework 4.8 installed
- [ ] ✅ SQL Server running correctly
- [ ] ✅ FatoraDB database exists
- [ ] ✅ Program opens without errors
- [ ] ✅ Login works
- [ ] ✅ Admin password changed
- [ ] ✅ Test product added
- [ ] ✅ Test invoice works
- [ ] ✅ Printer connected (if exists)
- [ ] ✅ Barcode scanner works (if exists)
- [ ] ✅ Backup created
- [ ] ✅ User permissions set

### If all points are ✅ you're ready! 🎉

---

<div align="center">

## 🎊 Congratulations! Installation Successful

**Now you're ready to use Fatora POS**

---

### Like the system?

⭐ **Don't forget to star on GitHub!**

[⭐ Star this project](https://github.com/Omartube70/Fatora)

---

**Made with ❤️ in Egypt**

📧 support@fatora.com  |  🌐 www.fatora.com  |  📱 @FatoraPOS

---

**Last Updated**: July 11, 2026  
**Version**: 1.0.0

</div>
