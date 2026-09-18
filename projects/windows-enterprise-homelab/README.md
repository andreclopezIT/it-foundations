# Windows Enterprise Homelab

## Overview

This project documents the design, deployment, and administration of a virtual Windows enterprise environment built for hands-on IT and systems administration practice.

The environment is being built incrementally to develop practical experience with Windows Server, networking, Active Directory, DNS, DHCP, Group Policy, PowerShell, system administration, and troubleshooting.

Rather than documenting only successful configurations, this project will also include troubleshooting scenarios, configuration changes, and the methods used to verify and resolve issues.

## Environment

| Component | Configuration |
|---|---|
| Hypervisor | Oracle VirtualBox |
| Server OS | Windows Server 2025 Standard Evaluation |
| Server | DC01 |
| Virtual Network | CyberLab-NAT |
| Network | 10.10.10.0/24 |
| DC01 Address | 10.10.10.10 |
| Gateway | 10.10.10.1 |
| Forest / Domain | drelab.test |

## Project Status

**Milestone 1 — Base Infrastructure Deployment: Complete**

The initial Windows Server environment was deployed, updated, configured with static networking, tested for connectivity, and saved as a clean baseline snapshot.

**Milestone 2 — Active Directory & Identity Foundation: Complete**

AD DS and DNS were deployed on DC01, the `drelab.test` forest/domain was created and verified, DNS forwarding was configured, and the initial OU, user, admin, and security-group structure was established.

**Milestone 3 — Access Control & File Services: Planned**

The next phase will focus on file shares, NTFS permissions, group-based access control, and access troubleshooting.

## Documentation

- [Milestone 1 — Base Infrastructure Deployment](./docs/01-base-infrastructure.md)
- [Milestone 2 — Active Directory & Identity Foundation](./docs/02-active-directory-foundation.md)
