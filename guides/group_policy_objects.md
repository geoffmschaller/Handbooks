# AD Group Policy Object Management

## Table Of Contents

- [AD Group Policy Object Management](#ad-group-policy-object-management)
  - [Table Of Contents](#table-of-contents)
  - [Creating A GPO](#creating-a-gpo)
  - [Copying A GPO](#copying-a-gpo)
  - [Deleting A GPO](#deleting-a-gpo)
  - [Modifying GPO Settings](#modifying-gpo-settings)
  - [Adding Logon Scripts](#adding-logon-scripts)
  - [Installing Applications](#installing-applications)
  - [Linking A GPO to an OU](#linking-a-gpo-to-an-ou)
  - [Blocking Inheritance](#blocking-inheritance)
  - [Enforcing A GPO](#enforcing-a-gpo)
  - [Applying Security Filters](#applying-security-filters)
  - [Creating and Applying WMI Filters](#creating-and-applying-wmi-filters)
  - [Configuring Loopback Processing](#configuring-loopback-processing)

--- 

<div style="page-break-after: always;"></div>
 
## Creating A GPO

### Using Group Policy Manager

1. Open the Group Policy Management Console (gpmc.msc). 
2. In the left navigation pane, expand the Forest node. 
3. Expand the Domains node, and then navigate to the domain where you want to create the GPO. 
4. Expand the domain name and select the Group Policy Objects node: 
5. Right-click the Group Policy Objects node and select New from the menu. 
6. In the New GPO popup window, enter the name of the GPO. Make sure that you don't select Starter GPOs. 
7. Click OK to create the GPO.  
 
You now have a GPO. However, it doesn't have any settings and it isn't linked—at least not yet.

### Using Powershell

```powershell
New-GPO -Name "New GPO Name"
```

---

<div style="page-break-after: always;"></div>

## Copying A GPO

### Using Group Policy Manager

1. Open the Group Policy Management Console (gpmc.msc). 
2. In the left navigation pane, expand the Forest node. 
3. Expand the Domains node, and then navigate to the domain where you want to copy a GPO. 
4. Expand the domain name and then expand the Group Policy Objects node. 
5. Locate the GPO that you want to copy. 
6. Right-click the GPO and select Copy from the menu. 
7. Right-click the Group Policy Objects node and select Paste from the menu. The Copy GPO popup window appears: 
8. In the Copy GPO popup window, select Preserve the existing permissions. of the GPO or Use the default permissions for new GPOs. 
9. In the Copy progress window, click OK to acknowledge that copying has succeeded. 
10. The new GPO is now named Copy of…, referencing the source GPO name. Right-click the GPO in the left navigation menu and select Rename from the menu. 
11. Enter the name of the GPO. Press Enter when done.

### Using Powershell

```powershell
Copy-GPO -Sourcename "Existing GPO Name" -TargetName "New GPO Name"
```

---

<div style="page-break-after: always;"></div>

## Deleting A GPO

### Using Group Policy Manager 

1. Open the Group Policy Management Console (gpmc.msc). 
2. In the left navigation pane, expand the Forest node. 
3. Expand the Domains node, and then navigate to the domain where you want to delete the GPO. 
4. Expand the domain name, and then expand the Group Policy Objects node. 
5. Locate the GPO that you want to delete. 
6. Select the GPO. 
7. In the main pane, on the Scope tab, check to see that the GPO is not linked to any GPO by inspecting the field for The following sites, domains and OUs are linked to this GPO: If it's not empty, the GPO is still linked to OUs, sites, and/or domains. Remove these links by right-clicking them and selecting Delete Link(s) from the menu, before deleting the GPO. 
8. In the left navigation pane, right-click the GPO and select Delete from the menu. 
9. In the Group Policy Management popup window, click OK to answer the question Do you want to delete this GPO and all links to it in this domain? 

This will not delete links in other domains.

### Using Powershell

```powershell
Remove-GPO -Name "Existing GPO Name"
```

---

<div style="page-break-after: always;"></div>

## Modifying GPO Settings

### Using Group Policy Manager

1. Open the Group Policy Management Console (gpmc.msc). 
2. In the left navigation pane, expand the Forest node. 
3. Expand the Domains node, and then navigate to the domain where you want to modify the GPO. 
4. Expand the domain name and then expand the Group Policy Objects node. 
5. Locate the GPO that you want to manage. 
6. Select the GPO. 
7. In the main pane, on the Settings tab, inspect the settings. Use the show, hide, and show all buttons to display the settings under their respective Group Policy setting nodes. 
8. In the left navigation pane, right-click the GPO and select Edit… from the menu. 
9. The Group Policy Management Editor (gpedit.msc) appears:
10. Edit the settings and/or preferences you want to edit in the Group Policy Management Editor window. 
11. Close the Group Policy Management

---

<div style="page-break-after: always;"></div>

## Adding Logon Scripts

### Using Group Policy Manager

1. Open the Group Policy Management Console (gpmc.msc). 
2. In the left navigation pane, expand the Forest node. 
3. Expand the Domains node, and then navigate to the domain where you want to assign a logon script. 
4. Expand the domain name and then expand the Group Policy Objects node. 
5. Locate the GPO that you want to manage. 
6. Select the GPO. 
7. In the left navigation pane, right-click the GPO and select Edit from the menu. The Group Policy Management Editor (gpedit.msc) appears. 
8. In the Group Policy Management Editor window, expand User Configuration, then Policies and Windows Settings. 
9. Select Scripts. 
10. In the main pane, right-click the Logon script and select Properties from the menu In the Logon window, click the Add… button. The Add a Script popup window appears:  
11. Type executable in the Script Name: field or browse to its location. 
12. In the Script Parameters: field, type any optional script parameters. 
13. Click OK to save the script settings. 
14. Click OK to close the Logon Properties window. 
15. Close the Group Policy Management Editor window.

---

<div style="page-break-after: always;"></div>

## Installing Applications

### Using Group Policy Manager

1. Open the Group Policy Management Console (gpmc.msc). 
2. In the left navigation pane, expand the Forest node. 
3. Expand the Domains node, and then navigate to the domain where you want to install the application. 
4. Expand the domain name and then expand the Group Policy Objects node. 
5. Locate the GPO that you want to manage. 
6. Select the GPO. 
7. In the left navigation pane, right-click the GPO and select Edit from the menu. The Group Policy Management Editor (gpedit.msc) appears. 
8. Expand Computer Configuration or User Configuration, depending on the kind of object you want to target the software installation to. 
9. Expand the Policies node, and then the Software Settings node. 
10. Right-click the Software Installation node and select New from the menu, and then Package…. 
11. In the Open screen, browse to the network share that has the package for the application as either an .msi or .zap file. Select the application and click Open. The Deploy Software popup screen appears: 
12. In the Deploy Software popup screen, select the deployment method. 
13. Click OK to save the settings. The package will be listed with its version, its deployment state, and source path. 
14. Close the Group Policy Management Editor window.

---

<div style="page-break-after: always;"></div>

## Linking A GPO to an OU

### Using Group Policy Manager

1. Open the Group Policy Management Console (gpmc.msc). 
2. In the left navigation pane, expand the Forest node. 
3. Expand the Domains node, and then navigate to the domain where you want to link the GPO. 
4. Expand the domain name. 
5. Navigate to the OU where you want to link an existing GPO. 
6. Right-click the OU and select Link an existing GPO… from the menu: 
7. In the Select GPO window, select the GPO you want to link from the list of available Group Policy objects:. 
8. Click OK to link the GPO.

---

<div style="page-break-after: always;"></div>

## Blocking Inheritance

### Using Group Policy Manager

1. Open the Group Policy Management Console (gpmc.msc). 
2. In the left navigation pane, expand the Forest node. 
3. Expand the Domains node. 
4. Expand the domain name. 
5. Navigate to the OU where you want to configure inheritance. 
6. Right-click the OU and select Block Inheritance from the menu.

---

<div style="page-break-after: always;"></div>

## Enforcing A GPO

### Using Group Policy Manager

1. Open the Group Policy Management Console (gpmc.msc). 
2. In the left navigation pane, expand the Forest node. 
3. Expand the Domains node, and then navigate to the domain where you want to link the GPO. 
4. Expand the domain name. 
5. Navigate to the OU where you want to enforce the GPO link. 
6. Expand the OU. 
7. Right-click the GPO link you want to enforce and click Enforced in the menu to enable or disable it. A check mark indicates whether Enforced is enabled or not.

---

<div style="page-break-after: always;"></div>

## Applying Security Filters

### Using Group Policy Manager

1. Open the Group Policy Management Console (gpmc.msc). 
2. In the left navigation pane, expand the Forest node. 
3. Expand the Domains node, and then navigate to the domain where you want to apply security filters the GPO. 
4. Expand the domain name and then expand the Group Policy Objects node. 
5. Locate the Group Policy Object that you want to manage. 
6. Select the Group Policy Object. 
7. In the main pane, on the Scope tab, in the Security Filtering area, click the Add… button to add a group for security filtering. 
8. In the Select User, Computer or Group window, type the name of a group and click the Check Names button. 
9. Click OK. to add the group to Security Filtering for the GPO. 
10. Select the default Authenticated Users entry and click the Remove button. 
11. The Group Policy Management popup window appears: 
12. In the Group Policy Management popup window, click OK to answer the question Do you want to remove this delegation privilege?.

---

<div style="page-break-after: always;"></div>

## Creating and Applying WMI Filters

### Using Group Policy Manager

1. Open the Group Policy Management Console (gpmc.msc). 
2. In the left navigation pane, expand the Forest node. 
3. Expand the Domains node, and then navigate to the domain where you want to apply WMI Filters. 
4. Expand the domain name. 
5. Right-click the WMI Filters node and select New… from the menu. 
6. In the New WMI Filter window, enter a name for the new WMI Filter. 
7. Optionally enter a description for the WMI Filter. 
8. Click the Add button. 
9. In the WMI Query window, select the WMI Namespace to target with the WMI Filter and enter the WMI Query: 
10. Click OK to save the WMI Query. 
11. Click Save to create the WMI Filter. 
12. In the left navigation pane, navigate to the Group Policy Objects node. 
13. Select the GPO you want to apply the WMI Filter to. 
14. In the main pane, on the Scope tab in the WMI Filtering area, select the WMI Filter. 
15. In the Group Policy Management popup window, click Yes to answer the question Would you like to change the WMI Filter to WMI Filter name?.

---

<div style="page-break-after: always;"></div>

## Configuring Loopback Processing

### Using Group Policy Manager

1. Open the Group Policy Management Console (gpmc.msc). 
2. In the left navigation pane, expand the Forest node. 
3. Expand the Domains node, and then navigate to the domain where you want to create the GPO. 
4. Expand the domain name and then expand the Group Policy Objects node. 
5. Locate the GPO that you want to manage. 
6. Select the GPO. 
7. In the left navigation pane, right-click the GPO and select Edit… from the menu. The Group Policy Management Editor (gpedit.msc) appears. 
8. In the Group Policy Management Editor window, expand Computer Configuration, Policies, then Administrative Templates, System and finally Group Policy. 
9. In the main pane, locate the Configure user Group Policy loopback processing mode setting and double-click it. The Configure user Group Policy loopback processing mode properties window appears: 
10. In the settings popup window, change the default value Not configured to Enabled. 
11. From the Mode drop-down menu, select either Merge or Replace (default). 
12. Click OK to save the setting. 
13. Close the Group Policy Management Editor window.