Description: There is a secret stored in a file that the local Apache web server can provide. Find this secret and have it as a /home/admin/secret.txt file.

Note that in this server the admin user is not a sudoer.

Also note that the password crackers Hashcat and Hydra are installed from packages and John the Ripper binaries have been built from source in /home/admin/john/run

Test: sha1sum /home/admin/secret.txt |awk '{print $1}' returns cc2c322fbcac56923048d083b465901aac0fe8f8
