1. Find the File Descriptor number (FD) with: lsof /home/admin/somefile

2. Use the "exec" built-in Bash command with the FD found (77) exec man page (Next "clue" gives the solution).

Solution: The file somefile was open by the shell as per lsof (run for example ls -la /proc/$$/fd/, where $$ returns the PID of the current shell). To close the FD: exec 77>&-
