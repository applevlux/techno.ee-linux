# techno.ee-linux Lab 4 - 5

## Lab addressing plan
| Segment | VirtualBox network | IPv4 | IPv6 (ULA) | Members |
|---|---|---|---|---|
| Management | Host-only vboxnet0 | 192.168.56.0/24 | — | Windows host .1, ubuntu .10, rocky .11, router .12 |
| LAN A | Internal labnet-a | 10.10.10.0/24 | fd00:10::/64 | router .1, ubuntu .20 |
| LAN B | Internal labnet-b | 10.10.20.0/24 | fd00:20::/64 | router .1, rocky .20 |

## Deliverable checklist

- [ ] working resolver config
- [ ] evidence of caching from two `dig` timings
- [ ] short "three failures" table with:
  - [ ] symptom
  - [ ] distinguishing command
  - [ ] cause
  - [ ] fix
