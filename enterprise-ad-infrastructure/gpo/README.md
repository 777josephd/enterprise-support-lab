# GPO

Two policies implemented. Wallpaper policy scoped to OU. Account lockout configured in Default Domain Policy per Microsoft recommendation.

## Policies

| GPO | Scope | Purpose |
|---|---|---|
| `Desktop-Wallpaper-Policy` | `_Users\IT` OU | Enforces department wallpaper |
| `Default Domain Policy` | Domain root | Account lockout settings |

## Desktop Wallpaper Policy

Image staged at `\\WinDC-01\NETLOGON`. Policy linked to IT OU. Style set to Fill.

```powershell
gpupdate /force
gpresult /r
```

## Account Lockout Policy

Configured directly in `Default Domain Policy` at domain root.

`Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy`


```powershell
gpupdate /force
net accounts /domain
```

## Notes

- UNC paths in GPO wallpaper settings must not include quotation marks. Copying a file path from Windows Explorer appends them automatically.
- Account lockout policy must live in Default Domain Policy. A standalone GPO at domain root will be overridden by DDPolicy's higher link order precedence.
