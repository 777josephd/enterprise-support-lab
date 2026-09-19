# Users and Groups

Mock department users, a security group, and a departmental SMB share. Users created via PowerShell script.

## Prerequisites

```powershell
Add-WindowsCapability -Name Rsat.ActiveDirectory.DS-LDS.Tools~~~~0.0.1.0 -Online
```

## Users

Created via `Create-ADUser.ps1`. Supports optional nested OU placement via `-ParentOU` parameter.

| Name | Username | OU |
|---|---|---|
| Alice Anderson | `aanderson` | `_Users\IT` |
| Bob Brooks | `bbrooks` | `_Users\HR` |
| Carol Carter | `ccarter` | `_Users\IT` |
| Dave Dixon | `ddixon` | `_Users\Finance` |

## Security Group

```powershell
New-ADGroup -Name "IT-Security" -GroupScope Global -GroupCategory Security `
    -Path "OU=IT,DC=soc-lab,DC=local" -Description "IT Department Security Group"

Add-ADGroupMember -Identity "IT-Security" -Members "ccarter","aanderson"
```

## SMB Share

Departmental share on `WinDC-01` with tiered access permissions.

| Principal | Access |
|---|---|
| `Domain Admins` | Full |
| `IT-Security` | Change |
| `Domain Users` | Read |

```powershell
Invoke-Command -ComputerName WinDC-01 -ScriptBlock {
    New-Item -Path "C:\Shares\DeptShare" -ItemType Directory -Force
    New-SmbShare -Name "DeptShare" -Path "C:\Shares\DeptShare" `
        -FullAccess "soc-lab\Domain Admins" `
        -ChangeAccess "soc-lab\IT-Security" `
        -ReadAccess "soc-lab\Domain Users"
}
```

## Notes

- Execution policy set to `RemoteSigned` at `CurrentUser` scope for script execution.
- `bbrooks` used to verify read-only access boundary enforcement on `DeptShare`.
