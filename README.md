# Bounty-Hacker
A beginner level Try Hack Me box that uses nmap, hydra, and privilege escalation.

### Enumeration

The first thing I did was run a nmap scan to determine what ports were open. The scan returned the results that ftp, ssh, and http were open. It is a critical vulnerability having port 21 (ftp) open because the default credientials are anonymous:. With no password, it is easy to gain access and download files. Port 22 (ssh) being open is also a critical vulnerability because if a username is found it can be brute-forced and used to log into a user's terminal.
The second step to my enumeration was to go to the webpage to see if there was any valuable information, which I didn't find.

Command: namp -sCV 10.10.212.36
![nmap scan](https://github.com/lindseytwilson/Bounty-Hacker/blob/main/Images/nmap.png)

### Task 1: Who wrote the task list?

The first task was to determine who wrote the task list

Commands:
- ftp 10.10.212.36
- ls -al
- get task.txt
- get locks.txt


### Task 2: What service can you bruteforce with the text file found?


### Task 3: What is the users password? 


### Task 4: user.txt


### Task 5: root.txt
