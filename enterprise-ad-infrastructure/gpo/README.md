# GPO

| GPO | Scope | Purpose |
|---|---|---|
| Desktop-Wallpaper-Policy | `_Users\IT` | Enforces department wallpaper |
| Workstation-LocalAdmin-T2 | `_Computers\Workstations` | Assigns T2 accounts as local admins |
| Default Domain Policy | Domain Root | Account lockout settings |

## Notes:

- UNC paths in GPO wallpaper settings must not include quotation marks. Windows Explorer appends them automatically when copying a path.
- Account lockout policy is configured in Default Domain Policy per Microsoft recommendation.
