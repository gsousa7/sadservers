Description: A developer created a testing program that is continuously writing to a log file `/var/log/bad.log` and filling up disk. You can check for example with `tail -f /var/log/bad.log`.
This program is no longer needed. Find it and terminate it.

Test: The log file hasn't changed in the last 6 seconds: `find /var/log/bad.log -mmin -0.1` (You don't need to know the details of this command).
zxc
