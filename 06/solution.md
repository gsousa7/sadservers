 1. Check the status of Nginx: systemctl status nginx

2. Check Nginx configuration file with nginx -t

3. After fixing the Nginx config file at /etc/nginx/sites-enabled/default (deleting first character ;) and restarting Nginx, when you curl again you get a 500 HTTP error. Look at application error logs in /var/log/ directory for the cause.



(Open window once more to see the complete solution).

Solution: (once previous steps done) As superuser, comment out or increase "LimitNOFILE" in /etc/systemd/system/nginx.service , reload the systemd configuration with systemctl daemon-reload and restart nginx with systemctl restart nginx
