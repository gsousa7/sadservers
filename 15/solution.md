1. chmod is not executable. This is a fun (granted, unrealistic) problem that is popular for the different inventive ways to fix it, so a web search to find solutions is easy :-)

2. (solution to chmod issue) To make chmod executable you can write some code like: sudo perl -e 'chmod 0755, "/usr/bin/chmod"' or /lib64/ld-linux-x86-64.so.2 /usr/bin/chmod +x /usr/bin/chmod, then you can do chmod +x /home/admin/wtfit

3. Upon execution of wtfit you get ERROR: can't open config file. You need to introspect the code or the system calls to find out the name and location that the program is expecting and create that file.

4. (Solution to config file) do strace /home/admin/wtfit and towards the end see the entry openat(AT_FDCWD, "/home/admin/wtfitconfig.conf", O_RDONLY|O_CLOEXEC) = -1 ENOENT (No such file or directory) , create the missing file, for ex: touch /home/admin/wtfitconfig.conf

5. Now wtfit gives an ERROR: can't connect to server. You need to look in the network for where the program is trying to communicate to, and create a network service that can listen to the network request.

6. Run tcpdump to sniff the network and while running, execute wtfit: sudo tcpdump -i lo & only listen to localhost, or all ports except our "ssh": sudo tcpdump -i any port not 8080 &

7. Filtering other traffic, you'll see this packet IP localhost.40302 > localhost.7777: Flags [S], seq 1326851547, win 65495, options ... (initiator port will vary )

8. (Solution to last issue) Run a server on tcp:7777, for ex: python3 -m http.server 7777 & (there's also nginx, apache and netcat installed or you could redirect with iptables to an existing service).
