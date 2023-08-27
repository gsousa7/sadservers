1. We can see one file webfile with ls -l /var/www/html/ and we don't have direct access to it, let's try and check web access with curl localhost

2. Apache is asking for credentials, we can see with /etc/apache2/sites-enabled/000-default.conf that it has basic authentication enanbled. We cannot edit this config file but we can try and break the /etc/apache2/.htpasswd file.

3. Running John the Ripper cd ~ ; john/run/john /etc/apache2/.htpasswd we obtain the Apache password of the user carlos, run curl again passing user:password

4. Running curl localhost -u "carlos:chalet" we see webfile, we can grab it and save it as secret: curl localhost/webfile -u "carlos:chalet" --output secret

5. We check with file secret that the file is a Zip archive. If we try to unzip secret we see it is password-protected.

6. You can use zip2john to extract the hash and then use john again to find the password for the zip file: john/run/zip2john secret > zip.hash then john/run/john zip.hash.

7. The previous step yield the password andes for the zip file of the secret, we can now just unzip secret, which creates a secret.txt file with the secret as asked. (Done).
