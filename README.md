# techno.ee-linux Lab 4 - 5

## Lab addressing plan
| Segment | VirtualBox network | IPv4 | IPv6 (ULA) | Members |
|---|---|---|---|---|
| Management | Host-only vboxnet0 | 192.168.56.0/24 | — | Windows host .1, ubuntu .10, rocky .11, router .12 |
| LAN A | Internal labnet-a | 10.10.10.0/24 | fd00:10::/64 | router .1, ubuntu .20 |
| LAN B | Internal labnet-b | 10.10.20.0/24 | fd00:20::/64 | router .1, rocky .20 |

## Three failures table

| Break Type | How | Diagnosis Command | Fix |
|---|---|---|---|
| Wrong nameserver IP	Set | DNS to invalid IP (e.g., 10.10.10.99) |	dig example.com → timeout |	Restore correct IP via nmcli/netplan |
|Unbound service down |	sudo systemctl stop unbound |	systemctl status unbound shows inactive |	sudo systemctl start unbound |
|Firewall blocking port 53 |	sudo ufw deny 53/udp |	tcpdump shows no responses | sudo ufw allow 53/udp |

## Deliverable checklist

- [x] working resolver config
- [x] evidence of caching from two `dig` timings
- [x] short "three failures" table with:
  - [x] symptom
  - [x] distinguishing command
  - [x] cause
  - [x] fix
