 1. Run the test. Is the Postgres server running? You can check with: systemctl status postgresql or with the ps command, for example: ps auxf|grep postgres

2. Try to start Postgres systemctl start postgresql and check its status again.

3. Check errors using journalctl , for example journalctl -u postgresql or journalctl -p err.

4. A log message says Timed out waiting for device /dev/xvdb.. The postgres data directory is /opt/pgdata/ but there's no data there. Check if there is a disk volume that hasn't been mounted.

5. Running lsblk -f you can see there's an unmounted xfs disk and file -s /dev/nvme0n1 confirms it has data (the exact device name may be different). Try and mount the device on the Postgres data directory.

6. Trying mount /dev/nvme0n1 /opt/pgdata does not work. From journalctl|tail we see: systemd[1]: opt-pgdata.mount: Unit is bound to inactive unit dev-xvdb.dev

7. systemd controls mounts and reads /etc/fstab , edit /etc/fstab and change /dev/xvdb into /dev/nvme0n1 and systemctl daemon-reload. Now you can: mount /dev/nvme0n1 /opt/pgdata and check there are postgres files there. Try restarting Postgres now.

8. See journalctl log entry No space left on device. Check disk space: df -h

9. Check the size of the Postgres data directory (for example: du -sh /opt/pgdata/main) and compare with the size of the volume /opt/pgdata

Solution: Delete /opt/pgdata/file*.bk files and restart Postgres with sudo systemctl start postgresql
