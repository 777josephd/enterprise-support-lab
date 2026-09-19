# DNS

AD-integrated DNS, installed as part of DC promotion.  
`WinDC-01` is the sole DNS server for `soc-lab.local`.

## Configuration

| Setting | Value |
|---|---|
| Zone | `soc-lab.local` - AD-integrated, auto-created at promotion |
| DNS Server | `10.0.10.111` (WinDC-01) |
| DC NIC DNS | Self (`10.0.10.111`) |
| Client DNS | Distributed via DHCP scope option |

## Verification

```powershell
Resolve-DnsName soc-lab.local
Resolve-DnsName WinDC-01.soc-lab.local
```
## Notes

- DC NIC DNS is set to self. Prevents resolution failures independent of DHCP.
- Clients do not required manual DNS configuration. DHCP scope option handles distribution.
