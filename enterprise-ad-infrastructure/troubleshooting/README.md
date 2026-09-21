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

DNS must be reset after sysprep. The generalize pass resets network configuration.

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

---

## lockoutTime Write Failure

**Symptom**  
Attempts to force an account lockout by writing directly to the lockoutTime attribute returned error 0x57 — The parameter is incorrect.

**Root Cause**  
lockoutTime is managed exclusively by the DC's Local Security Authority through the authentication pipeline. Direct LDAP writes to this attribute are not supported, even from a Domain Admin account.

**Resolution**  
Lockout state is only achievable through actual failed authentication attempts against the DC. Generated five failed SMB authentication attempts via net use to trigger the lockout threshold.

---

## T2 Account Unlock Permission Failure

**Symptom**  
Unlock-ADAccount returned "Insufficient access rights to perform the operation" when run as adm-t2-jd.

**Root Cause**  
T2 accounts had no delegated rights on the _Users OU.

**Resolution**  
Delegated control on _Users OU via ADUC Delegate Control wizard using common tasks.
