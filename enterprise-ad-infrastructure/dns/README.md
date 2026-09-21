# DNS

AD-integrated DNS, installed as part of DC promotion. WinDC-01 is the sole DNS server for soc-lab.local.

| Setting | Value |
|---|---|
| Zone | soc-lab.local |
| DNS Server | 10.0.10.111 (WinDC-01) |

## Notes:

- DC NIC DNS is set to self. Prevents resolution failures independent of client configuration.
- WIN11-WS DNS is configured statically on the NIC, does not rely on DHCP.
