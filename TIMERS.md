TIMERS
======

Credit for documentation:

https://documentation.suse.com/smart/systems-management/html/systemd-working-with-timers/index.html

Time is specified differently in cron and systemd. Use the patterns below as a conversion template:

```bash
# Cron:               Minute Hour Day Month DayOfWeek
# systemd: OnCalendar=DayOfWeek Year-Month-Day Hour:Minute:Second
```

```bash
# Cron     : systemd timer
# -------- : ----------------------------
# @reboot  : OnBootSec=1s
# @yearly  : OnCalendar=*-01-01 00:00:00
# @annually: OnCalendar=*-01-01 00:00:00
# @monthly : OnCalendar=*-*-01 00:00:00
# @weekly  : OnCalendar=Sun *-*-* 00:00:00
# @daily   : OnCalendar=*-*-* 00:00:00
# @hourly  : OnCalendar=*-*-* *:00:00
```

Verify that the files you created contain no errors (f the command returns no output, the files have passed the verification successfully):

`$ systemd-analyze verify /etc/systemd/system/hello-world.*`

As a regular user, you must provide the path to the unit files, as in the examples below. Otherwise, if a system-wide timer with the same name exists, it would be executed or listed instead.

`systemctl --user start  ${HOME}/.config/systemd/user/${TIMER}`
`systemctl --user enable ${HOME}/.config/systemd/user/${TIMER}`
