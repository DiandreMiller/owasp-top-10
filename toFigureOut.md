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

key derivation functions (KDF),

key derivation functions (KDF),

Diffie‑Hellman
and Elliptic Curve Diffie‑Hellman (ECDH)

RSA keys which are vulnerable to
Fermat factorization.

Online Certificate Status
Protocol (OCSP) Stapling

Verify that Encrypted Client Hello (ECH) is enabled in the application’s TLS
settings to prevent exposure of sensitive metadata, such as the Server Name
Indication (SNI), during TLS handshake processes.

back‑off algorithms.

Web Cache Deception attacks

mix‑up attacks

Demonstration of Proof of Possession (DPoP).

authorization code interception attacks

proof key for code
exchange (PKCE)

pushed authorization request (PAR) or JWT‑secured Authorization
Request (JAR)

Rich Authorization
Requests (RAR)

Verify that all cryptographic primitives utilize a minimum of 128‑bits of
security based on the algorithm, key size, and configuration.

Padding Oracle attacks

MAC
algorithm 

sandboxing

dependency confusion attack

containerization

What is the purpose of docker

type juggling, prototype pollution

semaphores

race conditions

time‑of‑check to time‑of‑use (TOCTOU) 

SIEM

 Applica‑
tions must also fail securely, avoiding unnecessary disclosure or disruption.

Verify that each log entry includes necessary metadata (such as when,
where, who, what) that would allow for a detailed investigation of the
timeline when an event happens.

log
injection

Verify that logs are securely transmitted to a logically separate system for
analysis, detection, alerting, and escalation. The aim is to ensure that if the
application is breached, the logs are not compromised.

circuit breakers
or graceful degradation

last‑resort event handlers

Web Real‑Time Communication (WebRTC) 

TURN (Traversal Us‑
ing Relays around NAT) servers.

validating timestamps

Datagram Transport Layer Security (DTLS)

Real‑time Transport Protocol (SRTP)

Real‑time Transport Protocol (RTP) injection attacks

Verify that the media server is not susceptible to the“ClientHello”Race
Condition vulnerability in Datagram Transport Layer Security (DTLS) by
checking if the media server is publicly known to be vulnerable or by
performing the race condition test.