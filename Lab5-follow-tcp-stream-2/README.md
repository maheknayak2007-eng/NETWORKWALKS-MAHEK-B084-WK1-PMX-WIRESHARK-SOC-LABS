# Lab 5: Follow TCP Stream, Part 2

**Result:** 100/100

## Scenario

A staff member browsed the company intranet. An admin thinks someone left a secret inside one of the web pages. The lab gives a pre-recorded capture of the traffic. The job was to use Follow TCP Stream to find the hidden text.

## What I Did

1. I opened Wireshark in the lab. The capture was already loaded, so I noted the number of packets.
2. The staff member had opened five pages, so I looked at the HTTP requests and filtered by stream, for example `tcp.stream eq <number>`, to check the pages one by one.
3. One page, `staff.html`, held the secret. I followed its TCP stream to read the whole request and the server's reply.
4. The note was not visible text. It was inside an HTML comment, so a person opening the page in a browser would never see it. In the capture it was easy to read.
5. The note named a backup server and an access code. The text was blue in the stream window, which means it travelled from the server to the client.
6. The server answered with HTTP status 200, which means the page was delivered normally.
7. The staff member had also downloaded a plain text file. I found that request with the display filter `http.request.uri contains "download"`.
8. I followed that stream too and read the file's contents, including who prepared the report.

## What I Found

- A secret can sit inside an HTML comment where users cannot see it, but the capture shows it
- A display filter on the request path can find one file in a big capture
- Both the page and the file were sent over plain HTTP, so everything was readable

## What I Learned

- HTML comments are hidden from the page, but they are not hidden from the network
- Never leave notes, access codes or server details in the code of a page
- `http.request.uri contains "..."` is a useful display filter for finding a specific file or page
- HTTP sends everything in clear text, which is why sites should use HTTPS

## Screenshots

**Filtering to the stream that carries the page**

<img width="1920" height="1200" alt="lab5-task2-stream-filter" src="https://github.com/user-attachments/assets/e3b471d8-ee53-4425-a2c5-ccadbcf09b19" />

**Follow TCP Stream window (sensitive text hidden)**

<img width="1920" height="1200" alt="lab5-task4-follow-stream" src="https://github.com/user-attachments/assets/f6d97eaa-a78b-4c06-9bca-926ec84a6d9b" />

**Finding the downloaded file with a display filter**

<img width="1920" height="1200" alt="lab5-task9-download-filter" src="https://github.com/user-attachments/assets/d53f3575-cb41-402a-81dc-4426a53a114f" />

**Final result**

<img width="1920" height="1200" alt="lab5-result" src="https://github.com/user-attachments/assets/812390c1-49fa-42e8-bb36-d783ca8816cd" />
