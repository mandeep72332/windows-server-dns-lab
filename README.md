# windows-server-dns-lab
Windows Server DNS administration and troubleshooting lab
# Windows Server DNS Administration Lab

## 📌 Overview

This project documents a hands-on **Windows Server DNS Administration Lab** completed in a virtualized Windows Server environment.

The lab covers DNS configuration, DNS records, DNS zones, zone transfers, secondary and stub zones, reverse DNS, dynamic updates, DNS forwarding, and root hints.

The project demonstrates practical experience with **Windows Server, Active Directory-integrated DNS, DNS Manager, PowerShell, and DNS troubleshooting**.

---

##  Objective

The objective of this lab was to build practical experience administering and troubleshooting DNS services in a Windows Server environment.

The lab focused on:

* Creating and managing DNS records
* Understanding DNS name resolution
* Creating and managing DNS zones
* Working with Active Directory-integrated DNS
* Configuring primary and secondary DNS zones
* Performing DNS zone transfers
* Creating stub zones
* Configuring reverse DNS
* Configuring dynamic DNS updates
* Configuring DNS forwarding
* Understanding DNS root hints
* Testing DNS resolution using command-line tools

---

##  Architecture

The lab uses a Windows Server environment consisting of a **Domain Controller/DNS server** and a secondary Windows Server (**SVR1**).

### Lab Components

| Component         | Role                                      |
| ----------------- | ----------------------------------------- |
| Domain Controller | Active Directory Domain Services + DNS    |
| SVR1              | Secondary DNS / Windows Server            |
| Web01             | Host used for DNS record testing          |
| PC1               | Host used for DNS resolution testing      |
| DNS Manager       | DNS configuration and administration      |
| PowerShell        | Server administration and troubleshooting |
| Command Prompt    | DNS/name-resolution testing               |

### Example DNS Environment


                    Internet
                       |
                    DNS Server
                       |
                  8.8.8.8
                       |
                       |
              +----------------+
              | Domain         |
              | Controller     |
              | AD DS + DNS    |
              +----------------+
                       |
              DNS Zone / Records
                       |
          +------------+------------+
          |                         |
       Web01                       PC1
          |
    CNAME / Host Record
          |
www.sainidomain.local


              +----------------+
              | SVR1           |
              | Secondary DNS  |
              +----------------+
                       ^
                       |
                  Zone Transfer
                       |
                Domain Controller
```

---

# ⚙️ Configuration Steps

## 1. DNS and Active Directory Integration

DNS was accessed through **Tools → DNS** on the Windows Server Domain Controller.

After installing **Active Directory Domain Services**, DNS records were automatically created as part of the environment.

This demonstrated the integration between **Active Directory Domain Services and DNS**.

---

## 2. DNS Records

Different DNS record types were reviewed and configured during the lab.

### AAAA Record

An example of an **AAAA record** was reviewed for IPv6 DNS addressing.

### Host (A) Record

Host records were created to associate a hostname with an IP address.

For example, a new host named `PC1` was created and then tested from Command Prompt using `ping`.

### CNAME Record

A **CNAME (Canonical Name/Alias)** record was configured.

The lab created an alias that allowed:

```
www.sainidomain.local
```

to resolve to:

```
Web01
```

This was tested using DNS name resolution.

---

#  DNS Zones

The lab covered multiple DNS zone types and configurations.

## Primary DNS Zone

A primary DNS zone was created and configured for DNS management.

The lab also demonstrated that DNS zone files can be viewed under:

```
C:\Windows\System32\dns
```

when using a standard primary DNS zone.

---

## Active Directory-Integrated Zone

An Active Directory-integrated DNS zone was examined.

The lab demonstrated that DNS information for an **Active Directory-integrated zone** is stored in Active Directory rather than being represented as a traditional DNS zone file in the same way as a standard primary zone.

---

## Secondary DNS Zone

A secondary DNS server was configured on **SVR1**.

The Domain Controller was used as the primary/master DNS server, and a secondary zone was configured on SVR1.

The lab demonstrated DNS zone transfer between the servers.

---

#  DNS Zone Transfer

DNS zone transfer was configured between the Domain Controller and SVR1.

The process included:

1. Configuring the DNS server.
2. Allowing zone transfer.
3. Configuring SVR1 as a secondary DNS server.
4. Adding the secondary zone on SVR1.
5. Transferring DNS zone information from the master server.
6. Verifying that the zone appeared on SVR1.

Example SVR1 IP address used in the lab:

```
192.168.1.251
```

The lab also demonstrated transferring a Host/A record from the primary DNS zone to the secondary DNS server.

---

#  Stub Zone

A **Stub Zone** was created and reviewed.

The lab demonstrated that a stub zone contains DNS server information, including **NS information**, rather than maintaining a complete copy of the DNS zone data.

---

#  Reverse DNS Zone

A **Reverse DNS Zone** was created as a primary zone on the Domain Controller.

Reverse DNS provides DNS resolution from an IP address back toward a hostname.

---

#  Dynamic Updates

Dynamic DNS updates were reviewed.

For an **Active Directory-integrated DNS zone**, the lab configured the zone to use:

```text
Secure Updates Only
```

This demonstrated the relationship between DNS, Active Directory, and secure dynamic DNS updates.

---

#  DNS Forwarding

DNS forwarding was configured on the Domain Controller.

An example external DNS forwarder used in the lab was:

```
8.8.8.8
```

The configuration allows DNS queries that cannot be resolved within the local DNS zones to be forwarded to the configured DNS server.

Example:

```
Client
   |
   v
Local DNS Server
   |
   |-- sainidomain.local
   |       |
   |       +--> Local DNS records
   |
   |-- Unknown external name
           |
           v
        8.8.8.8
```

---

#  Conditional Forwarder

The lab also included configuration and review of a **Conditional Forwarder**.

A conditional forwarder allows DNS queries for a particular domain to be forwarded to designated DNS servers.

---

#  Root Hints

The lab reviewed **DNS Root Hints**.

Root hints provide information about the root DNS infrastructure and can be used when a DNS server does not have a configured forwarder for resolving an external DNS query.

The lab observed the root server information available through the DNS configuration.

---

#  Troubleshooting

## Remote Role Installation Issue

During the lab, an issue was encountered while attempting to remotely add a DNS role to SVR1 from the Domain Controller.

The **Add Roles and Features** option appeared unavailable/greyed out.

The lab documentation identifies a packet-size configuration issue and notes that the required PowerShell command should be run with Administrator privileges on both servers.

### Troubleshooting Approach

```
Domain Controller
       |
       | Remote Server Management
       v
      SVR1
       |
       v
Add Roles and Features
       |
       v
Option unavailable
       |
       v
Check server configuration
       |
       v
Apply required PowerShell configuration
       |
       v
Retry remote role installation
```

This troubleshooting process reinforced the importance of checking **server management connectivity and configuration** when performing remote Windows Server administration.

---

## DNS Resolution Testing

DNS resolution was tested using hostname-based commands such as:

```powershell
ping <hostname>
```

For example:

```
www.sainidomain.local
```

was tested to verify that the DNS name resolved to the expected host.

---

#  Screenshots

Screenshots documenting the configuration and testing steps are included in the project documentation.


  

#  Technologies & Tools

* Windows Server
* Active Directory Domain Services
* DNS Server
* DNS Manager
* PowerShell
* Command Prompt
* IPv4 / IPv6
* Virtualized Lab Environment

---

#  Skills Demonstrated

### Windows Server Administration

* Windows Server configuration
* Server role management
* Remote server administration
* PowerShell administration

### DNS Administration

* DNS record management
* A/Host records
* AAAA records
* CNAME records
* DNS zones
* Primary zones
* Secondary zones
* Stub zones
* Reverse DNS
* Dynamic DNS
* DNS forwarding
* Conditional forwarding
* Root hints
* DNS zone transfers

### Active Directory

* Active Directory-integrated DNS
* Secure dynamic updates
* DNS and AD DS integration

### Networking

* Hostname resolution
* IPv4
* IPv6
* DNS troubleshooting
* Network connectivity testing
* Client/server DNS architecture

### Troubleshooting

* DNS resolution testing
* Remote server administration troubleshooting
* DNS zone transfer troubleshooting
* Configuration validation
* Command-line diagnostics

---

#  What I Learned

Through this lab, I developed a better understanding of how **DNS supports Windows Server and Active Directory environments**.

Key learning outcomes included:

* How Active Directory integrates with DNS.
* How different DNS record types are used.
* How DNS zones are created and managed.
* The difference between primary, secondary, and stub zones.
* How DNS zone transfers work between DNS servers.
* How reverse DNS zones are configured.
* How secure dynamic updates work with Active Directory-integrated DNS.
* How DNS forwarding can be used for external name resolution.
* The purpose of conditional forwarding.
* The role of DNS root hints.
* How to test DNS name resolution from the command line.
* How to troubleshoot Windows Server DNS configuration issues.

---



#  Project Documentation

Detailed lab procedures and screenshots are available in:

```
documentation/DNS-Sec5.docx
```

The documentation contains the step-by-step DNS configuration work performed during the lab.

---

##  Author

**Mandeep Saini**

IT Infrastructure | Systems Administration | Networking | Azure

### Areas of Interest

* Windows Server
* Microsoft Azure
* Networking
* Active Directory
* DNS / DHCP
* Infrastructure Administration
* PowerShell
* Cloud Administration
* IT Troubleshooting
