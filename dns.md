# DNS

## Table Of Contents

1. [DNS](#dns)
    1. [Table Of Contents](#table-of-contents)
    2. [Record Types](#record-types)
    3. [Add-DnsServerPrimaryZone](#add-dnsserverprimaryzone)
        1. [Create an AD integrated forward lookup (FQDN => IP) zone.](#create-an-ad-integrated-forward-lookup-fqdn--ip-zone)
        2. [Create a file backed forward lookup (FQDN => IP) zone.](#create-a-file-backed-forward-lookup-fqdn--ip-zone)
        3. [Create an AD integrated reverse lookup (IP => FQDN) zone.](#create-an-ad-integrated-reverse-lookup-ip--fqdn-zone)
        4. [Create a file backed reverse lookup (IP => FQDN) zone.](#create-a-file-backed-reverse-lookup-ip--fqdn-zone)
    4. [Add-DnsServerResourceA](#add-dnsserverresourcea)
    5. [Add-DnsServerZoneDelegation](#add-dnsserverzonedelegation)
    6. [Get-DnsServerForwarder](#get-dnsserverforwarder)
    7. [Get-DnsServerResourceRecord](#get-dnsserverresourcerecord)
    8. [Remove-DnsServerResourceRecord](#remove-dnsserverresourcerecord)
    9. [Set-DnsServerSecondaryZone](#set-dnsserversecondaryzone)

## Record Types

| Record | Desc |
| --- | --- |
| A | FQDN => IPv4 |
| AAAA | FQDN => IPv6 |
| NS | DNS Servers |
| MX | Mail Exchange |
| CNAME | Canonical Name. FQDN => Alias |
| PTR | Pointer Record. IP => FQDN |
| SRV | Server. In AD used to point the user to the local domain controller. |
| SOA | Start of authority. Provides general information about the DNS zone. |

---

## Add-DnsServerPrimaryZone

The Add-DnsServerPrimaryZone cmdlet adds a specified primary zone on a Domain Name System (DNS) server.

You can add an Active Directory-integrated forward lookup zone, an Active Directory-integrated reverse lookup zone, a file-backed forward lookup zone, or a file-backed reverse lookup zone.

### Create an AD integrated forward lookup (FQDN => IP) zone.

> `Add-DnsServerPrimaryZone -Name "DNS-TWO.geoff.com" -ReplicationScope "Forest" -PassThru`

### Create a file backed forward lookup (FQDN => IP) zone.

> `Add-DnsServerPrimaryZone -Name "DNS-TWO.geoff.com" -ZoneFile "DNS-TWO-BACKUP.geoff.com.dns"`

### Create an AD integrated reverse lookup (IP => FQDN) zone.

> `Add-DnsServerPrimaryZone -NetworkID "10.1.0.0/24" -ReplicationScope "Forest"`

### Create a file backed reverse lookup (IP => FQDN) zone.

> `Add-DnsServerPrimaryZone -NetworkID 10.3.0.0/24 -ZoneFile "DNS-BACKUP.evilcorp.com.dns"`

---

## Add-DnsServerResourceA

The Add-DnsServerResourceRecordA cmdlet adds a host address (A) record to a Domain Name System (DNS) zone. An A record specifies an IPv4 address.

> `Add-DnsServerResourceRecordA -Name "blog" -ZoneName "geoff.com" -IPv4Address "192.168.0.12"`

---

## Add-DnsServerZoneDelegation

The Add-DnsServerZoneDelegation cmdlet adds a zone delegation to a Domain Name System (DNS) zone. For instance, you can add a child domain called west01 to your top level domain, contoso.com, and specify a DNS server for that delegated domain.

> `Add-DnsServerZoneDelegation -Name "evilcorp.com" -ChildZoneName "blog" -NameServer "blog.evilcorp.com" -IPAddress 172.23.90.136 -PassThru -Verbose`

---

## Get-DnsServerForwarder

The Get-DnsServerForwarder cmdlet gets configuration settings on a DNS server. A forwarder is a Domain Name System (DNS) server on a network that is used to forward DNS queries for external DNS names to DNS servers outside that network.

> `Get-DnsServerForwarder`

---

## Get-DnsServerResourceRecord

The Get-DnsServerResourceRecord cmdlet gets the following information for a specified resource record from a Domain Name System (DNS) zone:

- HostName
- RecordType
- RecordClass
- TimeToLive
- Timestamp
- RecordData

> `Get-DnsServerResourceRecord -ZoneName "geoff.com" -RRType "A"`

> `Get-DnsServerResourceRecord -ZoneName "geoff.com" -RRType "CNAME"`

The `-ExpandedProperty RecordData` flag can be set for more detailed output.

> `Get-DnsServerResourceRecord -ZoneName "geoff.com" -RRType "SRV" | Select-Object -ExpandedProperty RecordData`

---

## Remove-DnsServerResourceRecord

The Remove-DnsServerResourceRecord cmdlet removes resource record objects from a Domain Name System (DNS) zone.

You can either use the Get-DnsServerResourceRecord cmdlet to specify an object, or you can specify the RRtype, Name and RecordData of the resource record you want to remove. If you specify an RRtype or name and there are multiple resource records, you can specify the RecordData to delete a specific record. If you do not specify RecordData, the cmdlet deletes all records that match RRtype and Name for the specified zone.

> `Remove-DnsServerResourceRecord -ZoneName "geoff.com" -RRType "A" -Name "blog"`

---

## Set-DnsServerSecondaryZone

The Set-DnsServerSecondaryZone cmdlet changes settings for an existing secondary zone on a Domain Name System (DNS) server.

> `Set-DnsServerSecondaryZone "DNS-SECONDARY.geoff.com" -MasterServers 172.23.90.124,2001:4898:7020:f100:458f:e6a2:fcaf:698c -PassThru`

---