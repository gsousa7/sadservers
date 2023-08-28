 1. Run the test. Is the Postgres server running? You can check with: `sudo systemctl status postgresql` or with the `ps` command, for example: `ps auxf|grep postgres`

2. Try to start sudo `systemctl start postgresql` and check status again.

3. Check service errors using `journalctl` , for example `journalctl -u postgresql` or `journalctl -p err`.

4. Check the system log `/var/log/syslog`, look out for recent postgres messages.

5. Check disk space `df -h`

6. Check if Postgres can't start due to lack of disk space: `grep -i 'no space left' /var/log/syslog`

7. Check the size of the Postgres data directory (for example: `du -sh /opt/pgdata/main`) and compare with the size of the volume `/opt/pgdata`

(Open window once more to see the complete solution).

Solution: Delete `/opt/pgdata/file*.bk` files and try to restart Postgres with `sudo systemctl start postgresql`
