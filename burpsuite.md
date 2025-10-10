# How Burp Suite Intercepts Traffic:

How it works (high level)
1.	Your browser opens a TLS connection to a site (e.g., https://example.com).
2.	Burp sits between your browser and the internet as a proxy. The browser is configured to send traffic to Burp instead of directly to the server.
3.	To the browser, Burp pretends to be the remote site by presenting a TLS certificate for example.com. Burp dynamically generates that certificate and signs it with its own Burp CA.
4.	The browser validates that certificate against its trusted root CAs. If the Burp CA is trusted by the browser/OS, the browser accepts the connection.
5.	Meanwhile, Burp opens a separate TLS connection to the real example.com. So Burp terminates TLS from the client and initiates TLS to the server — enabling it to see and modify plaintext requests/responses. This is classic MITM (man-in-the-middle).


