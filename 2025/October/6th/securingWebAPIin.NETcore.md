How would you secure a Web API in .NET Core?

Layer	Description	Keywords to Mention
1. Authentication	Verify who the user is	JWT, OAuth2, OpenID Connect, Azure AD
2. Authorization	Verify what the user can do	Roles, Policies, [Authorize] attribute
3. Data Protection	Protect data in transit and storage	HTTPS, SSL, Encryption
4. Application Hardening	Prevent common attacks	CORS, Input Validation, Anti-forgery, Rate Limiting, Logging
🧠 Model Answer (Senior-level way)

“I secure my APIs using a combination of authentication, authorization, encryption, and hardening techniques.”

1️⃣ Authentication:
I typically use JWT (JSON Web Token)-based authentication in .NET Core.
The token is issued by an identity provider after successful login and is validated on each request via middleware.
In enterprise setups, I’ve also worked with OAuth2 and OpenID Connect through Azure AD for single sign-on.

2️⃣ Authorization:
I apply role- and policy-based authorization using [Authorize(Roles="Admin")] or custom policies.
This ensures granular control over who can access which endpoints.

3️⃣ Data Protection:
All communications are secured via HTTPS. Sensitive data like passwords or connection strings are stored in Azure Key Vault or User Secrets during development.

4️⃣ Application Hardening:
I enable [CORS policies](url) to allow only trusted domains, implement input validation, and configure rate limiting to prevent DDoS or brute-force attacks.
I also log all requests and exceptions for audit and traceability.

(Optional closing)
“In my Maersk L3-support project, we’ve integrated security scanning and validation steps within our CI/CD pipeline to ensure APIs comply with OWASP standards.”
