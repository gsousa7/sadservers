1. Nginx is not running, start it and then try: curl http://localhost , which gives 502 Bad Gateway error.

2. in cat /etc/nginx/sites-enabled/default realize the file /run/gunicorn.socket does not exist. From /etc/systemd/system/gunicorn.service or ps auxf|grep gunicorn we see gunicorn is using the file /run/gunicorn.sock instead. Fix the nginx config file and restart nginx.

3. Now curl localhost returns nothing and curl -I localhost works. We can also curl against the socket file: curl --unix-socket /run/gunicorn.sock http://localhost also returns nothing but curl -I --unix-socket /run/gunicorn.sock http://localhost works. (Next "clue" gives the solution).

Solution From last command we see Content-Length: 0, fix the wsgi.py file (for ex use a number of bytes equal or greater than the 13 needed for the message, or take out the Content-Length header altogether) and restart the gunicorn service.
