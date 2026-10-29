# techno.ee-linux Lab 9


## Justification Table
TODO: finish this table
| Change            | What was exposed? | What was broken in result? |
|---                |---                |---                         |
| Purged Apache2    |                   |                            |
| Purged vsftpd     |                   |                            |
| Purged Samba      |                   |                            |


## Submission checklist

- [x] captured `before.txt`
- [x] captured `after.txt`
- [x] recorded the diff
- [ ] documented each removal with justification
- [x] hardened SSH on both VMs
- [x] validated `sshd -t`
- [x] reloaded SSH without closing the active session
- [x] disabled password authentication
- [x] configured `ProxyJump`
- [x] enabled unattended updates
- [ ] proved automatic updates ran
- [x] verified external port exposure and password refusal

## Evidence checklist

- [x] `before.txt`
- [x] `after.txt`
- [x] diff output
- [ ] service and package removal justification
- [ ] account audit results
- [x] SSH configuration or relevant drop-in config
- [x] `ProxyJump` configuration
- [ ] automatic update logs or journal output
- [x] `nmap` scan results
- [x] SSH password attempt refusal output

TODO: finish account audit and update logs for ubuntu-01