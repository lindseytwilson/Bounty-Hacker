# Bounty-Hacker
A beginner level Try Hack Me box that uses nmap, hydra, and privilege escalation.

### Enumeration

The first thing I did was run a nmap scan to determine what ports were open. The scan returned the results that ftp, ssh, and http were open. It is a critical vulnerability having port 21 (ftp) open because the default credentials are anonymous:. With no password, it is easy to gain access and download files. Port 22 (ssh) being open is also a critical vulnerability because if a username is found it can be brute-forced and used to log into a user's terminal.

The second step to my enumeration was to go to the webpage to see if there was any valuable information, which I didn't find.

Command: namp -sCV 10.10.212.36
![nmap scan](https://github.com/lindseytwilson/Bounty-Hacker/blob/main/Images/nmap.png)

Website
![website](https://github.com/lindseytwilson/Bounty-Hacker/blob/main/Images/Webpage.png)

### Task 1: Who wrote the task list?

The first task was to determine who wrote the task list. By logging into ftp I was able to find two files. By using the 'get' command, I was able to download the files to my kali machine. Once downloading and concatenating the files, it was determined that Lin wrote the task list. Another useful find came from the locks.txt file. This file showed what appears to be a list of passwords, which will be helpful with the next task.

Commands:
- ftp 10.10.212.36
- ls -al
- get task.txt
- get locks.txt

![ftp enumeration](https://github.com/lindseytwilson/Bounty-Hacker/blob/main/Images/ftp.png)

locks.txt and task.txt

![cat files](https://github.com/lindseytwilson/Bounty-Hacker/blob/main/Images/Task%20and%20Locks%20Files.png)

### Task 2: What service can you bruteforce with the text file found?

Now that we have a username, we are able to brute-force open port 22 (ssh).

### Task 3: What is the users password? 

Hydra is the best tool to brute-force Lin's password. We can run it against the locks.txt file found when enumerating ftp.

Command: hydra -l lin -P locks.txt -f ssh://10.10.212.36

Command Breakdown:
- hydra: a network logon cracker
- -l: flag for the login name
- lin: name of the user we're cracking a password for
- -P: flag to load passwords from a specific file
- locks.txt: name of file with passwords
- -f: stop running after the first correct username/password combination
- ssh://10.10.212.36: ip address specifying we're looking for a ssh login

![hydra](https://github.com/lindseytwilson/Bounty-Hacker/blob/main/Images/Hydra.png)

### Task 4: user.txt

I was able to ssh into Lin's terminal, once gaining access I was able to run the following commands to locate the user.txt flag.

![ssh to Lin](https://github.com/lindseytwilson/Bounty-Hacker/blob/main/Images/ssh%20to%20Lin.png)

Command:
- ls
- cat user.txt

![user.txt](https://github.com/lindseytwilson/Bounty-Hacker/blob/main/Images/user%20txt.png)

### Task 5: root.txt

Now to the final step, privilege escalation. The first step is to see what sudo privileges Lin has. Once determining this, I can use gtfobins.github.io to find a sudo privilege escalation command.

sudo -l showed that Lin has permissions in /bin/tar. After getting the permissions I found a command that would escalate my privileges and open up a shell, allowing me navigate to the root directory to find the final flag. 

sudo -l

![sudo privileges](https://github.com/lindseytwilson/Bounty-Hacker/blob/main/Images/Sudo%20Permissions.png)

Privilege Escalations

![privilege escalation](https://github.com/lindseytwilson/Bounty-Hacker/blob/main/Images/Privilege%20Escalation.png)
