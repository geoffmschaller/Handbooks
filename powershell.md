# Powershell Basics

## Table Of Conents

1. [Powershell Basics](#powershell-basics)
    1. [Table Of Conents](#table-of-conents)
    2. [Commands](#commands)
        1. [cd](#cd)
        2. [cls](#cls)
        3. [dir](#dir)
        4. [Get-Command](#get-command)
        5. [Get-Content](#get-content)
        6. [Get-Help](#get-help)
        7. [Get-Member](#get-member)
        8. [Get-Service](#get-service)
        9. [Get-Variable](#get-variable)
        10. [Resolve-DnsName](#resolve-dnsname)
        11. [Test-Connection](#test-connection)
        12. [Update-Help](#update-help)
    3. [Config](#config)
        1. [Set-ExecutionPolicy](#set-executionpolicy)
        2. [Set-StrictMode](#set-strictmode)
    4. [Errors](#errors)
        1. [Try, Catch, Finally](#try-catch-finally)
        2. [$Error](#error)
    5. [Flow Control](#flow-control)
        1. [not](#not)
        2. [if elseif else](#if-elseif-else)
        3. [Switch](#switch)
        4. [foreach](#foreach)
        5. [ForEach-Object](#foreach-object)
        6. [for](#for)
        7. [while](#while)
        8. [do while](#do-while)
        9. [do until](#do-until)
    6. [Powershell Functions](#powershell-functions)
    7. [Modules](#modules)
        1. [Module Save Locations](#module-save-locations)
        2. [Add a Module folder](#add-a-module-folder)
        3. [Get-Module](#get-module)
        4. [Import-Module](#import-module)
        5. [Remove-Module](#remove-module)
        6. [Find-Module](#find-module)
        7. [Install-Module](#install-module)
        8. [Uninstall-Module](#uninstall-module)
        9. [Create Custom Module](#create-custom-module)
    8. [Operators](#operators)
    9. [Parsing Files](#parsing-files)
        1. [CSV](#csv)
        2. [Excel Sheets](#excel-sheets)
        3. [JSON](#json)
    10. [Remote Execution](#remote-execution)
        1. [Invoke-Command](#invoke-command)
        2. [New-PSSession](#new-pssession)
        3. [Get-PSSession](#get-pssession)
        4. [Disconnect-PSSession](#disconnect-pssession)
        5. [Connect-PSSession](#connect-pssession)
        6. [Remove-PSSession](#remove-pssession)
    11. [Types](#types)
        1. [$null](#null)
        2. [$True and $False](#true-and-false)
        3. [Arrays](#arrays)
        4. [Array Lists](#array-lists)
        5. [Hash Tables](#hash-tables)
        6. [Custom Objects](#custom-objects)

## Commands

### cd

    Changes the current working directory.

| Command | Desc |
| --- | --- |
| `cd [PARAMS]` | Base command. |
| `cd ..` | Backs up one directory. |
| `cd Test` | Enters into the 'Test' subdirectory. |

---

### cls

    Clears the PS console screen.

| Command | Desc |
| --- | --- |
| `cls` | Base command. |

---

### dir

    Displays the contents of the current working directory.

| Command | Desc |
| --- | --- |
| `dir` | Base command. |

---

### Get-Command

    Displays the commands that PS is aware of.

| Command | Desc |
| --- | --- |
| `Get-Command` | Base command. |
| `Get-Command -Name <NAME OF COMMAND>` | Displays the command with the name provided. |
| `Get-Command -Verb <NAME OF VERB> [Get, Add, Clear, Set]` | Displays all the known commands with the given verb. |
| `Get-Command -Noun <NAME OF NOUN> [Job, Process, List, Host, etc]` | Displays all the known commands with the given noun. |
| `Get-Command -Verb <NAME OF VERB> -Noun <NAME OF NOUN>` | Displays all commands with the given verb and noun. | 

---

### Get-Content

    Gets content from a resource.

| Command | Desc |
| --- | --- |
| `Get-Content -Path <PATH TO FILE>` | Retrieves the content of the file. |

---

### Get-Help

    Shows the documentation for a given command.

| Command | Desc |
| --- | --- |
| `Get-Help <NAME OF COMMAND>` | Base command. |
| `Get-Help <NAME OF COMMAND> -Full` | Displays the full documentation for that command. |
| `Get-Help -Name <NAME OF COMMAND>*` | Displays documentation for commands that begin with the supplied name. |

---

### Get-Member

    Returns a list of all methods and properties of an object.

| Command | Desc |
| --- | --- |
| `Get-Member -InputObject <OBJECT NAME>` | Returns a list of all methods and properties of the supplied object. |

---

### Get-Service

    Returns a list of all services running on the OS.

| Command | Desc |
| --- | --- |
| `Get-Service` | Returns a list of all services |
| `Get-Service <NAME>` | Returns the service by name. |

---

### Get-Variable

    Returns a list of all variables, both user defined and built in.

| Command | Desc |
| --- | --- |
| `Get-Variable` | Base command. |
| `Get-Variable -Name <NAME OF VARIABLE>` | Returns the name and value for a given variable. |
| `Get-Variable -Name Preference*` | Returns a list of predefined preferences built into PS. |

---

### Resolve-DnsName

    Resolve DNS information for a given IP address.

| Command | Desc |
| --- | --- |
| `Resolve-DnsName -Name <IP ADDRESS>` | Base command. |

---

### Test-Connection

    Pings a host and returns information.

| Command | Desc |
| --- | --- |
| `Test-Connection <HOST>` | Base command. |
| `Test-Connection -ComputerName <NAME>` | Tests the connection to a computer using the host name. |
| `Test-Connection <HOST> -Count <NUMBER>` | Only sends one ICMP packet. |
| `Test-Connection <HOST> -Quiet` | Forces the command to return a simple bool for connection status. | 

---

### Update-Help

    Compares local documentation for commands against an online repository and downloads new docs if needed.

    May Require Admin.

| Command | Desc |
| --- | --- |
| `Update-Help` | Base command. |

---

## Config

### Set-ExecutionPolicy

    Sets the execution policy for scripts.

| Command | Desc |
| --- | --- |
| `Set-ExecutionPolicy -ExecutionPolicy <POLICY> [Restricted, AllSigned, RemoteSigned, Unrestricted]` | Base command. |

---

### Set-StrictMode

    Turns on many errors that are off by default.

| Command | Desc |
| --- | --- |
| `Set-StrictMode -Version Latest` | Base command. |

---

## Errors

### Try, Catch, Finally 

    Flow control and error handling. 
    Note that finally is optional. If it is set then it will run, even after an error was caught.
    Can only find terminating errors.

    Use $_.Exception.Message in the catch block return just the message.

    try {
        # Something Dangerous
    } catch {
        # Error Occured
    } finally {
        # Final code
    }

---

### $Error

    Stores a long history of errors. Newest errors are added to the front of the array.

| Command | Desc |
| --- | --- |
| `$Error` | Base command. |
| `$Error[0]` | Get the last error.

---

## Flow Control

### not

    -not (condition) 

---

### if elseif else

    if(statement) {
        # Something
    } elseif {
        # Something
    } else {
        # Something
    }

---

### Switch

    switch (statement) {
        caseOne {
            # Something
        }
        caseTwo {
            # Something
        }
        default {
            # Something
        }
    }

---

### foreach

    foreach($something in $array) {
        # Something

        ** Modifying an array element inside here does not modify the original array.
    }

---

### ForEach-Object

    $array | ForEach-Object - Process {
        # Something

        ** Modifying an array element inside here does not modify the original array.
    }

---

### for

    for($i = 0; $i -lt 10; $i++) {
        # Something
    }

---

### while

    while (condition) {
        # Something
    }

---

### do while

    do {
        # Something
    } while (condition)

---

### do until

    do {
        # Something
    } until (condition)

---

## Powershell Functions

    function Write-Name {

        param (

            # Mandatory and allow piping
            [Parameter(Mandatory, ValueFromPipeline)] 
            [string] $Name,

            # Optional named parameter w/ validation
            [Parameter()]
            [ValidateSet(33, 44, 55)]
            [int] $Age

        )

        # Runs once before process block
        begin {
            Write-Host "Beginning"
        }

        # Runs once for every value piped in. Required if you are piping in an array of values.
        process {
            Write-Host "My name is $Name and I am $Age years old."
        }

        # Runs once after the process block is complete.
        end {
            Write-Host "Ending"
        }
        
    }

$Names = ('Geoff', 'Kelly', 'Ellie')

$Names | Write-Name -Age 33

---

## Modules

### Module Save Locations

    System - C:\Windows\System32\WindowsPowershell\1.0\Modules
    All Users - C:\Program Files\WindowsPowershell\Modules
    Current User - C:\Users\<Current User>\Documents\WindowsPowerShell\Modules

---

### Add a Module folder

    $CurrentPath = [Environment]::GetEnvironmentVariable("PSModulePath", "Machine")
    [Environment]::SetEnvironmentVariable("PSModulePath", $CurrentValue + ";C:\<DIRECTORY PATH>", "Machine")

---

### Get-Module

    Shows the documentation for a given command.

| Command | Desc |
| --- | --- |
| `Get-Module <NAME OF COMMAND>` | Modules from this session only. |
| `Get-Module -ListAvailable` | Modules that are installed on the system (and all user folders) and available for import. |

---

### Import-Module

    Imports a module manually, if auto-import fails.

| Command | Desc |
| --- | --- |
| `Import-Module -Name <NAME OF MODULE>` | Imports Module |
| `Import-Module -Name <NAME OF MODULE> -Force` | Unload and then reimport module. Needs to be run if module code changes since last import. |

---

### Remove-Module

    Removes a module from the current session. It does not uninstall it.

| Command | Desc |
| --- | --- |
| `Remove-Module -Name <NAME OF MODULE>` | Removes Module |

---

### Find-Module

    Searches the Powershell Gallery for modules with the name or partial name.

| Command | Desc |
| --- | --- |
| `Remove-Module -Name <NAME OF MODULE>*` | Searches for the  Module |
| `Remove-Module -Name <NAME OF MODULE> | Install-Module` | Searches for the  Module and then installs it. |

---

### Install-Module

    Installs a module from the Powershell Gallery.

| Command | Desc |
| --- | --- |
| `Install-Module -Name <NAME OF MODULE>` | Install the  Module. By default it's installed for all users. |

---

### Uninstall-Module

    Uninstalls a module from the system.

| Command | Desc |
| --- | --- |
| `Uninstall-Module -Name <NAME OF MODULE>` | Uninstalls the  Module. |

---

### Create Custom Module

1. Create a folder with the module name. The folder must be the same name as the module.
2. Create custom .psm1 file.
3. Cretae a custom module manifest:


`New-ModuleManifest -Path '<PATH TO MANIFEST>.psd1' -Author '<AUTHOR>' -RootModule <PSM1 FILE NAME> -Description '<DESCRIPTION>'`

---

## Operators

| Operator | JS |
| --- | --- |
| -eq | === |
| -ne | !== |
| -gt | > |
| -ge | >= |
| -lt | < |
| -le | <= |
| -contains | array.contains('value') |

---

## Parsing Files

### CSV

#### Reading CSV Files

`Import-Csv -Path <FILE PATH>`

---

#### Querying CSV Files

`Import Csv  -Path <FILE PATH> | Where-Object {$_.'<HEADER KEY>' -eq '<VALUE>'}`

---

#### Renaming Header

`Import Csv -Path <FILE PATH> -Header '<KEY ONE>','<KEY TWO>','<KEY THREE>'`

---

#### Creating CSV Files

    You can add the -NoTypeInformation to remove the line at the top of the CSV file saying what powershell type this file came from.

    Add the -Append flag to prevent this from overwriting the file with each new line.

`<OBJECT> | Export-Csv -Path <OUTPUT FILE PATH>.csv`

---


### Excel Sheets

    Requires the third party module ImportExcel to be installed from the gallery.

#### Creating an Excel Sheet

`<OBJECT> | Export-Excel <FILE PATH>.xlsx`

---

#### Creating a worksheet

`<OBJECT> | Export-Excel <FILE PATH>.xlsx -WorksheetName '<WORKSHEET NAME>'`

---

#### Querying Worksheet Available

    Returns a list of the worksheets. Use a for loop to iterate through them.

`Get-ExcelSheetInfo -Path <FILE PATH>.xlsx`

---

#### Importing Excel Sheets

    By defualt only the first worksheet will be imported.

`Import-Excel -Path <FILE PATH> -WorksheetName '<WORKSHEET NAME>'`

---

#### Dynamic Fields

    Fields whos value is calculated on the fly, then added to the object/excel sheet.

    Usually done in a for loop so that each value is set for each row.

`<OBJECT> | Select-Object -Property @{Name = '<KEY NAME>'; Expression = {<EXPRESSION CALCULATED>}}`

Example: Adds a timestamp column to each entry.    
`<OBJECT> | Select-Object -Property @{Name = 'Timestamp'; Expression = {Get-Date -Format 'MM-dd-yy hh:mm:ss'}}}`

---

### JSON

#### Reading JSON

    Raw returns a plain string from the JSON file.

`Get-Content -Path <PATH TO JSON FILE>.json -Raw | ConvertFromJson`

---

#### Creating JSON

    Use the -Compress flag to obfuscate the json output.

`<OBJECT> | ConvertToJson -Compress`

---

#### JSON and Web Requests

    Use the latter to ignore the request status code and just show the result.

`Invoke-RestMethod -Uri <URI>`
`(Invoke-RestMethod -Uri <URI>).result`

---

## Remote Execution

### Invoke-Command

    Sends a command to a remote server. 
    
    If no Session variable is set then this command establishes connection, executes the command then closes the session. Think one off. Not very fast.

    Computers must be on the same AD domain and the executing computer must have priviledges on the host.

    Notice that local variables don't always work on the host.

    ** The 'using' method can cause problems when testing with Pester. You may have to use the ArgumentList.

| Command | Desc |
| --- | --- |
| `Invoke-Command -ComputerName <HOST COMPUTER NAME> -ScriptBlock {<SCRIPT TO EXECUTE}` | Base command. |
| `Invoke-Command -ComputerName <HOST COMPUTER NAME> -FilePath <SCRIPT FILE PATH>` | Executes the commands from a file. |
| `Invoke-Command -ComputerName <HOST COMPUTER NAME> { <SCRIPT TO RUN> $($args[0]) } -ArgumentList <LOCAL VARIABLE>` | Uses the argument list to pass local variables to the host. |
| `Invoke-Command -ComputerName <HOST COMPUTER NAME> { <SCRIPT TO RUN> $using:<LOCAL VARIABLE> }` | Uses the 'using' command to pass local variables to the host. |
| `Invoke-Command -Session <SESSION> { <SCRIPT TO RUN> }` | Executes the command using a pre-established session. |

---

### New-PSSession

    Creates a new session with a host.

| Command | Desc |
| --- | --- |
| `New-PSSession -ComputerName <COMPUTER NAME>` | Base command. |

---

### Get-PSSession

    Returns a list of past sessions. Can be saved as a variable.

| Command | Desc |
| --- | --- |
| `Get-PSSession` | Base command. |
| `Get-PSSession -Id <SESSION ID>` | Return a session by Id. |

---

### Disconnect-PSSession

    Disconnects the session but allows you to connect back later. You pipe in the session from Get-Session.

| Command | Desc |
| --- | --- |
| `Get-PSSession | Disconnect-PSSession` | Base command. |
| `Get-PSSession -Id <SESSION ID> | Disconnect-PSSession` | Disconnects a session by Id. |

---

### Connect-PSSession

    Connects to previouslly disconnected hosts, that you have already connected to.

| Command | Desc |
| --- | --- |
| `Connect-PSSession -ComputerName <COMPUTER NAME> ` | Base command. |

---

### Remove-PSSession

    Removes a previouslly connected session. You will not be allowed to connect again without creating a new session.

| Command | Desc |
| --- | --- |
| `Get-PSSession | Remove-PSSession` | Base command. |
| `Get-PSSession -Id <SESSION ID> | Remove-PSSession` | Removes a session by Id.

---

## Types

### $null

    The non-value assignment.

| Command | Desc |
| --- | --- |
| `$name = $null` | The variable 'name' is created but it's value is null. |

---

### $True and $False

    The true and false values.

| Command | Desc |
| --- | --- |
| `$isAlive = $True` | Value is true. |
| `$wantsToBeAtWork = $False` | Value is false. |

---

### Arrays

    Creates a fixed size array.

    Not efficient for larger data sets.

| Command | Desc |
| --- | --- |
| `$array = (<ONE>, <TWO>, <THREE>)` | Creates a fixed size array. |
| `$array += <four>` | Adds element 'four'. |
| `$array[0]` | Returns first value of the array. |
| `$array[-1]` | Returns the last value of the array. |
| `$array[1..2]` | Returns the second and third values of the array. |
| `$array = $array.Remove('four')` | Removes element 'four'. |

---

### Array Lists

    Creates a variable size array. Better for larger data sets. When adding or removing there is no need for overwrite.

| Command | Desc |
| --- | --- |
| `$arrayList = [System.Collections.ArrayList](<ONE>, <TWO>, <THREE>)` | Base command. |
| `$arrayList.Add(<FOUR>)` | Adds a fourth element. |
| `$arrayList.Remove(<FOUR>)` | Removes the 'fourth' element. |

---

### Hash Tables

    Creates a hash table dictionary. Notice the '@'

| Command | Desc |
| --- | --- |
| `$hashTable = @{ name = <NAME>; age = <AGE>;}` | Base command. |
| `$hashTable.Keys` | Returns a list of all of the keys. |
| `$hashTable.Values` | Returns a list of all of the values. |
| `$hashTable['<KEY>'] = <VALUE>` | Overwrites or creates a new entry into the hash table. |
| `$hashTable.Remove('<KEY>')` | Removes a key and value pair. |
| `$hashTable.ContainsKey('<KEY>')` | Returns a bool if a key exists in the hash table. |
| `$hashTable.ContainsValue('<Value>')` | Returns a bool if a value exists in the hash table. |

---

### Custom Objects

    Creates a custom object.

| Command | Desc |
| --- | --- |
| `$customObject = [PSCustomObject]@{<KEY> = <VALUE>;}` | Creates a custom object. |

---