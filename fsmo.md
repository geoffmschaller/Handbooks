# FSMO

## Table Of Contents

1. [FSMO](#fsmo)
    1. [Table Of Contents](#table-of-contents)
    2. [Schema Operations Master](#schema-operations-master)
    3. [Domain-Naming Operations Master](#domain-naming-operations-master)
    4. [Primary Domain Controller (PDC) Emulator Operations Master](#primary-domain-controller-pdc-emulator-operations-master)
    5. [Relative ID (RID) Operations Master Role](#relative-id-rid-operations-master-role)
    6. [Infastructure Operations Master](#infastructure-operations-master)
    7. [Query to see the FSMO Roles](#query-to-see-the-fsmo-roles)
    8. [Move-ADDirectoryServerOperationsMasterRole](#move-addirectoryserveroperationsmasterrole)
        1. [Transfer roles to a specific domain controller](#transfer-roles-to-a-specific-domain-controller)
        2. [Seize roles using -Force](#seize-roles-using--force)

## Schema Operations Master

Shows which domain controller holds the role of Schema Operations Master. The Schema Master is the only role that can update the AD Schema.

Limit one per forest.

This requires a user account on the DC that is a member of the Schema Admin Group.

> `Get-ADForest | select SchemaMaster`

---

## Domain-Naming Operations Master

Shows which domain controller holds the role of DomainNamingMaster. 

This role is the only one that can add or remove domains.

Limit one per forest.

> `Get-ADForest | select DomainNamingMaster`

---

## Primary Domain Controller (PDC) Emulator Operations Master

Role in charge of syncing time, password change replications, locking accounts because of failed login, and stores a copy of the Group Policy Object.

Limit one per domain.

> `Get-ADDomain | select PDCEmulator`

---

## Relative ID (RID) Operations Master Role

The RID value is used to process of SID (unique ID in a domain) creation. It's a pool of IDs. 

When a domain has multiple DCs, each DC is issued an initial pool of 500 RIDs. When 250 remain, the RID Role owner issues the DC sends another block.

Limit one per domain.

> `Get-ADDomain | select RIDMaster`

---

## Infastructure Operations Master

Replicates SID and Distinguished Name (DN) values changes to cross-domains, so that when a user moves domains, they have access to appropriate resources.

This role checks the SID and DN values against the global catalog. If the values are different, it updates the catalog and replicates the changes to other DCs.


Limit one per domain.

> `Get-ADDomain | select InfastructureMaster`

---

## Query to see the FSMO Roles

Displays which servers the roles reside on.

> `netdom query fsmo`

---

## Move-ADDirectoryServerOperationsMasterRole

The Move-ADDirectoryServerOperationMasterRole cmdlet moves one or more operation master roles to a directory server. You can move operation master roles to a directory server in a different domain if the credentials are the same in both domains.

The Identity parameter specifies the directory server that receives the roles. You can specify a directory server object by one of the following values:

    Name of the server object (name)
    The distinguished name of the NTDS Settings object
    The distinguished name of the server object that represents the directory server
    GUID (objectGUID) of server object under the configuration partition
    GUID (objectGUID) of NTDS settings object under the configuration partition

For Active Directory Lightweight Directory Services (AD LDS) instances the syntax for the server object name is <computer-name>$<instance-name>. The following is an example of this syntax:

asia-w7-vm4$instance1

When you type this value in Windows PowerShell, you must use the backtick (`) as an escape character for the dollar sign ($). Therefore, for this example, you would type the following:

asia-w7-vm4`$instance1

You can also set the parameter to a directory server object variable, such as $<localDirectoryServerObject>.

The Move-ADDirectoryServerOperationMasterRole cmdlet provides two options for moving operation master roles:

Role transfer, which involves transferring roles to be moved by running the cmdlet using the Identity parameter to specify the current role holder and the OperationMasterRole parameter to specify the roles for transfer. This is the recommended option.

Operation roles include PDCEmulator, RIDMaster, InfrastructureMaster, SchemaMaster, or DomainNamingMaster. To specify more than one role, use a comma-separated list.

Role seizure, which involves seizing roles you previously attempted to transfer by running the cmdlet a second time using the same parameters as the transfer operation, and adding the Force parameter. The Force parameter must be used as a switch to indicate that seizure, instead of transfer, of operation master roles is being performed. This operation still attempts graceful transfer first, then seizes if transfer is not possible.

Unlike using Ntdsutil.exe to move operation master roles, the Move-ADDirectoryServerOperationMasterRole cmdlet can be remotely executed from any domain joined computer where the Active Directory module for Windows PowerShell administration module is installed and available for use. This can make the process of moving roles simpler and easier to centrally administer as each of the two command operations required can be run remotely and do not have to be locally executed at each of the corresponding role holders involved in the movement of the roles, for instance, role transfer only allowed at the old role holder, role seizure only allowed at the new role holder.

### Transfer roles to a specific domain controller

> `Move-ADDirectoryServerOperationMasterRole -Identity USER04-DC1 -OperationMasterRole SchemaMaster,DomainNamingMaster,PDCEmulator,RIDMaster,InfrastructureMaster`

### Seize roles using -Force

> `Move-ADDirectoryServerOperationMasterRole -Identity USER04-DC1 -OperationMasterRole RIDMaster,InfrastructureMaster,DomainNamingMaster -Force`

---