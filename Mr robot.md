# flag 1
### the startup process
When starting any CTF like this one i scan the VM with nmap to see if there is any open services.
Upon search port 80 was open to a HTTP service
When you go to the IP:80 you will be greeted with a mr robot themed shell with afew commands you can use. 
I tried each of these and beyond the cool visuals got nothing from them.

### What i did next
I then decided to scan the directory of the site using dirsearch.
Upon completion i saw the site was using robots.txt which is a file that excludes items from webcrawling.
After opening robots.txt you will see the file name for the first flag which was then found.
You will also find a .dir file containing what i think is possible usernames to the website

# flag 2
For the next step i investigated the wordpress login i found during the dirsearch
I used burpsuite with the dictionary found during flag one and got the username "elliot"
I then used the found username with the same dic file and got no success finding the password

I then used the rockyou.txt file to find the password

### tools used
I could of continued to use burpsuite but its slow for such a large dataset.
I decided to use WPScan as it allows for faster password attacks

