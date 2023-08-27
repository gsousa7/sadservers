1. Use find and pass the results to grep via xargs

(Open window once more to see the solution to the first part).

2. (Solution to 1) for example: `find /home/admin/ -type f -name "*.txt" |xargs grep -c 'Alice'` , adding the results from three files: `echo -n 411 > /home/admin/solution`

(Open window once more to see the solution to the second part).

3. (Solution to 2) `grep Alice -A 1 /home/admin/1342-0.txt` (or open the file with less or vi and enter /Alice). Appending this result: `echo 156 >> /home/admin/solution.`
