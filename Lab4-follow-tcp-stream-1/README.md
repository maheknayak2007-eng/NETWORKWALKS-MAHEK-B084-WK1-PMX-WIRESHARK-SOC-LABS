# Lab 4: Follow TCP Stream 1

**Result:** 80/100

## Scenario

The manager says some staff use an old office chat tool that sends messages in plain text. The lab gives a pre-recorded capture of the traffic. The job was to use Follow TCP Stream to read one chat and see what was shared.

## What I Did

1. I opened Wireshark in the lab. The capture was already loaded, so I noted the number of packets.
2. I opened Statistics > Conversations and looked at the TCP tab. Most connections were normal web traffic on ports 80 and 443, but one conversation used a different port. That was the chat tool.
3. I filtered on that port with `tcp.port == <chat port>`. The first packet with the SYN flag shows which computer started the chat, and that is the client.
4. I right-clicked a packet and used Analyze > Follow > TCP Stream. The window title shows the stream number as `tcp.stream eq <number>`.
5. The window rebuilt the whole chat as readable text. The bottom bar shows how many bytes the conversation had.
6. I read the chat. A staff member from Accounts asked IT for help with a shared drive, and IT reset the access. Both a temporary password and a guest Wi-Fi password were sent in the chat in plain text.
7. Wireshark colours the text by direction: client text in one colour, server text in the other.

## What I Found

- The chat ran on its own port, separate from the web traffic
- The whole conversation could be read word for word
- Two passwords were sent without any protection, so anyone capturing the traffic could read them

## Mistakes I Made

I lost 20 marks in this lab, on two questions:

- **Stream number:** the question asked for the number, and I typed the whole filter text from the window title instead. Lesson: read exactly what the question asks for.
- **Text colour:** I picked the wrong colour for the client. In Follow TCP Stream the client's text is red and the server's text is blue. I know it now.

## What I Learned

- Follow TCP Stream turns hundreds of packets into one readable conversation
- Plain text protocols are unsafe, because passwords and other private data can be read straight from the capture
- Chat tools and similar services should use encryption
- Slow down and read each question properly, because small mistakes cost marks

## Screenshots

**Conversations window showing the one unusual port**

<img width="1920" height="1200" alt="lab4-task2-conversations" src="https://github.com/user-attachments/assets/60d3598c-1429-40fb-a837-24a510ed038a" />

**Filtering on the chat port to see how the connection started**

<img width="1920" height="1200" alt="lab4-task3-port-filter" src="https://github.com/user-attachments/assets/2b5b32a1-5522-4405-9ea9-b879932bf9d4" />

**Follow TCP Stream window (sensitive text hidden)**

<img width="1920" height="1200" alt="lab4-task4-follow-stream" src="https://github.com/user-attachments/assets/b961e2ae-ded8-4f76-b13b-23c7090e73cc" />

**Final result**

<img width="1920" height="1200" alt="lab4-result" src="https://github.com/user-attachments/assets/fa91f5d8-7906-4904-bf4e-3a49ece13267" />
