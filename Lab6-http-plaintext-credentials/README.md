# Lab 6: HTTP Plain Text Credentials

**Result:** 100/100

## Scenario

An old staff portal still runs on plain HTTP. The lab gives a pre-recorded capture of traffic to that portal. The job was to find out what a person can read from a sign-in that is not encrypted.

## What I Did

1. I opened Wireshark in the lab. The capture was already loaded, so I noted the number of packets.
2. A sign-in form sends the typed values to the server in a POST request, so I used the display filter `http.request.method == "POST"`. That left only two packets.
3. Both packets went to the same login page, and both came from the same PC. This showed me the user submitted the sign-in form twice.
4. I clicked one of the POST packets and expanded **HTML Form URL Encoded** in the packet details. It lists the typed username and password in plain, easy-to-read lines.
5. Both attempts used the same username but different passwords. The second sign-in was the one that worked, so the password in the second packet was the accepted one.
6. The fix for this is to use HTTPS, which encrypts the traffic so the form values cannot be read from a capture.

## What I Found

- The portal sent the sign-in over plain HTTP, with no encryption
- The username and password were readable straight from the packet details
- Both attempts were visible, including the wrong password from the first try
- In this capture the wrong password was very close to the working one, so even a failed attempt gives hints to someone watching

## What I Learned

- Filtering on `http.request.method == "POST"` is a fast way to find forms and sign-ins
- The HTML Form URL Encoded section shows typed values as a simple list
- HTTP sends everything in clear text, and HTTPS is the fix
- The same risk applies to other clear text protocols, like FTP and Telnet

## Screenshots

Passwords and usernames are hidden in these screenshots.

**Filtering to POST requests**

<img width="1920" height="1200" alt="lab6-task3-post-filter" src="https://github.com/user-attachments/assets/00ad2d93-dde0-436f-8113-e96cd87c6f28" />

**The HTML Form URL Encoded section**

<img width="1920" height="1200" alt="lab6-task9-form-urlencoded" src="https://github.com/user-attachments/assets/e1f7bc82-a0ab-423c-8aec-d2a650e866ab" />

**The fix: use HTTPS**

<img width="1920" height="1200" alt="lab6-task10-https-fix" src="https://github.com/user-attachments/assets/2b57b78b-7415-4fdc-b186-cba8a75963fd" />

**Final result**

<img width="1920" height="1200" alt="lab6-result" src="https://github.com/user-attachments/assets/1aad100d-9a59-4a99-9b28-adb8496d6cdf" />
