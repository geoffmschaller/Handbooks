# AD User Management

## Table Of Contents

- [AD User Management](#ad-user-management)
  - [Table Of Contents](#table-of-contents)
  - [Create a User](#create-a-user)
  - [Delete User](#delete-user)
  - [Modifying Users](#modifying-users)
  - [Moving A User](#moving-a-user)
  - [Renaming A User](#renaming-a-user)
  - [Enabling or Disabling A User](#enabling-or-disabling-a-user)
  - [Find All Locked Out Users](#find-all-locked-out-users)
  - [Unlocking A User](#unlocking-a-user)

---

<div style="page-break-after: always;"></div>

## Create a User

### Using Users and Computers

1. Open Active Directory Users and Computers (dsa.msc). 
2. In the left navigation pane, navigate to the OU or container where you want to create the user object. 
3. Perform one of these actions to open the New Object - User screen:  
   - From the taskbar, click the New User icon. 
   - Right-click an empty space in the main window and select New and then User from the menu. 
   - Right-click the OU or container in which you want to create a new user and select New and then User from the menu. 
4. In the New Object - User screen, specify values for the following fields: 
   - Specify the Full name, by either typing the full name or by filling the First name and Last name fields. 
   - Specify the User logon name in the top field of the two available fields. This will create the userPrincipalName attribute (the combination of the two top fields) and the sAMAccountName attribute (the combination of the two bottom fields, referred to as the Pre-Windows 2000 user log-on name in the user interface). 
5. Click Next >. 
6. In the second New Object - User screen, specify a Password and then confirm it in the second field. Click Next > when done. 
7. In the third New Object - User screen, click Finish.

### Using Powershell

```powershell
New-ADUser -Name [Name] -GivenName [First name] -Surname [Last name] -SamAccountName [Username] -UserPrincipalName [Principal name] -Path [Ou Path] -AccountPassword(Read-Host -AsSecureString "What is the new password?") -Enabled $true
```

### Using Admin Center

1. Open the Active Directory Administrative Center (dsac.exe). 
2. In the left navigation pane, right-click the domain name and select New and then User from the menu. The Create User window appears: 
3. In the Create User screen, specify values for the following fields:  
   1. Specify the Full name, by either typing the full name or by filling the First name and Last name fields. 
   2. Specify the User logon name in the top field of the two available fields. This will create the userPrincipalName attribute (the combination of the two top fields) and the sAMAccountName attribute (the combination of the two bottom fields, referred to as the Pre-Windows 2000 user logon name in the user interface). 
4. Click OK.

---

<div style="page-break-after: always;"></div>

## Delete User

### Using Users and Computers

1. Open Active Directory Users and Computers (dsa.msc). 
2. In the View menu, enable Advanced Features. 
3. In the left navigation pane, navigate to the OU or container where the user object that you intend to delete resides. 
4. From the Action menu, select Find. In the Name field, type the name of the user object you intend to delete and press Enter. From the list of Search results, select the user object: 
5. Right-click the user object and select Properties from the list. 
6. Navigate to the Object tab: 
7. Disable Protect object from accidental deletion (optional). 
8. Click OK to close the Properties window for the object. 
9. Right-click the user object again. This time select Delete from the list. 
10. Click Yes in the Active Directory Domain Services popup window to answer the question Are you sure you want to delete the User named 'user'?

### Using Powershell

```powershell
Remove-ADUser -Identity "CN=User,CN=Users,DC=lucernpub,DC=com"
```

### Using Admin Center

1. Open the Active Directory Administrative Center (dsac.exe). 
2. Perform one of these series of actions:  
   - In the left navigation pane, switch to Tree view. Navigate to the OU or container where the user object that you intend to delete resides. In the main pane, select the user object. 
   - From the main pane menu, under Global Search, type the name of the user object you intend to delete and press Enter. From the list of Global Search results, select the user object. 
3. Right-click the user object and select Properties from the list.
The User window appears: 
4. Disable Protect object from accidental deletion (optional). 
5. Click OK to close the Properties window for the object. 
6. Right-click the user object again. This time, select Delete from the list.
The Delete confirmation popup window appears: 
1. Click Yes in the Delete Confirmation popup window to answer the question Are you sure you want to delete the User user?

---

<div style="page-break-after: always;"></div>

## Modifying Users

### Using Users and Computers

1. Open Active Directory Users and Computers (dsa.msc). 
2. In the left navigation pane, navigate to the OU or container where the user objects reside. 
3. In the main pane, select the user objects by selecting them while holding down the Shift button. 
4. Right-click the objects and select Properties from the menu. 
5. Change the attribute or attributes that you want to modify. 
6. Click OK when you have done this.

### Using Powershell

```powershell
Get-ADUser -ldapfilter "(sAMAccountName=service_*)" | 
Set-ADObject -ProtectedFromAccidentalDeletion $true
```

### Using Admin Center

1. Open the Active Directory Administrative Center (dsac.exe). 
2. In the left navigation pane, select the OU or container to use as the base scope for the filter. 
3. In the main pane, expand the top bar. 
4. Click the Add criteria button: 
5. Add the criteria you want to use to select the user objects you want to modify at once. Use one or more of the built-in filters or scroll down to create a filter based on the user-friendly names of one or more attributes. Click Add to add the filter. When going the last route, you can use matches such as starts with, equals, does not equal, is empty, and is not empty. 
6. In the Search results pane, select all the user objects that match the filter, by selecting one and then pressing Ctrl + A. 
7. In the right task pane, click Properties.
The Multiple Users window appears: 
8. Change the attribute or attributes that you want to modify. 
9. Click OK when you have done this.

---

<div style="page-break-after: always;"></div>

## Moving A User

### Using Users and Computers

1. Open Active Directory Users and Computers (dsa.msc). 
2. In the View menu, enable Advanced Features. 
3. Perform one of these series of actions:  
   - In the left navigation pane, navigate to the OU or container where the user object that you intend to delete resides. In the main pane, select the user object. 
   - From the Action menu, select Find…. In the Name field, type the name of the user object you intend to move, and press Enter. From the list of Search results:, select the user object. 
4. Right-click the user object and select Properties from the list. 
5. Navigate to the Object tab. 
6. Disable Protect object from accidental deletion. 
7. Click OK to close the Properties window for the object. 
8. Right-click the user object again. This time, select Move… from the list. The Move window appears: 
9. In the Move window, navigate to the OU or container where you want to move the user object to, and select it. 
10. Click OK to move the object.

### Using Powershell

```powershell
Move-ADObject -Identity:"CN=User,CN=Users,DC=lucernpub,DC=com" 
-TargetPath:"OU=Organizational Unit,DC=lucernpub,DC=com"
```

### Using Admin Center

1. Open the Active Directory Administrative Center (dsac.exe). 
2. Perform one of these series of actions:  
    - In the left navigation pane, switch to Tree view. Navigate to the OU or container where the user object that you intend to move resides. In the main pane, select the user object. 
    - From the main pane menu, under Global Search, type the name of the user object you intend to move, and press Enter. From the list of Global Search result, select the user object. 
3. Right-click the user object and select Properties from the list. 
4. Disable Protect object from accidental deletion. 
5. Click OK to close the Properties window for the object. 
6. Right-click the user object again. This time, select Move… from the list. The Move window appears: 
7. In the Move window, navigate to the OU or container where you want to move the user object to, and select it. 
8. Click OK to move the object.

---

<div style="page-break-after: always;"></div>

## Renaming A User

### Using Users and Computers

1. Open Active Directory Users and Computers (dsa.msc). 
2. In the View menu, enable Advanced Features. 
3. Perform one of these actions:  
    - In the left navigation pane, navigate to the OU or container where the user object resides. In the main pane, select the user object. 
    - From the Action menu, select Find…. In the Name field, type the name of the user object and press Enter. From the list of Search results:, select the user object. 
4. Right-click the user object and select Rename from the list. 
5. Type the new name for the user object and press Enter. 
6. In the Rename User popup window, type new values for other attributes that you want subsequently renamed: 
7. Click OK.

### Using Powershell

```powershell
Rename-ADObject -Identity "CN=User,CN=Users,DC=lucernpub,DC=com" -NewName "User Account"
```

### Using Admin Center

1. Open the Active Directory Administrative Center (dsac.exe). 
2. Perform one of these actions:  
    - In the left navigation pane, switch to Tree view. Navigate to the OU or container where the user object resides. In the main pane, select the user object. 
    - From the main pane menu, under Global Search, type the name of the user object, and press Enter. From the list of Global Search results, select the user object. 
3. Right-click the user object and select Properties from the list. 
4. In the User window, change one or more of the following fields for the user object:  
   1. In the Account field:  
       - First name 
       - Last name 
       - Full name 
       - User UPN log-on 
       - User SamAccountName log-on 
   2. In the Organization field, change the Display Name. 
5. Click OK.

---

<div style="page-break-after: always;"></div>

## Enabling or Disabling A User

### Using Users and Computers

1. Open Active Directory Users and Computers (dsa.msc). 
2. Perform one of these series of actions:  
   - In the left navigation pane, navigate to the OU or container where the user object resides. In the main pane, select the user object. 
   - From the Action menu, select Find…. In the Name field, type the name of the user object, and press Enter. From the list of Search results:, select the user object. 
3. Right-click the user object and select Enable account or Disable account from the list. 
4. In the Active Directory Domain Services popup window, dismiss the message that says User Object has been disabled or User Object has been enabled by clicking OK.

### Using Powershell

```powershell
# Enable
Enable-ADAccount -Identity "CN=User,CN=Users,DC=lucernpub,DC=com"

# Disable
Disable-ADAccount -Identity "CN=User,CN=Users,DC=lucernpub,DC=com" 
```

### Using Admin Center

1. Open the Active Directory Administrative Center (dsac.exe). 
2. Perform one of these series of actions:  
   1. In the left navigation pane, switch to Tree view. Navigate to the OU or container where the user object resides. In the main pane, select the user object. 
   2. From the main pane menu, under Global Search, type the name of the user object and press Enter. From the list of Global Search results, select the user object. 
3. Right-click the user object and select Properties from the list. 
4. In the top bar of the User window, click the Tasks button. 
5. From the Tasks menu, select Disable or Enable. 
6. Click OK:

---

<div style="page-break-after: always;"></div>

## Find All Locked Out Users

### Using Powershell

```powershell
Search-ADAccount -LockedOut -UsersOnly | Format-Table Name,LockedOut       -AutoSize
```

### Using Admin Center

1. Open the Active Directory Administrative Center (dsac.exe). 
2. In the left navigation pane, select the OU or container to use as the base scope for the filter. 
3. In the main pane, expand the top bar. 
4. Click the Add criteria button. 
5. Select the Users with enabled but locked accounts criteria: 
6. Click Add to add the filter. 
7. The locked-out accounts will be displayed in the main pane.

---

<div style="page-break-after: always;"></div>

## Unlocking A User

### Using Powershell

```powershell
Unlock-ADAccount -Identity "CN=User,CN=Users,DC=lucernpub,DC=com"
```

### Using Admin Center

1. Open the Active Directory Administrative Center (dsac.exe). 
2. In the left navigation pane, navigate to the OU or container where the user objects reside. 
3. In the main pane, select the user object you want to unlock. 
4. Right-click the object and select Properties from the menu. The User window appears: 
5. Click the Unlock account text.  
6. Click OK when you have done this. 

To unlock all locked-out accounts in a certain OU or container, combine the steps from the Finding locked-out accounts recipe with steps 4, 5, and 6.

---