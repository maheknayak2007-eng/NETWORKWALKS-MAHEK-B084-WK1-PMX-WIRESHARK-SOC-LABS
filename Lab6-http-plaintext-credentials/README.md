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

![POST filter](lab6-task3-post-filter.png)

**The HTML Form URL Encoded section**

![Form URL Encoded](lab6-task9-form-urlencoded.png)

**The fix: use HTTPS**

![HTTPS fix](lab6-task10-https-fix.png)

**Final result**

![Result](lab6-result.png)
