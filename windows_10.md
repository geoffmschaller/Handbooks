# Windows 10

## Table Of Conents

- [Windows 10](#windows-10)
  - [Table Of Conents](#table-of-conents)
  - [System Information](#system-information)
  - [Disk Partition](#disk-partition)
  - [MSInfo32](#msinfo32)

## System Information

CLI tool that displays information regarding the current system.

```powershell
# Displays local system info
systeminfo

# Remote system information
systeminfo /s [Hostname] /u [Remote Username] /p [Remote Password]

# Output to a file
systeminfo >> [File name].txt
```

## Disk Partition

CLI tool that mirrors Disk Manager GUI

```powershell
# Enter the CLI
diskpart

# Lists disks
> list disk

# Selects a disk
> select disk [Disk number]

# Lists partitions on a disk
> list partition

# Lists volumes on a disk
> list volume

# Additional Commands 
> ?
```

## MSInfo32

Displays a GUI that shows low level details about the system. This can be saved in a .nfo file to be viewed later.

```powershell
msinfo32
```