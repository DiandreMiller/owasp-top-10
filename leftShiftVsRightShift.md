# Shift Left vs Shift Right

### The four basic types of shift left testing are the following:###

Traditional shift left testing. The traditional approach focuses on unit and integration testing, typically involving APIs and cross-browser compatibility. This approach focuses more on unit testing small pieces of code to deliver information early and often rather than more systems-level operational and acceptance testing.
Incremental shift left testing. This is a popular approach for teams migrating from a waterfall development approach to one that breaks complex projects into smaller pieces. In this scenario, teams conduct systems-level operational and acceptance testing on a smaller, more incremental scale. Incremental testing is popular for validating large and complex systems.
Agile/DevOps testing. This is a series of short, continuous sprints during the development stage. This approach does not intend to address operational performance but rather validate adherence to basic requirements architecture.
Model-based shift left. Model-based testing aims to reduce errors introduced during the requirements definition, architecture, and design phases. It tests for executable requirements, architecture, and design. The advantage of model-based testing is that it can begin almost immediately instead of after completing all other test cycles.

## Static Application Security Testing (STAS)

 SAST tools analyze the source code without executing it. They identify potential security issues, coding standards violations, and vulnerabilities. Linters (e.g., ESLint for JavaScript, pylint for Python) fall into this category. 

## Dynamic Application Security Testing (DAST)

DAST tools test the application during runtime by simulating attacks. They identify vulnerabilities that can be exploited by attackers. Examples include OWASP ZAP and Burp Suite. 

Questions:

- Are static languages such as typescript similar to SAST tools?

[Notes](https://www.dynatrace.com/news/blog/what-is-shift-left-and-what-is-shift-right/)
