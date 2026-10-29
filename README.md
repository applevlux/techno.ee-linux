# techno.ee-linux Lab 9


## Justification Table

| Change            | What was exposed?          | What was broken in result?                       |
|---                |---                         |---                                               |
| Purged Apache2    |http attack surface         |Web hosting and any app relying on a web interface|
| Purged vsftpd     |ftp protocol vulnurabilities|FTP file transfers                                |
| Purged Samba      |SMB vulnerabilities         |Windows file sharing                              |


## Submission checklist

- [x] captured `before.txt`
- [x] captured `after.txt`
- [x] recorded the diff
- [x] documented each removal with justification
- [x] hardened SSH on both VMs
- [x] validated `sshd -t`
- [x] reloaded SSH without closing the active session
- [x] disabled password authentication
- [x] configured `ProxyJump`
- [x] enabled unattended updates
- [x] proved automatic updates ran
- [x] verified external port exposure and password refusal

## Evidence checklist

- [x] `before.txt`
- [x] `after.txt`
- [x] diff output
- [x] service and package removal justification
- [x] account audit results
- [x] SSH configuration or relevant drop-in config
- [x] `ProxyJump` configuration
- [x] automatic update logs or journal output
- [x] `nmap` scan results
- [x] SSH password attempt refusal output
