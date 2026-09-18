# Milestone 2 — Active Directory & Identity Foundation

## Objective

Deploy Active Directory Domain Services on `DC01`, create the `drelab.test` forest and domain, verify Active Directory-integrated DNS, and establish a basic identity and organizational structure for future domain administration labs.

## Active Directory Deployment

Installed the **Active Directory Domain Services (AD DS)** role and required management tools on `DC01`.

The server was then promoted as the first domain controller in a new forest with the following configuration:

| Component | Configuration |
|---|---|
| Forest / Domain | `drelab.test` |
| Domain Controller | `DC01` |
| Forest Functional Level | Windows Server 2025 |
| Domain Functional Level | Windows Server 2025 |
| DNS Server | Enabled |
| Global Catalog | Enabled |
| Read-Only Domain Controller | Disabled |

A Directory Services Restore Mode (DSRM) password was configured during promotion. The password is not stored in this repository.

The default Active Directory storage paths were retained:

| Component | Path |
|---|---|
| AD DS Database | `C:\WINDOWS\NTDS` |
| AD DS Log Files | `C:\WINDOWS\NTDS` |
| SYSVOL | `C:\WINDOWS\SYSVOL` |

The prerequisite check completed successfully before promotion, and `DC01` rebooted automatically after the domain controller installation completed.

## Post-Promotion Verification

The following commands were used to verify the domain controller after reboot:

```powershell
whoami
hostname
Get-ADDomain
Get-ADForest
Get-Service NTDS,DNS
```

Verification confirmed that:

- The server hostname remained `DC01`.
- The forest and domain were created as `drelab.test`.
- Active Directory Domain Services (`NTDS`) was running.
- The DNS Server service was running.
- `DC01.drelab.test` was operating as the domain controller for the new environment.

## DNS Verification

After promotion, DNS functionality was verified using:

```powershell
Get-DnsClientServerAddress -InterfaceAlias "Ethernet" -AddressFamily IPv4
Resolve-DnsName drelab.test
Resolve-DnsName _ldap._tcp.dc._msdcs.drelab.test -Type SRV
```

The checks confirmed that:

- `DC01` was using its local DNS service.
- `drelab.test` resolved to `10.10.10.10`.
- The Active Directory LDAP SRV record resolved to `dc01.drelab.test` on TCP port 389.

External DNS forwarders were configured as:

```text
1.1.1.1
8.8.8.8
```

External name resolution was then verified with:

```powershell
Get-DnsServerForwarder
Resolve-DnsName google.com
```

## Organizational Unit Structure

A basic OU structure was created under `drelab.test` for lab-managed objects:

```text
drelab.test
├── Admins
├── Lab-Users
├── Workstations
├── Servers
└── Groups
```

Default Active Directory containers such as `Users`, `Computers`, and `Domain Controllers` were left intact.

The custom `Lab-Users` OU was created instead of using the default `Users` container so lab users can be managed through a clean OU-based structure.

## User Accounts

Two accounts were created to separate standard and privileged access:

| Account | Purpose |
|---|---|
| `andre.lopez` | Standard domain user |
| `andre.admin` | Separate privileged administrative account |

`andre.lopez` was created in the `Lab-Users` OU.

`andre.admin` was created in the `Admins` OU and added to the `Domain Admins` group for administrative tasks.

No passwords are stored in this repository.

## Security Groups

Two Global Security groups were created in the `Groups` OU:

| Group | Membership |
|---|---|
| `IT-Admins` | `andre.admin` |
| `Helpdesk` | `andre.lopez` |

These groups provide a foundation for later role-based access control labs instead of assigning permissions directly to individual users.

## Recovery Snapshot

After Active Directory and DNS were successfully configured and verified, a VirtualBox snapshot was created:

```text
AD - Forest and DNS Configured
```

This snapshot provides a known-good restore point before additional services, permissions, client systems, and Group Policy configurations are introduced.

## Milestone Result

`DC01` is now operating as the first domain controller and DNS server for the `drelab.test` environment.

The domain has a basic organizational structure, separate standard and administrative identities, security groups, working internal DNS, and external DNS forwarding.

The environment is ready for the next milestone: **Access Control & File Services**.
