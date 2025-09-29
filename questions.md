# OWASP

## Access Broken Control:

- Is the concept of Access Broken Control similar to encapulation?

- If a client is using raw SQL, are there other ways to ensure data is secure other than ensuring you sanitize and validate inputs as well as rate limiting?

- To my knowledge, using Passkeys are the most secure form of login for users, would the use of passkeys when logging in prevent some of the access control issues?

- Should you encrypt params like account numbers or hide it entirely on the client side?

## Cryptographic Failures:

- When using STARTTLS, how do you prevent the man in the middle attacks in the period before the data being transported is encrypted?


- Would the use of libraries such as bcrypt be the best way to ensure data is secured encrypted and prevent malicious actors from being able to access sensitive data?


- Is it ever wise for developers to develop their own cryptographic algorithms?


## Injections:

- How can hostile data be used within ORMs to extract additional, sensitive info? 

- What does it mean for hostile data to be concatenated?


## Insecure Design:

- If an application has an insecure design, what are things to consider when rewriting the application from scratch or patching thing up? 


- Can shifting left in coding help prevent an issue such as this? 

- If credential recovery that includes “questions and answers” is prohibited by NIST 800-63b, the OWASP ASVS and the OWASP top 10, why do so many applications use that as a valid recovery method?

## Security Misconfiguration:

- What are some examples of having error messages that are too detailed that can expose sensitive data or underlying flaws in your application?

## Vulnerable and Outdated Components:

- Are there ways to receive notifications if any of your software is out of date?

- How do you know what components are from official sources? Does secure links mean the links are HTTPS?


# Identity and Authentication Failures:

- Does the use of UUID help prevent Authentication failures?

- Should passkeys be optional considering it’s the most secure way to ensure proper authentication? If not, what to do about users who do not have passkey enabled devices considering the potential downsides of other forms of authentication?

- Is there a library that checks the user’s password against the 10,000 worst passwords list and is that necessary if you write strong enough password requirements?

## Security Logging and Monitoring Failures:

- Once you notice suspicious activity being logged to the server, what immediate steps do you take to ensure data integrity?


## Server-Side Request Forgery:

- Is implementing a proper CORS policy effective in preventing SSRF attacks?

- Does blocking API testing tools like Postman or cURL improve API security?

## Other questions?

- Are static languages such as typescript similar to SAST tools?

- If a client is using raw SQL, are there other ways to ensure data is secure other than ensuring you sanitize and validate inputs as well as rate limiting?  

- To my knowledge, using Passkeys are the most secure form of login for users, would the use of passkeys when logging in prevent some of the access control issues? 

- Should you encrypt params like account numbers or hide it entirely on the client side?  

- Is any data transmitted in clear text? This includes protocols such as HTTP, SMTP, FTP also using TLS upgrades like ([STARTTLS](https://mailtrap.io/blog/starttls-ssl-tls/)). External internet traffic is hazardous. Verify all internal traffic between [load balancers](https://www.cloudflare.com/learning/performance/what-is-load-balancing/), web servers, or back-end systems.  

- Are any old or weak cryptographic algorithms or protocols used either by default or in older code?

- Are default crypto keys in use, weak crypto keys generated or re-used, or is proper key management or rotation missing? Are crypto keys checked into source code repositories?  

- Is encryption not enforced, e.g., are any HTTP headers (browser) security directives or headers missing?  

- Is the received server certificate and the trust chain properly validated?  

- Are initialization vectors ignored, reused, or not generated sufficiently secure for the cryptographic mode of operation? Is an insecure mode of operation such as ECB in use? Is encryption used when authenticated encryption is more appropriate?  

- Are passwords being used as cryptographic keys in absence of a password base key derivation function?  

- Is randomness used for cryptographic purposes that was not designed to meet cryptographic requirements? Even if the correct function is chosen, does it need to be seeded by the developer, and if not, has the developer over-written the strong seeding functionality built into it with a seed that lacks sufficient entropy/unpredictability? (What does this mean?)  

- Are deprecated hash functions such as MD5 or SHA1 in use, or are non-cryptographic hash functions used when cryptographic hash functions are needed?

- When using STARTTLS, how do you prevent the man in the middle attacks in the period before the data being transported is encrypted?  

- Would the use of libraries such as bcrypt be the best way to ensure data is secured encrypted and prevent malicious actors from being able to access sensitive data?  

- Is it ever wise for developers to develop their own cryptographic algorithms? 

- How can hostile data be used within ORMs to extract additional, sensitive info?  

- What does it mean for hostile data to be concatenated?  

- If an application has an insecure design, do you have to rewrite the application from scratch?  

- Can [shifting left in coding](https://www.dynatrace.com/news/blog/what-is-shift-left-and-what-is-shift-right/) help prevent an issue such as this?  

- If credential recovery that includes “questions and answers” is prohibited by NIST 800-63b, the OWASP ASVS and the OWASP top 10, why do so many applications use that as a valid recovery method? 