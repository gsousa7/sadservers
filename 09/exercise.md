Description: The file /home/admin/somefile is open for writing by some process. Close this file without killing the process.

Test: lsof /home/admin/somefile returns nothing.
