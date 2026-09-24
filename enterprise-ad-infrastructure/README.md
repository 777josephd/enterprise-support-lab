# Enterprise AD Infrastructure

Windows Server 2022 Active Directory environment built on Proxmox, administered remotely via RSAT.

## Infrastructure Summary

| Hostname | IP | Roles | OS |
|---|---|---|---|
| WinDC-01 | 10.0.10.111 | DC, AD DS, DNS, DHCP | Windows Server 2022 |
| WIN11-ADMIN | 10.0.10.100 | Domain-joined endpoint, RSAT management workstation | Windows 11 | 
| WIN11-WS | 10.0.10.113 | Domain-joined endpoint, standard user workstation | Windows 11 |

## Domain and Network
**Domain:** `soc-lab.local`  
**Network:** VLAN10 `10.0.10.0/24`  
**Gateway:** `10.0.10.1`

## OU Structure

```
soc-lab.local
├── _Admin
│   ├── Tier0-Accounts
│   └── Tier2-Accounts
├── _Computers
│   ├── Workstations
│   └── Servers
├── _Groups
│   └── Security
├── _Service-Accounts
└── _Users
    ├── HR
    ├── IT
    └── Sales
```

## Admin Tier Model
- Tier 0 for DC-level work only
- Tier 2 for endpoint administration
- Built-in Administrator as break-glass account

## Services Deployed

| Service | Status | Notes |
|---|---|---|
| AD DS | Active | soc-lab.local, single domain |
| DNS | Active | AD-integrated, forward lookup zone for soc-lab.local |
| DHCP | Active | Authorized in AD, scope VLAN10 10.0.10.100 - 10.0.10.200 |

## GPOs

| GPO | Scope | Purpose |
|---|---|---|
| Desktop-Wallpaper-Policy | `_Users\IT` | Enforces department wallpaper |
| Workstation-LocalAdmin-T2 | `_Computers\Workstations` | Assigns T2 accounts as local admins |
| Default Domain Policy | Domain Root | Account lockout settings |

## Users and Departments

| Department | Users |
|---|---|
| HR | aanderson |
| Sales | bbrooks |
| IT | ccarter |
| IT | ddixon |

## References

[Active Directory Domain Services Tier Model](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/tier-model)  
[Active Directory Domain Services Tier Model Best Practices](https://microsoft.github.io/ActiveDirectoryTierModel/best-practices/)
