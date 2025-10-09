#  Interview Questions:

**Question 1:** Look up examples of cross site scripting attacks and SQL injections.



**Question 2:** How to prevent scripting attacks?

You can prevent scripting attacks by sanitizing inputs and validating inputs

**Question 3:** What is the purpose of burp suite?



**Question 4:** Vulnerabilities of above design:

![Vulnerable Client Server Database Design](assets/flawedClientServerDiagram.png)

**Question 5:** Network vulnerabilities. What are examples of network attacks and vulnerabilities?



**Question 6:** Wireshark and tools for LLM injections.



**Question 7:** What to do if you get a really large cookie of human indistinguishable text? What tools can you use to figure out what the cookie is?

1. Identify the Format:

- Base64/JWT: Even if it look random, try base64-decoding. Many web frameworks base64-encode session data. If it's JWT you'll see JSON structure ({ "alg": ..., "typ": ... } in the header).

- Encrypted Seesion Token: Some frameworks (like Rails, Django, Sping) encrypt the whole session onject into the cookie. If so, you won't be able to read it without the server's key.

- Opaque Session ID: It might just be a long random string that's a pointer to session data on the server - this is actually the safest approach.

2. Security Checks You Should Perform:

- Check the cookie attributes:

    - Secure (only sent over HTTPS).

    - HTTPOnly (not accesible to Javascript).

    - SameSite (helps prevent CSRF).

- Size: Browser cookies have a 4 KB limit: If this one is far larger, it is a sign of bad design or possible leakage.

- Transport: Ensure it's being sent only over TLS.

3. Risks of Large Non-Readable Cookies

- Framework Session Storage: If it's storing session state clinet-side, it could bloat quickly and expose risks if encryption isn't solid. 

- Key Mismanagement: If weak cypto or predictable keys are used, attackers could forge session cookies.

- Hidden Data Leakage: Even though it looks random, it might hide sensitive info like user roles or PII.

4. As a Security Student, Next Steps:

- Try base64 decoding (sometimes multiple layers).

- It it's a JWT, inspect the claims and algorithm. 

- If it stays unreadable after decoding attempts, assume it was encrypted and focus on:

 - Whether the app reies too heavily on client-side state instead of server-side sessions. 
 
- Document the cookie size, attributes, and risks.

