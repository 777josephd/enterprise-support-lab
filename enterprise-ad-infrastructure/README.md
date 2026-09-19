# Enterprise AD Infrastructure

Windows Server 2022 Active Directory environment built on Proxmox, administered remotely via PowerShell and RSAT.

## Infrastructure Summary

| Hostname | IP | Roles | OS |
|---|---|---|---|
| WinDC-01 | 10.0.10.111 | DC, AD DS, DNS, DHCP | Windows Server 2022 |
| DESKTOP-P1NSWB9 | 10.0.10.113 | Domain-joined endpoint, RSAT management workstation | Windows 11 |

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

| GPO	| Linked To	| Purpose	| Status
|---|---|---|---|
| Account-Lockout-Policy | Domain	| Account lockout thresholds | Active |
| IT-Wallpaper | _Users\IT |	Enforces IT department desktop wallpaper | Active |

## Users and Departments

| Department | Users | OU Path |
|---|---|---|
| IT | ccarter | - |

## References

[Active Directory Domain Services Tier Model](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/tier-model)  
[Active Directory Domain Services Tier Model Best Practices](https://microsoft.github.io/ActiveDirectoryTierModel/best-practices/)
