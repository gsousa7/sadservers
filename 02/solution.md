 1. To get the first field (IP) of the file, you can do `awk '{print $1}' access.log` or using "cut" with delimiter of space (-d' ') and picking the first field (-f1): `cat access.log |cut -d' ' -f1`. You may want to append a pipe | head or | tail as you construct the command to see how your filters are working.

2. After the previous step, you want to sort the IPs so they are together and can be counted: `cat access.log | awk '{print $1}' |sort`

3. Now you want to do the count with "uniq -c", so we have so far: `awk '{print $1}' access.log |sort|uniq -c`

4. Finally you want to sort the results with "sort" (goes in ascending order) and get the latest one (with "tail -1" for example), or sort in reverse order with "sort -r" and get the top result: `awk '{print $1}' access.log|sort|uniq -c|sort -r|head -1`.

(Open window once more to see the complete solution).

Solution: One posible way is `awk '{print $1}' access.log|sort|uniq -c|sort -r|head -1|awk '{print $2}' > /home/admin/highestip.txt`
