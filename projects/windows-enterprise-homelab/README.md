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

## Project Status

**Milestone 1 — Base Infrastructure Deployment: Complete**

The initial Windows Server environment has been deployed, updated, configured with static networking, tested for connectivity, and saved as a clean baseline snapshot.

Active Directory and other infrastructure services have not yet been deployed.
