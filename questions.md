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


**Asked**

- If credential recovery that includes “questions and answers” is prohibited by NIST 800-63b, the OWASP ASVS and the OWASP top 10, why do so many applications use that as a valid recovery method?

- What's the difference between a System prompt leakage and an Indirect Prompt injection?

- What is the relationship to embedding and LLMs?

## Important:

**Asked**
- Is this similar to siri? 
Action-selector pattern. The model selects from a list of pre-approved actions. It cannot create arbitrary tool calls or generate free-form commands. This eliminates the ability of injected prompts to influence execution.


**Asked**

- Is this:

Input guardrails try to stop known prompt injection patterns before they reach the model. This can include:

Keyword and phrase detection (e.g., "ignore previous instructions").
Regex-based rules for known jailbreak formats, trigger words (e.g. competitor names).
Semantic similarity to known attacks.
Structural flags (e.g., very long or complex user messages).
Prompt intent detection (user inputs that resemble instructions).
When suspicious input is detected, the system can:

Block it entirely.
Redirect to a safer path (e.g., a fallback message or human escalation).
Rewrite the input to neutralize risky elements.

 similar to blocking api testing tools?

 ```
 app.use((request, response, next) => {
    const userAgent = request.headers['user-agent'];
    
    const blockedAgents = [
        'Postman', 'Insomnia', 'Paw', 'Swagger', 'curl', 'HTTPie', 
        'Apigee', 'Rest-Assured', 'JMeter', 'Karate DSL', 'Tavern', 'Hoppscotch', 
        'Newman', 'Assertible', 'TestMace', 'Beeceptor', 'API Fortress', 'Runscope', 
        'Wget', 'Arthas Tunnel', 'Bat', 'Hurl', 'Restish', 'Axios Mock Adapter', 
        'fetch-mock', 'Mocha', 'Cypress', 'Nightwatch.js', 'PyRestTest', 'Locust', 
        'pytest-httpx', 'HTTPretty', 'WireMock', 'Spock Framework', 'TestNG', 
        'VCR', 'Faraday', 'RSpec API Documentation', 'Guzzle', 'Laravel Dusk', 
        'Artillery', 'Gatling', 'Vegeta', 'Boom', 'PostgREST', 'JSON Server', 
        'MSW (Mock Service Worker)', 'Prism', 'OWASP ZAP', 'Burp Suite', 
        'Nikto', 'Mitmproxy', 'SmartBear ReadyAPI', 'BlazeMeter', 'Testim', 
        'Thunder Client', 'REST Client', 'Postwoman (Hoppscotch)', 'Tyk Test Framework', 
        'FastAPI TestClient', 'Grpcurl', 'RoboHydra', 'Apache HttpClient', 
        'Zerocode', 'Step CI', 'Spectral', 'Fortio', 'Apiritif', 'SoapUI', 
        'GraphiQL', 'Altair', 'Mockoon', 'Swagger UI', 'Chakram', 'Supertest', 
        'K6', 'WireMock', 'API Tester', 'Boomi', 'LoopBack Explorer', 'API Blueprint', 
        'CloudTest', 'SlashDB', 'LambdaTest', 'Dredd', 'API Gateway Testing Console', 
        'RestCase', 'Nock', 'MockServer', 'Mirage JS', 'Traffic Parrot', 'Hoverfly', 
        'MockLab', 'Interceptor', 'Scriptrunner', 'Kong', 'LocalStack', 'Acunetix', 
        'Nessus', 'NetSparker', 'Qualys', 'Burp API Scanner', 'SecApps', 'SSLyze', 
        'Intruder.io', 'API Security.io', 'Firebug Lite', 'API Buddy', 'Fiddler Everywhere', 
        'Boomerang', 'Advanced REST Client', 'ReqBin', 'ReqRes', 'HTTP Debugger', 
        'Charles Proxy', 'BrowserStack API Testing', 'Nightfall AI', 'HTTP Toolkit', 
        'Smocker', 'HTTP Prompt', 'FakeIt', 'JQ', 'HTTPRequester', 'Netcat', 
        'TLSScan', 'SockJS', 'NanoHTTPD', 'Feign', 'OkHttp', 'Unirest', 'Retrofit', 
        'Spring WebTestClient', 'Requests-Mock', 'WebTest', 'Testify', 
        'Falcon Testing Library', 'Tornado HTTPClient', 'FrisbyJS', 'PactJS', 
        'Puppeteer', 'Jasmine-ajax', 'Jest Mock Fetch', 'Zend HTTP Client', 
        'PHPUnit REST API Testing', 'PHPSpec', 'Cucumber', 'Typhoeus', 'Resty', 
        'Golang HTTP Mock', 'Loader.io', 'Tsung', 'NeoLoad', 'LoadNinja', 'WebLOAD', 
        'OpenSTA', 'Locust', 'Siege', 'Hey', 'Taurus', 'Postman Monitors', 
        'Uptrends', 'StatusCake', 'Pingdom', 'Datadog API Monitoring', 'Uptime Robot', 
        'Moesif', 'Dotcom-Monitor', 'Splunk Synthetic Monitoring', 'Sentry', 
        'Parasoft SOAtest', 'Telerik Test Studio', 'Protractor', 'Katalon Studio', 
        'TestProject', 'API-Checker', 'ScriptRunner for APIs', 'Mocky.io', 
        'Faker.js', 'Pyngrok', 'Clouditor', 'Firecamp', 'FoxyProxy', 'Grizzly HTTP', 
        'HTTPBin', 'Requestly', 'WireMock Cloud', 'SwaggerHub', 'Gravitee', 
        'WcfStorm', 'API Umbrella', 'Redocly', 'API Science', 'Dart HTTP Client', 
        'Hitch', 'OpenAPI Diff', 'Swagger Validator', 'RoboHydra Server', 'OverOps', 
        'StormForge', 'LoadView', 'Tyk Dashboard', 'Kubernetes Kube-API', 
        'AquaSec Kube-Bench', 'AppDynamics API Monitoring', 'Keycloak REST Client', 
        'Dredd CLI', 'Tyk Gateway', 'Grizzly Load Tester', 'Restlet Client', 
        'Fiddler Classic', 'K6 Cloud', 'Parrot', 'Swagger Codegen', 'APIsec', 
        'Zanshin API Scanner', 'Imperva API Security', 'Salt Security', 
        'Traceable AI', 'Sauce Labs API Testing', 'SmartMock.io', 'Snapshooter', 
        'Reflect', 'Vialer.js', 'NGINX Amplify', 'GraphQL Inspector'
    ];
    
    
    if (blockedAgents.some(agent => userAgent && userAgent.includes(agent))) {
        return response.status(403).send('Requests from API testing tools are not allowed.');
    }
    
    next();
});

```
