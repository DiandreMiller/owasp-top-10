WYSIWYG editors

Why is eval() dangerous

Spring Expression Language (SpEL)

JNDI injection

memcache

SMTP or IMAP injection.

ReDoS or Runaway Regex attacks

stack randomization

The conversion of data from a stored or transmitted representation into actual application objects
(deserialization) has historically been the cause of various code injection vulnerabilities. It is impor‑
tant to perform this process carefully and safely to avoid these types of issues.

Deserialization Attacks

XML eXternal Entity (XXE) attacks.

Remote File Inclusion (RFI)

Server‑side Request Forgery (SSRF) attacks.

Business Logic

XXE attacks

DTCs

JSON Schema validation

HTTP Strict Transport Security (HSTS)

Content Security Policy (CSP)

DOM clobbering

redress attacks

cross‑site request forgery (CSRF)


Verify that when the application writes a cookie, the cookie name and value
length combined are not over 4096 bytes. Overly large cookies will not be
stored by the browser and therefore not sent with requests, preventing the
user from using application functionality which relies on that cookie.

nonces

Cross‑Origin Read Blocking (CORB)

tabnabbing and frame
counting

JSONP

Cross‑Site Script Inclusion

Verify that the application shows a notification when the user is being
redirected to a URL outside of the application’s control, with an option to
cancel the navigation.

request smuggling, 

response splitting, 

header injection, 

denial of service

HTTP/2

HTTP/3

CR (\r), LF (\n), or CRLF
(\r\n) sequences

Header Injection Attacks

pixel flood attacks

local or
remote file inclusion (LFI, RFI)

RFC 6266

NIST SP 800‑63

anti‑automation

IDO
hardware key

Cryptographically Secure
Pseudorandom Number Generator (CSPRNG)

VOIP

number porting

Note that NIST has also recently provided guidance which discourages the use of push notifications.
While this ASVS section does not do so, it is important to be aware of the risks of“push bombing”.

replay attacks

 OIDC

cryptographically secure pseudo‑random
number generator (CSPRNG)

insecure direct object reference (IDOR) and broken object level
authorization (BOLA)

broken
object property level authorization (BOPLA)

The most common examples of self‑contained tokens
are JSON Web Tokens (JWTs) and SAML assertions

 The allowlist must include the
permitted algorithms, ideally only either symmetric or asymmetric
algorithms, and must not include the‘None’algorithm. 