# DHCP

DHCP Server role installed on `WinDC-01`. Authorized in AD. Single scope serving `10.0.10.0/24`.

## Prerequisite

DC NIC must have a static IP before the DHCP role is functional. Converted from DHCP-assigned:

```powershell
netsh interface ip set address "Ethernet" static 10.0.10.111 255.255.255.0 10.0.10.1
netsh interface ip set dns "Ethernet" static 10.0.10.111
```

## Configuration

| Setting | Value |
|---|---|
| DHCP Server | `WinDC-01` (`10.0.10.111`) |
| Scope Name | `VLAN10` |
| Range | `10.0.10.100` – `10.0.10.200` |
| Subnet Mask | `255.255.255.0` |
| Default Gateway | `10.0.10.1` |
| DNS Server | `10.0.10.111` |
| DNS Domain | `soc-lab.local` |
| Lease Duration | 8 days (default) |

## Verification

```powershell
Get-DhcpServerInDC
Get-DhcpServerv4Scope
```
