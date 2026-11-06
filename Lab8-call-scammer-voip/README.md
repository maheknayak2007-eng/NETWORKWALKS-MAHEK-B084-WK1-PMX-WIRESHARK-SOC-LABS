# Lab 8: Catch the Call Scammer (VoIP Call Replay)

**Result:** 90/100

## Scenario

A phone call was made through the company VoIP system. The lab gives a pre-recorded capture of the network traffic. The job was to find the call and play it back to learn what was said.

## What I Did

1. I opened Wireshark in the lab. The capture was already loaded, so I noted the number of packets.
2. A call has two parts: the setup and the voice. The setup uses SIP, so I filtered with `sip`. Only a few packets were left, showing the call starting (INVITE, Trying, Ringing, OK, ACK) and ending (BYE, OK).
3. The voice travels as RTP, a steady stream of small packets. I filtered with `rtp`, and it was most of the capture.
4. I opened the INVITE packet and read the SIP headers. The From header shows who is calling and the To header shows who is being called.
5. I clicked an RTP packet and checked the payload type in the details to find the codec, which was G.711 PCMU.
6. I played the call back with the lab's player and listened to it. [Edit if you did this differently.]
7. In the call, payment card details were read out loud, and I could hear them clearly.
8. The fix is to encrypt the call with SRTP, so the voice cannot be replayed from a capture.

## What I Found

- The call setup (SIP) and the voice (RTP) were separate and easy to filter
- The voice was not encrypted, so the call could be played back from the capture
- Private information, including payment card details, was spoken during the call and could be heard by anyone with the capture

## A Mistake I Made

I lost 10 marks on the caller's extension. I used the number from the first line of the INVITE, but that line shows the extension being **called**. The caller's number is in the **From** header. Next time I will read the whole SIP header and not only the first line.

## What I Learned

- SIP sets up and ends the call, and RTP carries the voice
- If a call is not encrypted, someone with a capture can replay it
- Anything said on an unencrypted call, such as card details, is exposed
- Read the full header before answering a question about who called whom

## Screenshots

**Filtering the call setup (SIP)**

![SIP filter](lab8-task2-sip-filter.png)

**Filtering the voice stream (RTP)**

![RTP filter](lab8-task3-rtp-filter.png)

**Finding the codec in the RTP details**

![Codec](lab8-task6-codec.png)

**The fix: encrypt the call (SRTP)**

![SRTP fix](lab8-task10-srtp-fix.png)

**Final result**

![Result](lab8-result.png)
