# Q1: Web Exploitation: 

Once upon a time, in a neon-lit battlefield, there existed a valorant agent 'Raze'. Raze was the explosive duelist who could conquer enemies but not languages. For him, Egyptian was too cryptic yet French too simple (earning only a “B”), and the elusive “S” grade was always out of reach. Raze was determined to hack her way to glory ("S grade"). She discovered her teacher’s admin portal where by getting through, she might just blast open the hidden path to her long-sought 'S' grade. Can you help her?
http://r4z3k1lljoy.ch25.acmvit.in 
PS: Certain <ins>roles</ins> hold more weight than others. A <ins>small adjustment</ins> might unlock hidden access, keep most of it unchanged and consider what <ins>“none”</ins> could imply.

The goal is to gain access to the admin portal.
### Tools
* burp suite
* jwt.io
* devtools

By navigating the website it was clear that the admin page that we have to get access was already provided. We have to gain authorization for it. 

<img width="400" alt="Screenshot 2026-01-07 215816" src="https://github.com/user-attachments/assets/8cc4894c-8e46-4f62-8ad6-e540e9feea9f" />    <img width="400" alt="image" src="https://github.com/user-attachments/assets/0d1e43cb-9ca0-4b83-a486-18d3447b8849" />

We check the https request which is sent on clicking Proceed to portal by intercepting it on burpsuite.

<img width="1902" height="1116" alt="image" src="https://github.com/user-attachments/assets/4e31d1bd-a7b2-46e5-a0c4-5b41db6417ad" />

This indicated that session data was being stored client-side. We proceed to decode the cookie.

---

## Cookie Analysis

The session cookie value was Base64-encoded multiple times. Decoding it revealed a **JSON Web Token (JWT)** with signature:

<img width="1892" height="1111" alt="Screenshot 2026-01-07 211851" src="https://github.com/user-attachments/assets/f99ba9d4-79c7-4423-9967-efcd617d925c" />

---

## Vulnerability

This showed that authorization was based on the JWT payload. The application trusted the role value inside the JWT to control access.
This is a `Broken Access Control / JWT Misconfiguration vulnerability`.
Also, the hint emphasized on the word "none", which pointed towards a potential JWT `alg=none` attack.

---

## Exploitation

we modify the header and payload according to the hints provided in the problem and use jwt.io produce a token.

<img width="1920" height="1140" alt="image" src="https://github.com/user-attachments/assets/b45e8777-f1ee-4e52-94a0-06b64d7790c9" />


This token is encoded using base64 untill it is double padded.

<img width="1900" height="692" alt="image" src="https://github.com/user-attachments/assets/d0a357c8-2100-46ab-8319-b99c938f8a59" />


The encoded JWT was then placed back into the cookie and the request is sent.

<img width="1920" height="1200" alt="Screenshot 2026-01-07 211737" src="https://github.com/user-attachments/assets/81200461-dddd-4e1a-9d04-0998aa83e9ab" />
<img width="773" height="223" alt="Screenshot 2026-01-07 211811" src="https://github.com/user-attachments/assets/b913e741-b3d5-4d46-97db-1c7262d00256" />

The response clearly indicates successful authorization.🎉🎉


The cookie can also be modified in the developer tools in a broswer.

<img width="1920" height="1200" alt="Screenshot 2026-01-07 211656" src="https://github.com/user-attachments/assets/05cb7094-34a0-47d1-ab08-c06516a211a5" />
<img width="875" height="431" alt="Screenshot 2026-01-07 211502" src="https://github.com/user-attachments/assets/fab2726c-4208-4c49-a111-7efcd132dce0" />

