# AD Structure

OU structure follows a minimal enterprise-aligned model. Default containers are not used for managed objects. All OUs use an underscore prefix to avoid naming conflicts with built-in containers. Built-in Administrator account remains in the default Users container as a break-glass account only.

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
## Notes

- `Protect object from accidental deletion` is enabled on all OUs. Disable via `View > Advanced Features` in ADUC before moving or deleting objects. Re-enable after.
