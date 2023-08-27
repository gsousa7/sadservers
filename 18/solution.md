1. Running the test you get a "man-in-the-middle" warning, as suggested you can sudo -u client ssh-keygen -f "/home/client/.ssh/known_hosts" -R "localhost" (note: if you run the command not as client then you need to change the owner of the file to client. You can also delete the file's contents> /home/client/.ssh/known_hosts.

2. Running the test again adds the correct host key but returns client@localhost: Permission denied (publickey).. Review the ssh service configuration under /etc/ssh/.

3. There's a DenyUsers client entry in the sshd configuration; as root delete the file /etc/ssh/sshd_config.d/sad.conf and systemctl restart ssh

4. Running the test command results in the message: WARNING: UNPROTECTED PRIVATE KEY FILE! Permissions 0644 for '/home/client/.ssh/id_rsa' are too open., so we take out "others" permissions for the private key: chmod 600 /home/client/.ssh/id_rsa.

5. Error is now: "Your account has expired; please contact your system administrator.". Look at lslogins client or grep client /etc/shadow. The "password" (rather account) expiration is set to "0" ("1970-Jan01"), to set to no expiration run as superuser: chage -E-1 client.

6. Now we get the error:exec request failed on channel 0. See in /etc/pam.d/sshd the configuration used /etc/security/limits.conf, which includes a line to limit the processes for user client to zero: client hard nproc 0. Comment out or delete that line as root.

7. Error is now "This account is currently not available.". Look again at lslogins client or grep client /etc/passwd, see the shell field set to "nologin". Change it to for example (as root): usermod --shell /bin/bash client (to see a list of available shells: cat /etc/shells). This is the last broken thing!
