# 🦈 Wireshark SOC Labs | Week 1 Extra Project
 
Networkwalks Cybersecurity Internship (Batch [YOUR BATCH])
 
## 📌 Overview
 
This repository has my work for the extra Wireshark project from Week 1 of the Cybersecurity Internship at Networkwalks.
 
The project has six live SOC labs that run in the browser. Each lab gives a network capture and 10 tasks, and I investigate it like a SOC analyst: finding an attacker, reading hidden data, spotting passwords sent in clear text, catching a brute force attack, and replaying a phone call. The captures are pre-recorded by Networkwalks, so my job is to analyse them, not to generate the traffic. All six labs are done and documented here.
 
## Labs
 
- [Lab 3: Identify the Attacker's IP](Lab3-attacker-ip/README.md) (result: 90/100)
- [Lab 4: Follow TCP Stream 1](Lab4-follow-tcp-stream-1/README.md) (result: 80/100)
- [Lab 5: Follow TCP Stream, Part 2](Lab5-follow-tcp-stream-2/README.md) (result: 100/100)
- [Lab 6: HTTP Plain Text Credentials](Lab6-http-plaintext-credentials/README.md) (result: 100/100)
- [Lab 7: Catch the Brute Force Attacker](Lab7-brute-force-attacker/README.md) (result: 100/100)
- [Lab 8: Catch the Call Scammer (VoIP)](Lab8-call-scammer-voip/README.md) (result: 90/100)
## What I Practiced
 
- Using display filters to cut a big capture down to the packets that matter
- Reading Statistics > Conversations and Protocol Hierarchy to understand a capture quickly
- Rebuilding a whole conversation with Follow TCP Stream
- Telling normal traffic from suspicious traffic, such as a port scan or a brute force attack
- Reading clear text credentials in HTTP and FTP
- Reading SIP and RTP to understand a VoIP call
- Seeing why unencrypted protocols are risky and what fixes them
## Tools Used
 
- Wireshark (the browser version inside the Networkwalks SOC labs)
- Display filters, Conversations, Protocol Hierarchy, Follow TCP Stream, packet details
## How This Repo Is Organised
 
Each lab has its own folder. Inside is a README with the scenario, the steps I followed, what I found, what I learned, and screenshots from the lab. Where I lost marks, I wrote down the mistake.
 
## Key Takeaways
 
- Filtering first saves a lot of time. Most of a capture is normal traffic.
- Attacks leave patterns: many connection requests to many ports is a scan, and many failed logins followed by one success is brute force.
- Anything sent in plain text (HTTP, FTP, chat, unencrypted calls) can be read by anyone who captures it.
- The fix for most of these is encryption: HTTPS, secure alternatives to FTP, and SRTP for calls.
- I lost marks by rushing through small details, so I now re-read each question before I submit.
## ⚠️ Disclaimer
 
All work was done inside the practice labs provided by Networkwalks. The captures are pre-made, and I did not capture or scan anything myself. No real network or real data was involved. Passwords and other sensitive text from the labs are hidden in the screenshots. This project is for educational purposes only.
