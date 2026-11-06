# Lab 3: Identify the Attacker's IP

**Result:** 90/100

## Scenario

A staff member reported unusual traffic to the company web server. The lab gives a pre-recorded capture of that traffic. The job was to analyse it in Wireshark and find out what kind of attack it was and which IP address was behind it.

## What I Did

1. I opened Wireshark in the lab. The capture was already loaded, so I checked how many packets it had to know how big the data was before filtering.
2. Most traffic in a capture is normal, so I used the display filter `tcp.flags.syn == 1`. It shows only the packets that start a TCP connection, and it cut the list down a lot.
3. In that list, most PCs sent one or two SYN packets. One address sent a long block of them, one after another, within a fraction of a second. That was the attacker.
4. I checked where that block was going. Every packet went to the same server, so that was the target.
5. In the packet details, the attacker's source port stayed the same in every packet, while the destination port kept changing.
6. I opened Statistics > Conversations (TCP tab) to see all the ports the attacker touched in one list.
7. I filtered on the attacker's address with `ip.addr == <attacker IP>` to see the traffic in both directions, including the server's replies.
8. Open ports replied with SYN, ACK. Closed ports replied with RST, ACK, which Wireshark colours dark red. I used this to sort the open ports from the closed ones.
9. Just before the scan, there was also a ping (ICMP) from the attacker to the server. It looks like the attacker checked that the host was alive first.

## What I Found

- The attacker sent connection requests to many ports on one server in a very short time
- The server's replies showed which ports were open and which were closed
- A ping came before the scan
- The attack type was a **port scan**

## A Mistake I Made

I lost 10 marks on the "ports probed" question. Later tasks asked for the open ports and the closed ports, and I got both of those right. Adding the two numbers together would have given me the total. Next time I will cross-check my answers against each other before I submit.

## What I Learned

- A display filter on the SYN flag is a fast way to find scanning
- Normal PCs make a few connections, scanners make many
- A server's replies show which ports are open and which are closed, so a scan can tell an attacker what is running
- Statistics > Conversations gives a clear overview that is hard to get from the packet list

## Screenshots

**Filtering to SYN packets only**

<img width="1920" height="1200" alt="lab3-task2-syn-filter" src="https://github.com/user-attachments/assets/19427a94-f7d5-4726-af3f-2ce052a57ed2" />

**Conversations window showing one source hitting many ports**

<img width="1920" height="1200" alt="lab3-task6-conversations" src="https://github.com/user-attachments/assets/079243c2-1911-4f37-92d4-e66554b90699" />

**Server replies to closed ports (RST, ACK)**

<img width="1920" height="1200" alt="lab3-task8-rst-ack" src="https://github.com/user-attachments/assets/d4ad1f6d-20ee-4afe-a10f-f907c519ae72" />

**The ping before the scan**

<img width="1920" height="1200" alt="lab3-task9-ping" src="https://github.com/user-attachments/assets/641941dd-5799-45e1-9c46-b38097d0197d" />

**Final result**

<img width="1920" height="1200" alt="lab3-result" src="https://github.com/user-attachments/assets/c2887881-cf10-4e29-a0e5-36b4f0539135" />
