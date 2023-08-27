1. (You need to be superuser to run Docker; use sudo for the commands). Check current images and containers with docker images; docker ps -a

2. Check logs with docker logs container_name

3. You can try and docker run using a different entrypoint or command if there's an issue with the executable. (Open window once more to see a partial solution).

4. In Dockerfile, in the CMD line change serve.js to server.js and rebuild the image (from the /home/admin/app directory and using an image name like "app" here for ex): docker build -t app . (use the local node:15.7-alpine provided image, there's no Internet access to pull other ones).
You could run as well docker run -d app node server.js to fix this issue.

5. Check the exposed port we want in the container.

6. Stop the nginx server running on the same port and restart the container.(Open window once more to see the solution).

7. In the Dockerfile, in the EXPOSE line change port 8880 to 8888 and rebuild the image. Run with: docker run -d -p 8888:8888 app (where app is your Docker image name). Or without fixing and rebuilding the image you could docker run -d -p 8888:8888 app or docker run -d -p 8888:8888 app node server.js.
