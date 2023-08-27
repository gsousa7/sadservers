Description: (Credit for the idea: fuero)

There is a one-class Java application in your /home/admin directory. Running the program will print out a secret code, or you may be able to extract the secret from the class file without executing it but I'm not providing any special tools for that.

Put the secret code in a /home/admin/solution file, eg echo "code" > /home/admin/solution.

Test: md5sum /home/admin/solution |awk '{print $1}' returns 9d2bd7aabb26681eacd9444da6b6643c
