1. There are no clues, contact me if you can think of any that won't immediately give away the solution. (Open window once more to see the solution).

Solution: This is in fact a Podman container :-)
You can get the image: docker.io/fduran/venice.

A way of checking is by looking at the environment of the PID=1 process and see if there's a container variable, for ex: cat /proc/1/environ|tr "\0" "\n"|grep container , in our case would be container=podman but I changed its value.

An indicator is to look at the running processes and see that there are no kernel threads like [kthreadd].
