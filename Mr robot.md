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
I then used the found username with the same dic file

### tools used
I could of continued to use burpsuite but its slow for such a large dataset.
I decided to use WPScan as it allows for faster password attacks since its not limited 

After the password wordlist had ran for abit i got the password.

Once i had access to the wordpress i needed to find a way to get a shell on my terminal from the vulnerable machine

For this i used a PHP reverse shell exploit from Pentestmonkey
https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php
I inserted the code into the archive.php site and then when i go to this site the exploit will auto execute giving me a reverse shell
First i set up the listener
```
└─$ nc -nvlp 8080      
listening on [any] 8080 ...
```

then when i went to the site i got the execution of exploit and a shell in my terminal 
```
connect to [IP] from (UNKNOWN) [IP] 50319
Linux linux 3.13.0-55-generic #94-Ubuntu SMP Thu Jun 18 00:27:10 UTC 2015 x86_64 x86_64 x86_64 GNU/Linux
 11:45:12 up 13:26,  0 users,  load average: 0.00, 0.01, 0.38
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
uid=1(daemon) gid=1(daemon) groups=1(daemon)
/bin/sh: 0: can't access tty; job control turned off
$ 
```
### what i found using the reverse shell
in the /home/robot/ directory is two files
key-2-of-3.txt
and a password hash

I cannot access the key without the correct permissions so for this we will need to crack the password hash.
```
robot:c3fcd3d76192e4007dfb496cca67e13b
```
is the password has for robots user
For the cracking of the hash i used a online md5 cracking website
That successfully gives you the password

### the trouble
After this i was stuck on how to login to the user i had now got the password for.
I tried to SSH into it but couldnt get passed a connection fail
This is when someone suggested i needed to include the bin/bash folder so using python i did this with the command
```
python3 -c 'import pty;pty.spawn("/bin/bash")'
```
after this i could login as robot by doing 
```
su robot
```
and the password

Once i had the user set as robot i was able to go to /home/robot and open key-2-of-3.txt successfully getting the key

# flag 3



