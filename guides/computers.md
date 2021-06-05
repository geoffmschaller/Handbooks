# AD Computer Management

## Table Of Contents

- [AD Computer Management](#ad-computer-management)
  - [Table Of Contents](#table-of-contents)
  - [Create A Computer](#create-a-computer)
  - [Deleting A Computer](#deleting-a-computer)
  - [Join A Computer To A Domain](#join-a-computer-to-a-domain)
  - [Renaming a Computer](#renaming-a-computer)

---

<div style="page-break-after: always;"></div>

## Create A Computer 

### Using Users and Computers

1. Open Active Directory Users and Computers (dsa.msc). 
2. In the left navigation pane, navigate to the OU or container where you want to create the computer object. 
3. Perform one of the following actions to open the New Object – Computer screen:  
   1. From the taskbar, click the New Computer icon. 
   2. Right-click an empty space in the main window and select New; then, select Computer from the menu. 
   3. Right-click the OU or container that you want to create a new computer in and select New; then, select Computer from the menu. 
   4. The New Object – Computer screen appears: 
4. In the New Object – Computer screen, specify values for the following fields:  
   1. Specify the Computer name. 
   2. Change the Computer name (pre-Windows 2000) if you need it to be different from the automatically-generated value, based on the value of the Computer name. 
5. Click OK when you are done.

### Using Powershell

```powershell
New-ADComputer -Name "Computer" -sAMAccountName "Computer" -Path "CN=Computers,DC=lucernpub,DC=com"
```

### Using Admin Center

1. Open the Active Directory Administrative Center (dsac.exe). 
2. In the left navigation pane, right-click the domain name and select New. Then, select Computer from the menu. The Create Computer screen appears: 
3. In the Create Computer screen, specify values for the following fields:  
   1. Specify the Computer name. 
   2. Change the Computer name (pre-Windows 2000) if you need it to be different from the automatically-generated value, based on the value of the Computer name. 
4. Click OK.

---

<div style="page-break-after: always;"></div>

## Deleting A Computer

### Using Users and Computers

1. Open Active Directory Users and Computers (dsa.msc). 
2. In the View menu, enable Advanced Features. 
3. Perform one of these series of actions:  
   1. In the left navigation pane, navigate to the OU or container where the computer object that you intend to delete resides. In the main menu pane, select the computer object. 
   2. From the Action menu, select Find. In the Name field, type the name of the computer object that you intend to delete, and then press Enter. From the list of Search results, select the computer object. 
4. Right-click the computer object and select Properties from the list. 
5. Navigate to the Object tab. 
6. Disable Protect object from accidental deletion. 
7. Click OK to close the Properties window for the object. 
8. Right-click the computer object again; this time, select Delete from the list.
The Active Directory Domain Services popup window appears: 
9. Click Yes in the Active Directory Domain Services popup window in order to answer the Are you sure you want to delete the Computer named 'Computer'? question.

```powershell
Remove-ADComputer -Identity "CN=Computer,CN=Computers,DC=lucernpub,DC=com"
```

### Using Admin Center

1. Open the Active Directory Administrative Center (dsac.exe). 
2. Perform one of these series of actions:  
   1. In the left navigation pane, switch to the Tree view. Navigate to the OU or container where the computer object that you intend to delete resides. In the main menu pane, select the computer object. 
   2. From the main menu pane, under Global Search, type the name of the computer object that you intend to delete, and then press Enter. From the list of Global Search results, select the computer object. 
3. Right-click the computer object and select Properties from the list. The Computer properties window appears: 
4. Disable Protect object from accidental deletion. 
5. Click OK to close the Properties window for the object. 
6. Right-click the computer object again; this time, select Delete from the list: 
7. Click Yes in the Delete Confirmation popup window to answer the Are you sure you want to delete

---

<div style="page-break-after: always;"></div>

## Join A Computer To A Domain

### Using the GUI

1. Press the Start flag and either click the cog in the left-side of the Start Menu to access Settings, or type Settings and click the Settings trusted Microsoft Store app from the results. Alternatively, press the Start button on your keyboard and the X key simultaneously, and select Settings from the context menu. The Settings trusted Microsoft Store app appears: 
2. In the Windows Settings window, click Accounts. 
3. In the left navigation pane, click Access work or school. 
4. In the main menu pane, click + Connect. 
5. In the Microsoft Account window, click Join this device to a local Active Directory domain under Alternative Options. 
6. In the Join a Domain window, type the DNS domain name or the NetBIOS name of the Active Directory environment. Then, click Next. 
7. Type the credentials in the Windows Security popup message that asks to enter your domain account information to verify that you have permission to connect to the domain. Then, click OK. 
8. In the Restart your PC window, click Restart now to restart

### Using Powershell

```powershell
Add-Computer -DomainName lucernpub.com -Credential LUCERNPUB\Administrator
 Restart-Computer
```

---

<div style="page-break-after: always;"></div>

## Renaming a Computer

### Using Windows Settings

1. Press the Start flag and either click the cog in the left-side of the Start Menu to access Settings, or type Settings and click the Settings trusted Microsoft Store app from the results. Alternatively, press Start + X on your keyboard and select Settings from the context menu. 
2. In the Settings window, click System. 
3. In the left navigation pane, click About. 
4. In the main menu pane, click the Rename this PC button under Device Specifications. The Rename your PC window appears: 
5. In the Rename your PC window, type the new hostname for the device. Then, click Next. 
6. Click Restart now.

### Using Powershell

```powershell
Rename-Computer NewComputerName
Restart-Computer
```