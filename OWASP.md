# OWASP-Top-10 Top 10 Web Application Security Risks

## Access Broken Control:

94 percent of applications were tested for some form of broken access control. The 34 Common Weakness Enumerations (CWEs) mapped to Broken Access Control had more occurrences in applications than any other category.

### Description:

Access control enforces policy that users cannot act outside of their intended permissions. Failure typically leads to unauthorized information disclosure, modification, or destruction of all data or performing a business function outside the user’s limits. Common access control vulnerabilities include:

- Violations of principle of least privilege or deny by default, where access should only be granted for particular capabilities, roles, or users, but is available to anyone.  
- Bypassing access control checks by modifying the URL ([parameter tampering](https://owasp.org/www-community/attacks/Web_Parameter_Tampering) or [force browsing](https://owasp.org/www-community/attacks/Forced_browsing)), internal application state, or the HTML page, or by using an attack tool modifying API requests.  
- Permitting viewing or editing someone else’s account by providing it’s unique identifier (insecure direct object references)  
- Accessing API with missing access controls for POST, PUT, DELETE.  
- Elevation of privilege. Acting as a user without being logged in or acting as an admin when logged in as a user.  
- Metadata manipulation, such as replaying or tampering with a JSON Web token (JWT) access control token, or a cookie or hidden field manipulated to elevate privileges or abusing JWT invalidation.  
- CORS misconfiguration allows API access from unauthorized/untrusted origins.  
- Force browsing to authenticate pages as an unauthenticated user or to privileged pages as a standard user.  

### How to Prevent:

Access control is only effective in trusted server-side code or server-less API, where the attacker cannot modify the access control check or metadata.

- Except for public resources, deny by default.  
- Implement access control mechanisms once and reuse them throughout the application, including minimizing (CORS) usage.  
- Model access controls should enforce record ownership rather than accepting that the user can perform CRUD operations on any record.  
- Unique application business limits requirements should be enforced by [domain models](https://simplea.com/resources/articles/what-is-a-domain-model).  
- Disable web server directory listing and ensure file metadata (git) and backup files are not present within web roots.  
- Log access control failures, alert admins when appropriate (repeated failures)  
- Rate limit API and controller access to minimize the harm from automated attack tooling.  
- Stateful session identifiers should be invalidated on the server after logout. Stateless JWT tokens should rather be short-lived so that the window of opportunity for an attacker is minimized. For longer lived JWTs it is recommended to follow the OAuth standards to revoke access.  

### Questions:

- Is this similar to encapsulation?  
- If a client is using raw SQL, are there other ways to ensure data is secure other than ensuring you sanitize and validate inputs as well as rate limiting?  
- To my knowledge, using Passkeys are the most secure form of login for users, would the use of passkeys when logging in prevent some of the access control issues?  
- Should you encrypt params like account numbers or hide it entirely on the client side?  

(Add Examples)

---

## Cryptographic Failures:

Cryptographic failures or the lack thereof can lead to data leaks or compromises system databases. The first thing to determine is the protection needs of data in transit and at rest. For example, password, credit card numbers (apple does this with apple pay similar to passkeys), health records, personal information, and business secrets require extra protection, mainly if the data falls under privacy laws such as EU’s General Data Protection such as PCI Data Security Standard (PCI DSS). For all such data:

- Is any data transmitted in clear text? This includes protocols such as HTTP, SMTP, FTP also using TLS upgrades like ([STARTTLS](https://mailtrap.io/blog/starttls-ssl-tls/)). External internet traffic is hazardous. Verify all internal traffic between [load balancers](https://www.cloudflare.com/learning/performance/what-is-load-balancing/), web servers, or back-end systems.  
- Are any old or weak cryptographic algorithms or protocols used either by default or in older code?  
- Are default crypto keys in use, weak crypto keys generated or re-used, or is proper key management or rotation missing? Are crypto keys checked into source code repositories?  
- Is encryption not enforced, e.g., are any HTTP headers (browser) security directives or headers missing?  
- Is the received server certificate and the trust chain properly validated?  
- Are initialization vectors ignored, reused, or not generated sufficiently secure for the cryptographic mode of operation? Is an insecure mode of operation such as ECB in use? Is encryption used when authenticated encryption is more appropriate?  
- Are passwords being used as cryptographic keys in absence of a password base key derivation function?  
- Is randomness used for cryptographic purposes that was not designed to meet cryptographic requirements? Even if the correct function is chosen, does it need to be seeded by the developer, and if not, has the developer over-written the strong seeding functionality built into it with a seed that lacks sufficient entropy/unpredictability? (What does this mean?)  
- Are deprecated hash functions such as MD5 or SHA1 in use, or are non-cryptographic hash functions used when cryptographic hash functions are needed?  

### Questions:

- When using STARTTLS, how do you prevent the man in the middle attacks in the period before the data being transported is encrypted?  
- Would the use of libraries such as bcrypt be the best way to ensure data is secured encrypted and prevent malicious actors from being able to access sensitive data?  
- Is it ever wise for developers to develop their own cryptographic algorithms?  

---

## Injection:

94% of the applications were tested for some form of injection with a max incidence rate of 19%, an average incidence rate of 3%, and 274k occurrences. Notable Common Weakness Enumerations (CWEs) included are CWE-79: Cross-site Scripting, CWE-89: SQL Injection, and CWE-73: External Control of File Name or Path.

An application is vulnerable to an attack when:  
- User data is not validated, filtered, or sanitized by the application.  
- Dynamic queries or non-parameterized calls without context aware escaping are used directly in the interpreter. Hostile data is used without (ORM) search parameters to extract additional sensitive records. (Research more)  
- Hostile data is directly used or concatenated. The SQL or command contains the structure and malicious data is dynamic queries, commands, or stored procedures. (Research more)  

Some of the more common injections are SQL, NoSQL, OS command, Object Relational Mapping (ORM), LDAP, and Expression Language (EL) or Object Graph Navigation Library (OGNL) injection. The concept is identical among all interpreters. Source code review is the best method of detecting if applications are vulnerable to injections. Automated testing of all parameters, headers, URL, cookies, JSON, SOAP, and XML data inputs is strongly encouraged. Organizations can include static (SAST), dynamic (DAST), and interactive (IAST) application security testing tools into the CI/CD pipeline to identify introduced injection flaws before production deployment.

### How to Prevent:

**Preventing injection requires keeping data separate from commands and queries:**

- The preferred option is to use a safe API, which avoids using the interpreter entirely, provides a parameterized interface, or migrates to Object Relational Mapping Tools (ORMs). Note: Even when parameterized, stored procedures can still introduce SQL injection if PL/SQL or T-SQL concatenates queries and data or executes hostile data with EXECUTE IMMEDIATE or exec(). (Did not know injections can be introduced even when using parameterized queries. Research more)  

- Use positive server-side input validation. This is not a complete defense as many applications require special characters, such as text areas or APIs for mobile applications.  

- For any residual dynamic queries, escape special characters using the specific escape syntax for that interpreter.  

- Note: SQL structures such as table names, column names, and so on cannot be escaped, and thus user-supplied structure names are dangerous. This is a common issue in report-writing software.  

(Include some examples)

### Questions:

- How can hostile data be used within ORMs to extract additional, sensitive info?  
- What does it mean for hostile data to be concatenated?  

---

## Insecure Design:

Insecure design is a broad category representing different weaknesses, expressed as “missing or ineffective control design.” Insecure design is not the source for all other Top 10 risk categories. There is a difference between insecure design and insecure implementation. We differentiate between design flaws and implementation defects for a reason, they have different root causes and remediation. A secure design can still have implementation defects leading to vulnerabilities that may be exploited. An insecure design cannot be fixed by a perfect implementation as by definition, needed security controls were never created to defend against specific attacks. One of the factors that contribute to insecure design is the lack of business risk profiling inherent in the software or system being developed, and thus the failure to determine what level of security design is required.

### Requirements and Resource Management

Collect and negotiate the business requirements for an application with the business, including the protection requirements concerning confidentiality, integrity, availability, and authenticity of all data assets and the expected business logic. Take into account how exposed your application will be and if you need segregation of tenants (additionally to access control). Compile the technical requirements, including functional and non-functional security requirements. Plan and negotiate the budget covering all design, build, testing, and operation, including security activities.

### Secure Design

Secure design is a culture and methodology that constantly evaluates threats and ensures that code is robustly designed and tested to prevent known attack methods. Threat modeling should be integrated into refinement sessions (or similar activities); look for changes in data flows and access control or other security controls. In the user story development determine the correct flow and failure states, ensure they are well understood and agreed upon by responsible and impacted parties. Analyze assumptions and conditions for expected and failure flows, ensure they are still accurate and desirable. Determine how to validate the assumptions and enforce conditions needed for proper behaviors. Ensure the results are documented in the user story. Learn from mistakes and offer positive incentives to promote improvements. Secure design is neither an add-on nor a tool that you can add to software.

### Secure Development Lifecycle

Secure software requires a secure development lifecycle, some form of secure design pattern, paved road methodology, secured component library, tooling, and threat modeling. Reach out for your security specialists at the beginning of a software project throughout the whole project and maintenance of your software. Consider leveraging the [OWASP Software Assurance Maturity Model (SAMM)](https://owaspsamm.org/) to help structure your secure software development efforts.

### How to Prevent

- Establish and use a secure development lifecycle with AppSec professionals to help evaluate and design security and privacy-related controls  
- Establish and use a library of secure design patterns or paved road ready to use components  
- Use threat modeling for critical authentication, access control, business logic, and key flows  
- Integrate security language and controls into user stories  
- Integrate plausibility checks at each tier of your application (from frontend to backend)  
- Write unit and integration tests to validate that all critical flows are resistant to the threat model. Compile use-cases and misuse-cases for each tier of your application.  
- Segregate tier layers on the system and network layers depending on the exposure and protection needs  
- Segregate tenants robustly by design throughout all tiers  
- Limit resource consumption by user or service  

### Questions:

- If an application has an insecure design, do you have to rewrite the application from scratch?  
- Can [shifting left in coding](https://www.dynatrace.com/news/blog/what-is-shift-left-and-what-is-shift-right/) help prevent an issue such as this?  
- If credential recovery that includes “questions and answers” is prohibited by NIST 800-63b, the OWASP ASVS and the OWASP top 10, why do so many applications use that as a valid recovery method?  

---

## Security Misconfiguration:

The application might be vulnerable if the application is:  
- Missing appropriate security hardening across any part of the application stack or improperly configured permissions on cloud services.  
- Unnecessary features are enabled or installed (e.g., unnecessary ports, services, pages, accounts, or privileges).  
- Default accounts and their passwords are still enabled and unchanged.  
- Error handling reveals stack traces or other overly informative error messages to users.  
- For upgraded systems, the latest security features are disabled or not configured securely.  
- The security settings in the application servers, application frameworks (e.g., Struts, Spring, ASP.NET), libraries, databases, etc., are not set to secure values.  
- The server does not send security headers or directives, or they are not set to secure values.  
- The software is out of date or vulnerable ([A06:2021-Vulnerable and Outdated Components](https://owasp.org/Top10/A06_2021-Vulnerable_and_Outdated_Components/)).  

Without a concerted, repeatable application security configuration process, systems are at a higher risk.

### How to Prevent

Secure installation processes should be implemented, including:  

- A repeatable hardening process makes it fast and easy to deploy another environment that is appropriately locked down. Development, QA, and production environments should all be configured identically, with different credentials used in each environment. This process should be automated to minimize the effort required to set up a new secure environment. (Learn more about)  
- A minimal platform without any unnecessary features, components, documentation, and samples. Remove or do not install unused features and frameworks.  
- A task to review and update the configurations appropriate to all security notes, updates, and patches as part of the patch management process ([A06:2021-Vulnerable and Outdated Components](https://owasp.org/Top10/A06_2021-Vulnerable_and_Outdated_Components/)). Review cloud storage permissions (e.g., S3 bucket permissions).  
- A segmented application architecture provides effective and secure separation between components or tenants, with segmentation, containerization, or cloud security groups (ACLs).  
- Sending security directives to clients, e.g., Security Headers  
- An automated process to verify the effectiveness of the configurations and settings in all environments.  

### Questions:

- What are some examples of having error messages that are too detailed that can expose sensitive data or underlying flaws in your application?  

Hi

---

## Vulnerable and Outdated Components:

You are likely vulnerable:

- If you do not know the versions of all components you use (both client-side and server-side). This includes components you directly use as well as nested dependencies.  
- If the software is vulnerable, unsupported, or out of date. This includes the OS, web/application server, database management system (DBMS), applications, APIs and all components, runtime environments, and libraries.  
- If you do not scan for vulnerabilities regularly and subscribe to security bulletins related to the components you use.  
- If you do not fix or upgrade the underlying platform, frameworks, and dependencies in a risk-based, timely fashion. This commonly happens in environments when patching is a monthly or quarterly task under change control, leaving organizations open to days or months of unnecessary exposure to fixed vulnerabilities.  
- If software developers do not test the compatibility of updated, upgraded, or patched libraries.  
- If you do not secure the components’ configurations ([A05:2021-Security Misconfiguration](https://owasp.org/Top10/A05_2021-Security_Misconfiguration/)).  

### How to Prevent

There should be a patch management process in place to:  

- Remove unused dependencies, unnecessary features, components, files, and documentation.  
- Continuously inventory the versions of both client-side and server-side components (e.g., frameworks, libraries) and their dependencies using tools like versions, OWASP Dependency Check, retire.js, etc. Continuously monitor sources like Common Vulnerability and Exposures (CVE) and National Vulnerability Database (NVD) for vulnerabilities in the components. Use software composition analysis tools to automate the process. Subscribe to email alerts for security vulnerabilities related to components you use.  
- Only obtain components from official sources over secure links. Prefer signed packages to reduce the chance of including a modified, malicious component ([A08:2021-Software and Data Integrity Failures](https://owasp.org/Top10/A08_2021-Software_and_Data_Integrity_Failures/)).  
- Monitor for libraries and components that are unmaintained or do not create security patches for older versions. If patching is not possible, consider deploying a virtual patch to monitor, detect, or protect against the discovered issue.  
- Every organization must ensure an ongoing plan for monitoring, triaging, and applying updates or configuration changes for the lifetime of the application or portfolio.  

### Questions:

- Are there ways to receive notifications if any of your software is out of date?  
- How do you know what components are from official sources? Does secure links mean the links are HTTPS?  

---

## Identification and Authentication Failures:

Confirmation of the user's identity, authentication, and session management is critical to protect against authentication-related attacks. There may be authentication weaknesses if the application:

- Permits automated attacks such as credential stuffing, where the attacker has a list of valid usernames and passwords.  
- Permits brute force or other automated attacks.  
- Permits default, weak, or well-known passwords, such as "Password1" or "admin/admin".  
- Uses weak or ineffective credential recovery and forgot-password processes, such as "knowledge-based answers," which cannot be made safe.  
- Uses plain text, encrypted, or weakly hashed passwords data stores ([A02:2021-Cryptographic Failures](https://owasp.org/Top10/A02_2021-Cryptographic_Failures/)).  
- Has missing or ineffective multi-factor authentication.  
- Exposes session identifier in the URL.  
- Reuse session identifier after successful login.  
- Does not correctly invalidate Session IDs. User sessions or authentication tokens (mainly single sign-on (SSO) tokens) aren't properly invalidated during logout or a period of inactivity.  

### How to Prevent: 

(Finish this)

### Questions:

- Does the use of UUID help prevent Authentication failures?  
- Should passkeys be optional considering it’s the most secure way to ensure proper authentication? If not, what to do about users who do not have passkey enabled devices considering the potential downsides of other forms of authentication?  
- Is there a library that checks the user’s password against the 10,000 worst passwords list and is that necessary if you write strong enough password requirements?  

---

## Software and Data Integrity Failures:

(Finish)

---

## Security Logging and Monitoring Failures:

### Questions:

- Once you notice suspicious activity being logged to the server, what immediate steps do you take to ensure data integrity?  

---

## Server-Side Request Forgery:

### Questions:

- Is implementing a proper CORS policy effective in preventing SSRF attacks?  
- Does blocking API testing tools like Postman or cURL improve API security?  

---

# [CI/CD Pipeline](https://www.geeksforgeeks.org/devops/what-is-ci-cd/)

I see a course on pluralsight for the owasp top 10, should I buy the course?  
Ask about [CIA triad](https://cybersecuritynews.com/cia-triad-confidentiality-integrity-availability/)

---

# [Notes](https://owasp.org/www-project-top-ten/)