# Milestone 1 — Base Infrastructure Deployment

## Objective

Set up a clean Windows Server virtual machine to serve as the foundation for future homelabs and hands-on IT practice. Ensure the server has the necessary updates, networking, and tools configured before installing additional roles or software. Create a clean baseline snapshot that can be restored if a future configuration change causes the server to fail.

## Environment

| Component | Configuration |
|---|---|
| Hypervisor | Oracle VirtualBox |
| Server OS | Windows Server 2025 Standard Evaluation (Desktop Experience) |
| VM Name / Hostname | DC01 |
| Memory | 4 GB |
| vCPUs | 2 |
| Virtual Disk | 60 GB dynamically allocated |
| Virtual Network | CyberLab-NAT |
| IPv4 Address | 10.10.10.10 |
| Subnet / Prefix | 10.10.10.0/24 |
| Default Gateway | 10.10.10.1 |
| DNS Server | 192.168.1.254 (temporary) |

## Implementation

### Server Identity

Changed the default Windows-generated computer name to `DC01` to make the server easy to identify and prepare it for its planned role as the domain controller.

#### Configuration

```powershell
Rename-Computer -NewName "DC01" -Restart
```

### Static IPv4 Configuration

Configured `DC01` with the static IPv4 address `10.10.10.10/24` to ensure the server maintains a consistent network address. This will allow client systems to reliably locate services hosted by the server, including DNS and Active Directory.

#### Configuration

```powershell
New-NetIPAddress -InterfaceAlias "Ethernet" -IPAddress 10.10.10.10 -PrefixLength 24 -DefaultGateway 10.10.10.1
```

Temporary DNS configuration:

```powershell
Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ServerAddresses 192.168.1.254
```

## Verification

Running `hostname` returned `DC01`, confirming that the server was successfully renamed.

Running `ipconfig /all` verified that Windows was using the configured static IPv4 settings.

Connectivity was tested using:

```powershell
ping 10.10.10.1
ping 8.8.8.8
ping google.com
```

The tests verified:

- `10.10.10.1` — connectivity between DC01 and its default gateway.
- `8.8.8.8` — external IP connectivity without depending on DNS resolution.
- `google.com` — DNS name resolution and external connectivity.

All three tests returned 4 of 4 replies with 0% packet loss.

## System Preparation

Installed VirtualBox Guest Additions to improve integration between the Windows Server guest and the VirtualBox host.

Windows Update was then used to install current security, cumulative, .NET, Microsoft Defender, and Windows Security platform updates before deploying additional server roles.

## Baseline Snapshot

After verifying the server configuration and completing system updates, the virtual machine was shut down and a VirtualBox snapshot was created.

**Snapshot:** `BASE - Server 2025 Clean`

The snapshot provides a known-good recovery point that can be restored if future configuration changes or lab exercises cause the server to become unusable.

## Milestone Result

The base Windows Server environment is operational and ready for additional infrastructure services. No Active Directory or other server roles were installed during this milestone.
