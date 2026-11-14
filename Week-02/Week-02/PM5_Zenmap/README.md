# PM5 — Network Scanning with Zenmap

Environment observed:
- Kali Linux in VirtualBox NAT Network mode
- Interface: `eth0`
- IPv4: `10.0.0.2`
- Subnet: `10.0.0.0/24`
- Gateway: `10.0.0.1`
- Local MAC: `08:00:27:ab:5b:02`

Scans performed:
- `nmap -sn 10.0.0.2` — 1 host reported up.
- `nmap -sn 10.0.0.0/24` — 256 addresses scanned; 255 hosts reported up in 59.99 seconds.

**Caution:** 255 hosts up is the Nmap-reported count, not an independently verified count of distinct devices. Virtual NAT networking may affect discovery responses.

Zenmap topology visualization was generated, but the requested PDF export was not obtained. Add the original scan output and screenshots here.
