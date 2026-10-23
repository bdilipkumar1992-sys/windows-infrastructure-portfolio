# Enterprise Windows Server 2022 — Active Directory Lab

## 1. Project Overview

This project documents a hands-on Windows Server 2022 lab focused on Active Directory Domain Services (AD DS), DNS, domain controller discovery, and Windows infrastructure administration.

The objective is to demonstrate practical infrastructure knowledge, PowerShell-based verification, and structured troubleshooting.

## 2. Lab Environment

| Component | Verified configuration |
|---|---|
| Operating system | Windows Server 2022 Standard Evaluation |
| Primary server | DC01 |
| Active Directory domain | cloud.com |
| Domain distinguished name | DC=cloud,DC=com |
| Domain controllers discovered | DC01 and DC02 |
| DNS role | Installed on DC01 |
| AD DS role | Installed on DC01 |
| Virtualization | Hyper-V lab |

## 3. Technologies Used

- Windows Server 2022
- Active Directory Domain Services
- DNS Server
- PowerShell
- Active Directory administration tools
- Windows domain controller diagnostics

## 4. Implementation and Verification

### 4.1 Operating System and Server Roles

Commands used:

```powershell
Get-ComputerInfo |
    Select-Object CsName, WindowsProductName, WindowsVersion

Get-WindowsFeature AD-Domain-Services, DNS
```

**Verified results:** DC01 runs Windows Server 2022 Standard Evaluation. The AD DS and DNS Server roles are installed.

### 4.2 Active Directory Domain

Command used:

```powershell
Get-ADDomain
```

**Verified results:** The command returned the `cloud.com` domain configuration and the distinguished name `DC=cloud,DC=com`.

### 4.3 Domain Controller Discovery

Command used:

```powershell
Get-ADDomainController -Filter *
```

**Verified results:** DC01 and DC02 were returned by the domain controller discovery query.

### 4.4 DNS Name Resolution

Command used:

```powershell
Resolve-DnsName $env:USERDNSDOMAIN
```

**Verified results:** The query returned A-record answers for `CLOUD.COM`, including the addresses `192.168.1.10` and `192.168.1.11`.

A separate query also resolved `DC02.cloud.com` to `192.168.1.11`.

### 4.5 DNS and Netlogon Services

Command used:

```powershell
Get-Service DNS, Netlogon |
    Select-Object Name, Status, StartType
```

**Verified results:** DNS and Netlogon were running on DC01 when checked.

## 5. Troubleshooting Lessons

During additional validation, an Active Directory replication diagnostic reported error 8524, indicating a DNS lookup failure.

This issue has not yet been resolved and is outside the current project's completed scope. Replication health is therefore not claimed as verified.

The diagnostic highlighted the importance of validating DNS service-location records, domain controller discovery, and replication separately from basic A-record resolution.

## 6. Project Status

**Completed:** Initial operating system and role checks, domain configuration inspection, domain controller discovery, and basic DNS resolution tests.

**Pending:** Detailed DNS validation, Organizational Unit and security group exercises, Group Policy implementation, domain client testing, and further domain health checks.

## 7. Skills Demonstrated

- Windows Server administration
- Active Directory domain inspection
- DNS troubleshooting fundamentals
- PowerShell-based infrastructure verification
- Domain controller discovery
- Technical documentation and incident analysis

## 8. Security and Lab Boundaries

This project uses a controlled lab environment. Credentials, passwords, private keys, and employer-confidential information must not be published.

Network addresses and internal infrastructure identifiers should be sanitized before sharing screenshots publicly.

## 9. Future Enhancements

- Create test Organizational Units, users, and security groups.
- Configure and validate a test Group Policy Object.
- Test domain client membership and authentication.
- Add a PowerShell domain health-check report.
- Revisit replication diagnostics in a separate troubleshooting exercise.
