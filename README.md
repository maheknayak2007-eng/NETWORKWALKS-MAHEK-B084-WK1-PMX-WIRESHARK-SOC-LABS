# 🦈 Wireshark SOC Labs | Week 1 Extra Project

Networkwalks Cybersecurity Internship (Batch B084)

## 📌 Overview

This repository has my work for the extra Wireshark project from Week 1 of the Cybersecurity Internship at Networkwalks.

The project has six live SOC labs that run in the browser. Each lab gives a network capture and 10 tasks, and I have to investigate it like a SOC analyst: finding an attacker, reading hidden data, spotting passwords sent in clear text, and so on. The captures are pre-recorded by Networkwalks, so my job is to analyse them, not to generate the traffic. I am adding each lab to this repo as I finish it.

## Labs

- [Lab 3: Identify the Attacker's IP](Lab3-attacker-ip/README.md) (result: 90/100)
- [Lab 4: Follow TCP Stream 1](Lab4-follow-tcp-stream-1/README.md) (result: 80/100)
- [Lab 5: Follow TCP Stream, Part 2](Lab5-follow-tcp-stream-2/README.md) (result: 100/100)
- Lab 6: HTTP Plain Text Credentials (in progress)
- Lab 7: Catch the Brute Force Attacker (in progress)
- Lab 8: Catch the Call Scammer (in progress)

## What I Practiced

- Using display filters to cut a big capture down to the packets that matter
- Reading Statistics > Conversations to see who talked to whom, and on which ports
- Rebuilding a whole conversation with Follow TCP Stream
- Telling normal traffic from suspicious traffic, such as a port scan
- Seeing why unencrypted protocols like HTTP and plain text chat are risky

## Tools Used

- Wireshark (the browser version inside the Networkwalks SOC labs)
- Display filters, Conversations, Follow TCP Stream

## How This Repo Is Organised

Each lab has its own folder. Inside is a README with the scenario, the steps I followed, what I found, a mistake I made, and what I learned, plus screenshots from the lab.

## Key Takeaways

- Filtering first saves a lot of time. Most of a capture is normal traffic.
- Attacks leave patterns, like one device sending many connection requests to many ports.
- Anything sent in plain text can be read by anyone who captures it.
- I lost marks by rushing through small details, so I now re-read each question before I submit.

## ⚠️ Disclaimer

All work was done inside the practice labs provided by Networkwalks. The captures are pre-made, and I did not capture or scan anything myself. No real network or real data was involved. This project is for educational purposes only.
