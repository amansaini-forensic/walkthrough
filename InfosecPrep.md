InfosecPrep
 “This machine was created for the InfoSec Prep Discord Server as a give way for a 30d
 voucher to the OSCP Lab, Lab materials, and an exam attempt.”
 First of all start VPN which we have downloaded from the official site of Offsec to enter in the
 Offsec free rooms network

  Now start the InfosecPrep machine

 First thing what we have to do run the Nmap scan on the given ip address
 nmap which will led us to the services that are running, I’m gonna use the command below.
 command : nmap -sCV -A -p- -Pn --min-rate 5000 192.168.121.89
 Breaking it Down:
 1.  nmap → Runs the Nmap network scanning tool.
 2. -sC → Runs default scripts.
 3. -sV → Detects service versions.
 4. -A → Enables OS detection, version detection, script scanning, and traceroute.
 5. -p → Scans all 65,535 ports.
 6. -Pn → Disables host discovery (treats the target as alive).
 7. --min-rate 5000 → Sends at least 5000 packets per second (faster scan).
 8. 192.168.121.89 → The target IP address



we can see the following ports and services:
 port 22/tcp - SSH
 port 80/tcp - HTTP
 Now, let’s first have a look at the HTTP service running on Port 80

In the page on http port we can see in the text is written :
Oh yea1 Almost forgot the only user on this box is "oscp".
 here we can see is only one user the is 
oscp


 Here we are not getting much details or any information about the user password or anything
 now here we gonna do directory fuzzing with our best tool
 dirsearch
 ==here is the command :- dirsearch --url 
http://192.168.121.89/

  Here we can see the 
/secret.txt file is Disallow lets check if we can see it or it conatian
 something interesting

 Upon visiting this file we see a bunch of text which is actually base64 encoded:
 Lets decode is using 
cyber chef




And here we get a private key to login in the server we already have a user name 
OSCP
 lets check if its for this user
 to use it we need to save this key in a file
 command : 
vi filename
 press i to write
 paste the key
 press 
ESC
 press 
:wq! to exit from vi and save the key


After saving the key in a file give permission 
chmod 600 id_rsa
 Breaking it Down:
 1. 
chmod
 → Changes file permissions.
 2. 
600
 → Sets the file permissions to:
6
 → Owner: Read (r) + Write (w)
 0
 → Group: No permissions
 0
 → Others: No permissions
 3. 
id_rsa
 → The private SSH key file.
 Now login via ssh port 22 using 
ssh -i filename 
oscp@192.168.121.89




And here we got shell and the we get user flag here
 via cat flag.txt

And here we need to do Privilege Escalation
 first we check sudo permissions but when we check using sudo -l it ask or password but
unfortunately we dont have password
 Now we check here for suid permissions
 using this command :
 find / -type f -perm -u=s 2>/dev/null


might have noticed the permissions on / bin / bash are a bit off. Usually / bin / bash does not
 have the setuid bit set:
 Check suid binary on gtfo bin


 And here we go we have here 
./bash -p
 we have the path of bash /usr/bin/bash
 use this command : 
/usr/bin/bash -p




 root!!!!!!!
 🥳
 "I hope you found this explanation helpful in understanding how I solved the challenge!
 If you liked it or have any suggestions on how I can improve, feel free to share—I’m
 always open to feedback. Your thoughts help me get better!"

This keeps it engaging, friendly, and professional while reflecting your open-minded attitude. Let
 me know if you'd like any further tweaks! 
