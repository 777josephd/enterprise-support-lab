# AD Structure

OU structure follows a minimal enterprise-aligned model. Default containers are not used for managed objects. All OUs use an underscore prefix to avoid naming conflicts with built-in containers.

## OU Hierarchy

```
SOC-LAB.local
├── _Admin
│   ├── Tier0-Accounts
│   └── Tier2-Accounts
├── _Computers
│   ├── Workstations
│   └── Servers
├── _Users
│   ├── IT
│   ├── HR
│   └── Sales
├── _Groups
│   └── Security
└── _Service-Accounts
```

## Object Placement

| Object | OU |
|---|---|
| Win11 endpoint | `_Computers\Workstations` |
| Domain Admin account (`adm-t0-1`) | `_Admin\Tier0-Accounts` |
| Built-in Administrator | Default container — break-glass only |
| Department users | `_Users\<department>` |

## Notes

- `Protect object from accidental deletion` is enabled on all OUs. Disable via `View > Advanced Features` in ADUC before moving or deleting objects. Re-enable after.
- Initial flat OUs (Groups, HR, IT, Sales) were created in an earlier iteration. Restructured to current hierarchy in this session.
