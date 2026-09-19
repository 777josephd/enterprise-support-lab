# Troubleshooting

Documented incidents encountered during lab build and configuration. Each entry includes the observed symptom, identified root cause, and resolution applied.

---

## Domain Join Failure Proxmox Clone

**Symptom**
`Add-Computer` returns errors when attempting to join `soc-lab.local`.

**Root Cause**
Proxmox cloning copies the disk byte-for-byte. The cloned machine retains the source machine's SID, causing identity conflicts on the domain.

**Resolution**
Run sysprep to generalize the machine, then rejoin.

```powershell
C:\Windows\System32\Sysprep\sysprep.exe /generalize /oobe /reboot
Set-DnsClientServerAddress -InterfaceIndex (Get-NetAdapter).ifIndex -ServerAddresses 10.0.10.111
Add-Computer -DomainName "soc-lab.local" -Credential SOC-LAB\Administrator -Restart
```

> DNS must be reset after sysprep. The generalize pass resets network configuration.

---

## Wallpaper GPO Black Screen on Login

**Symptom**
`ccarter` receives a black desktop after login. GPO is confirmed applied via `gpresult /r`. UNC path resolves correctly via `Test-Path`.

**Root Cause**
UNC path in the GPO wallpaper setting contained quotation marks. Windows Explorer appends them automatically when copying a file path. Group Policy does not strip them and fails silently.

**Resolution**
Remove quotation marks from the wallpaper path in the GPO setting. Run `gpupdate /force` and re-login to verify.

---

## Account Lockout Policy Settings Not Taking Effect

**Symptom**
`net accounts` does not reflect the configured lockout values after `gpupdate /force`. A standalone GPO `Account-Lockout-Policy` is linked at domain root and confirmed present in `gpresult /r`.

**Root Cause**
`Default Domain Policy` holds link order 1 at domain root, giving it highest precedence. The standalone GPO is present but overridden.

**Resolution**
Microsoft's documented recommendation is to configure account policies directly in `Default Domain Policy`. Standalone GPO deleted.

`Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy`

```powershell
gpupdate /force
net accounts /domain
```
