# AD Group Management

## Table Of Contents

- [AD Group Management](#ad-group-management)
  - [Table Of Contents](#table-of-contents)
  - [Creating A Group](#creating-a-group)
  - [Delete A Group](#delete-a-group)
  - [Managing Group Members](#managing-group-members)

---

<div style="page-break-after: always;"></div>

## Creating A Group

### Using Users and Computers

1. Open Active Directory Users and Computers (dsa.msc). 
2. In the left navigation pane, navigate to the OU or Container where you want to create the group object. 
3. Perform one of the following actions to open the New Object - Group screen:
   1. From the taskbar, click the New Group icon. 
   2. Right-click an empty space in the main window and select New; then, select Group from the menu. 
   3. Right-click the OU or Container that you want to create a new group in and select New; then, select Group from the menu. The New Object - Group screen appears: 
4. In the New Object - Group screen, specify values for the following fields: 
   1. Specify the Group Name; the pre-Windows 2000 group name will also be filled, based on the name of the group. 
   2. Specify the Group scope or accept the default Global scope. 
   3. Specify the Group type or accept the default Security type. 
5. Click OK to create the group.

### Using Powershell

```powershell
New-ADGroup -GroupCategory Security -GroupScope Global -Name "Group" -Path "OU=Organizational Unit,DC=lucernpub,DC=com" -SamAccountName "Group"
```

### Using Admin Center

1. Open the Active Directory Administrative Center (dsac.exe). 
2. In the left navigation pane, right-click the domain name and select New; then, select Group from the menu. The Create Group screen appears: 
3. In the Create Group screen, specify values for the following fields: 
   1. Specify the Group name; the Group (sAMAccountName) name will also be filled, based on the name of the group. 
   2. Specify the Group scope or accept the default Global scope. 
   3. Specify the Group type or accept the default Security type. 
4. Click OK to create the group.

---

<div style="page-break-after: always;"></div>

## Delete A Group

### Using Users and Computers

1. Open Active Directory Users and Computers (dsa.msc). 
2. In the View menu, enable Advanced Features. 
3. Perform one of these series of actions:  
   1. In the left navigation pane, navigate to the OU or container where the group that you intend to delete resides. Then, in the main menu pane, select the group. 
   2. From the Action menu, select Find…. In the Name field, type in the name of the group you intend to delete, and then press Enter. From the list of Search results, select the group. 
4. Right-click the group and select Properties from the list. The Group Properties window appears: 
5. Navigate to the Object tab. 
6. Disable Protect object from accidental deletion. 
7. Click OK to close the Properties window for the object. 
8. Right-click the group again; this time, select Delete from the list. 
9. Click Yes in the Active Directory Domain Services popup window to answer Are you sure you want to delete the group named 'group'?.

### Using Powershell

```powershell
Remove-ADObject -Identity "CN=Group,OU=Organizational Unit,DC=lucernpub,DC=com"
```

### Using Admin Center

1. Open the Active Directory Administrative Center (dsac.exe). 
2. Perform one of these series of actions:  
   1. In the left navigation pane, switch to the Tree view. Navigate to the OU or container where the group that you intend to delete resides. In the main menu pane, select the group. 
   2. From the main menu pane, under Global Search, type in the name of the group you intend to delete, and press Enter. From the list of Global Search results, select the group. 
3. Right-click the group and select Properties from the list. 
4. Disable Protect object from accidental deletion. 
5. Click OK to close the Properties window for the object. 
6. Right-click the group again; this time, select Delete from the list. 
7. Click Yes in the Delete confirmation popup window to answer Are you sure you want to delete the Group group?.

---

<div style="page-break-after: always;"></div>

## Managing Group Members

### Using Users and Computers

1. Open Active Directory Users and Computers (dsa.msc). 
2. Perform one of these series of actions:  
   1. In the left navigation pane, navigate to the OU or container where the user that you intend to manage group memberships for resides. In the main menu pane, select the user. 
   2. From the Action menu, select Find…. In the Name field, type in the name of the user that you intend to manage group memberships for, and then press Enter. From the list of Search results, select the user. 
3. Right-click the user object and select Add to a group… from the menu. The Select Groups window appears: 
4. In the Select Groups window, type in the name of the group that you want to add the user account to, otherwise, click the Advanced button to search for the group. 
5. Click Check Names. 
6. Click OK to add the user to the group.

```powershell
# Add
Add-ADGroupMember -Identity "CN=Group,OU=Organizational Unit,DC=lucernpub,DC=com" -Members "User"


```

### Using Admin Center

1. Open the Active Directory Administrative Center (dsac.exe). 
2. Perform one of these series of actions:  
   1. In the left navigation pane, switch to the Tree view. Navigate to the OU or container where the user object resides. In the main menu pane, select the user object. 
   2. From the main pane menu, under Global Search, type in the name of the user object, and then press Enter. From the list of Global Search results, select the user object. 
3. Right-click the user object and select Add to group… from the list. 
4. In the Select Groups window, type in the name of the group that you want to add the user account to or click the Advanced button to search for the group. 
5. Click Check Names. 
6. Click OK to add the user to the group.