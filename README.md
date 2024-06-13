# Apigee API Management | Google Cloud

## Why Apigee Load Balancer and Cloud Armor alone are not enough to protect API?

**GCP Load Balancers:** Distribute incoming traffic across multiple API instances for scalability and availability. They provide basic network-level (Layer 3/4) security.

**Cloud Armor:** A Web Application Firewall (WAF) that protects against Layer 7 attacks like DDoS, SQL injection, cross-site scripting (XSS). It integrates with GCP Load Balancers.

**The Gaps: Why It's Not Enough**

- **API-Specific Threats**: Load Balancers and Cloud Armor are not specialized in understanding the nuances of API vulnerabilities.  Attackers can exploit the logic and structure of APIs (e.g., broken object-level authorization, mass assignment) that general network-level protection may miss.
- **Data/Model Security**: API Endpoints may expose sensitive data or models. Cloud Armor won't protect against:
  - Data exfiltration at the API level
  - Unauthorized access to model inference endpoints
  - Attacks on model integrity (model poisoning), models can be manipulated by sending incorrect or malicious data to the training data or learning process.
- **Business Logic Flaws**: Load Balancers and Cloud Armor don't understand your application's business logic. Attackers might manipulate API calls in ways that seem legitimate but abuse the underlying business processes.

> **Apigee is the API Management complements GCP Load Balancer and Cloud Armor, adding essential layers.**

## The security points: 

- Access
	- OAuth 2.0
	- IP address access control
- Applications
	- API keys
	- OAuth 2.0
	- TLS
- Developers and partners
	- SSO
	- RBAC
- APIs
	- OAuth 2.0
	- OpenID Connect
	- Quotas
	- Spike arrest
	- Threat protection
- API team
	- IAM RBAC
	- Federated logic
	- Data masking
	- Audit logs
- Backend
	- Private networking
	- Mutual TLS
	- IP address access control

## Apigee default policies to secure your APIs

|	Policy type	|	Policy name	|	Security use case	|
|-------|-------|-------|
|	Traffic management	|	SpikeArrest policy	|	Applies rate limiting to the number of requests sent to the backend.	|
|	Traffic management	|	Quota policy	|	Helps your organization to enforce quotas (the number of API calls made) for each consumer.	|
|	Traffic management	|	ResponseCache policy	|	Caches responses, reducing the number of requests to the backend.	|
|	Message-level protection	|	OASValidation policy	|	Validates incoming requests or response messages against an OpenAPI 3.0 Specification (JSON or YAML).	|
|	Message-level protection	|	SOAPMessageValidation policy	|	Validates XML messages against a schema of your choice. Validates SOAP messages against a WSDL and determines whether JSON and XML messages are correctly formed.	|
|	Message-level protection	|	JSONThreatProtection policy	|	Helps to mitigate the risk of content-level attacks by letting you specify limits on JSON structures like arrays and strings.	|
|	Message-level protection	|	XMLThreatProtection policy	|	Helps you to address XML vulnerabilities and mitigate the risk of attacks by evaluating message content and detecting corrupt or malformed messages before they can be parsed.	|
|	Message-level protection	|	RegularExpressionProtection policy	|	Evaluates content against predefined regular expressions and rejects it if the expression is true.	|
|	Security	|	BasicAuthentication policy	|	Base64 encodes and decodes user credentials.	|
|	Security	|	VerifyAPIKey policy	|	Enforces the verification and the validation of API keys at runtime. Only allows applications with approved API keys associated with your API products to access your APIs.	|
|	Security	|	OAuthV2 policy	|	Performs OAuth 2.0 grant type operations to generate and validate access tokens.	|
|	Security	|	JWS and JWT policies	|	Generates, verifies, and decodes JSON Web Tokens (JWT) and JSON Web Signatures (JWS).	|
|	Security	|	HMAC policy	|	Computes and verifies hash-based message authentication code (HMAC) for authentication and application-level integrity checks.	|
|	Security	|	SAMLAssertion policy	|	- Validates incoming messages that contain a digitally signed SAML assertion. - Generates SAML assertions to outbound XML requests.	|
|	Security	|	CORS policy	|	Lets you set cross-origin resource sharing (CORS) headers for APIs that are consumed by web applications.	|
