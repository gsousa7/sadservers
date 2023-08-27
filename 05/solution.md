1. Run the test. If "curl" doesn't return, perhaps something is blocking the network connection.

2. Check the local firewall (iptables) settings with iptables -L

3. Partial Solution: Delete the iptables rule blocking port :80 , for example: iptables -F and test again.

4. Check permissions and ownership of the index.html file with: ls -l /var/www/html/index.html

(Open window once more to see the complete solution).

5. Final solution: change the ownership of the index file to the apache user: chown www-data: /var/www/html/index.html or allow other users to read the file owned by root (worse solution): chmod 644 /var/www/html/index.html
