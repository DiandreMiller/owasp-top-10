# [OWASP Top 10 LLM](https://www.evidentlyai.com/blog/owasp-top-10-llm)

## [Prompt Injections](https://www.evidentlyai.com/llm-guide/prompt-injection-llm)

## [Prompt Injection vs Jail Breaking](https://simonwillison.net/2024/Mar/5/prompt-injection-jailbreaking/)

## Principal of Least Privilege 

The Principle of Least Privilege (PoLP) is an information security concept requiring users, processes, and systems to have only the minimum permissions necessary to perform their essential tasks, and nothing more. By restricting access, PoLP minimizes the potential harm from compromised accounts, insider threats, or unintended errors, thereby reducing the overall attack surface and improving security posture. This principle is a core component of robust security frameworks like Zero Trust and helps organizations meet compliance requirements by limiting exposure to sensitive data and resources. 

## Structed Prompting Similar to Parameterized Queries

(write up)

breakdown

Loses context, starts to breakdown


### Is this similar to siri? (research)
Action-selector pattern. The model selects from a list of pre-approved actions. It cannot create arbitrary tool calls or generate free-form commands. This eliminates the ability of injected prompts to influence execution.


Is this:

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

I don't think I've ever added output guardrails in any of my projects. How would I implement that?