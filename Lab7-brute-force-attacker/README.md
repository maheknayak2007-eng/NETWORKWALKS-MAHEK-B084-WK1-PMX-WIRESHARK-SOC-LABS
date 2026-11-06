# Lab 7: Catch the Brute Force Attacker

**Result:** 100/100

## Scenario

The owner of an FTP server reports many failed sign-ins in the last few minutes. The lab gives a pre-recorded capture. The job was to find who is guessing passwords and whether the attacker got in.

## What I Did

1. I opened Wireshark in the lab. The capture was already loaded, so I noted the number of packets.
2. I opened Statistics > Protocol Hierarchy to see which protocols were in the capture. FTP made up almost a third of all packets, which is a lot for one protocol.
3. I used the display filter `ftp` to see only FTP traffic. The list showed login requests (USER and PASS) and the server's replies.
4. One address was sending all the login attempts, and they all went to the same FTP server.
5. The attacker kept trying the same username again and again with different passwords.
6. FTP replies have codes. 530 means "Login incorrect". I used the filter `ftp.response.code == 530` and read the number of failed logins from the status bar.
7. 230 means "Login successful". I looked through the capture and found one 230 reply near the end, so the attacker did get in.
8. After the successful login, the attacker ran a command to see the current directory and then quit.
9. The password used just before the 230 reply was the one that worked.

## What I Found

- One source, one server, one username, and many different passwords
- A pile of 530 replies in a short time, followed by a single 230
- The attacker got in after repeated guessing
- The attack type was **brute force**

## What I Learned

- Protocol Hierarchy gives a quick overview of a big capture
- Brute force looks like many failed logins in a row, then one success
- FTP sends usernames and passwords in clear text, so even the guesses can be read in the capture
- Ways to defend: limit failed attempts, use strong passwords, and use a secure alternative like SFTP

## Screenshots

Passwords are hidden in these screenshots.

**Protocol Hierarchy**

<img width="1920" height="1200" alt="lab7-task2-protocol-hierarchy" src="https://github.com/user-attachments/assets/2a77c58a-551c-4c3c-ac10-646a1ecc9d2b" />

**Filtering failed logins (530)**

<img width="1920" height="1200" alt="lab7-task7-failed-logins" src="https://github.com/user-attachments/assets/8c58b4a4-591e-45b9-8810-66b09cbd11b9" />

**The successful login (230)**

<img width="1920" height="1200" alt="lab7-task8-success" src="https://github.com/user-attachments/assets/2977d62f-627a-44b9-bc77-c7a0a471c6bb" />

**Final result**

<img width="1920" height="1200" alt="lab7-result" src="https://github.com/user-attachments/assets/cdcf0b7e-75ba-45bb-b623-f862a8c304bd" />
