# techno.ee-linux Lab 2

## Unit Files

#### disk-report.service
```ini
[Unit]
Description=Append disk usage to log
Documentation=man:df(1)
After=local-fs.target

[Service]
Type=oneshot
User=reports
ExecStart=/usr/local/bin/disk-report.sh
StandardOutput=append:/var/log/disk-report.log
StandardError=append:/var/log/disk-report.log
```
#### disk-report.timer

```ini
[Unit]
Description=Run disk-report everyday
Documentation=systemd.time(7)

[Timer]
OnCalendar=daily
Persistent=true

[Install]
WantedBy=timers.target
```
## journal error output

```bash
Oct 29 14:45:03 ubuntu-01 disk-report.sh[2502]: /usr/local/bin/disk-report.sh: line 3: /var/log/disk-report.log: Permission denied
Oct 29 14:45:03 ubuntu-01 systemd[1]: disk-report.service: Main process exited, code=exited, status=1/FAILURE
Oct 29 14:45:03 ubuntu-01 systemd[1]: disk-report.service: Failed with result 'exit-code'.
Oct 29 14:45:03 ubuntu-01 systemd[1]: Failed to start disk-report.service - Append disk usage to log.
Oct 29 14:50:04 ubuntu-01 systemd[1]: Starting disk-report.service - Append disk usage to log...
Oct 29 14:50:04 ubuntu-01 disk-report.sh[2510]: /usr/local/bin/disk-report.sh: line 2: /var/log/disk-report.log: Permission denied
Oct 29 14:50:04 ubuntu-01 disk-report.sh[2515]: /usr/local/bin/disk-report.sh: line 3: /var/log/disk-report.log: Permission denied
Oct 29 14:50:04 ubuntu-01 systemd[1]: disk-report.service: Main process exited, code=exited, status=1/FAILURE
Oct 29 14:50:04 ubuntu-01 systemd[1]: disk-report.service: Failed with result 'exit-code'.
Oct 29 14:50:04 ubuntu-01 systemd[1]: Failed to start disk-report.service - Append disk usage to log.
```
## Why Option B is better than A
It allows us to avoid an incident where a malicious actor gets the ability to write whatever they want in /var/log/ using the reports account.
## list-timers output

```
NEXT                        LEFT LAST                              PASSED UNIT              >
Fri 2026-10-30 00:00:00 UTC   8h Thu 2026-10-29 15:40:09 UTC 1min 35s ago disk-report.timer >

1 timers listed.
Pass --all to see loaded but inactive timers, too.
```
## journalctl successful runs

```
Oct 29 15:38:53 ubuntu-01 systemd[1]: Starting disk-report.service - Append disk usage to log...
Oct 29 15:38:53 ubuntu-01 systemd[1]: disk-report.service: Deactivated successfully.
Oct 29 15:38:53 ubuntu-01 systemd[1]: Finished disk-report.service - Append disk usage to log.
Oct 29 15:40:09 ubuntu-01 systemd[1]: Starting disk-report.service - Append disk usage to log...
Oct 29 15:40:09 ubuntu-01 systemd[1]: disk-report.service: Deactivated successfully.
Oct 29 15:40:09 ubuntu-01 systemd[1]: Finished disk-report.service - Append disk usage to log.
Oct 29 15:56:28 ubuntu-01 systemd[1]: Starting disk-report.service - Append disk usage to log...
Oct 29 15:56:28 ubuntu-01 systemd[1]: disk-report.service: Deactivated successfully.
Oct 29 15:56:28 ubuntu-01 systemd[1]: Finished disk-report.service - Append disk usage to log.
```
## why was the `reports` user created with `--no-create-home --shell /usr/sbin/nologin`, and what would an attacker gain if those flags were omitted?
The flags were added to disallow anyone to attempt to login into the reports user and prevent them from using it as well as getting rid of a home directory with the ability to write, read, execute any file in there.
An attacker would be able to login, make a malicious script, execute it and attempt privilege escalation to cause damage and/or havoc to our linux system.

