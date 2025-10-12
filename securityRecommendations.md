# Recommended, in‑scope mechanisms


The following items are in‑scope for ASVS. They should not be made mandatory but it is strongly
recommended to consider them as part of a secure application.

- A password strength meter should provided to help users set a stronger password.

- Create a publicly available security.txt file at the root or .well‑known directory of the application that clearly defines a link or e‑mail address for people to contact owners about security issues.

- Client‑side input validation should be enforced in addition to validation at a trusted service
layer as this provides a good opportunity to discover when someone has bypassed client‑side controls in an attempt to attack the application.

- Prevent accidentally accessible and sensitive pages from appearing in search engines using a robots.txt file, the X‑Robots‑Tag response header or a robots html meta tag.

- When using GraphQL, implement authorization logic at the business logic layer instead of the GraphQL or resolver layer to avoid having to handle authorization on every separate interface.