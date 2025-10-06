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
I enable [CORS policies](https://github.com/sbindgithub/dev-journal/blob/main/2025/October/6th/CORS%20Policies.md) to allow only trusted domains, implement input validation, and configure rate limiting to prevent DDoS or brute-force attacks.
I also log all requests and exceptions for audit and traceability.

(Optional closing)
“In my Maersk L3-support project, we’ve integrated security scanning and validation steps within our CI/CD pipeline to ensure APIs comply with OWASP standards.”

--

I secure Web APIs using layered controls: authentication (who), authorization (what), data protection (how it’s transported/stored), and application hardening (prevent attacks).
In practice I use JWT/OAuth2/OpenID Connect for authentication (Azure AD for enterprise SSO), role- and policy-based authorization in .NET Core, HTTPS + secrets in Azure Key Vault, and hardening like CORS, input validation, rate-limiting, logging and CI security scans. In my Maersk projects we also enforce security checks in the CI/CD pipeline to ensure OWASP best practices are met.

- Authentication: JWT tokens or Azure AD (OAuth2 / OpenID Connect).

- Authorization: Role-based and policy-based ([Authorize], IAuthorizationRequirement).

- Transport & secrets: HTTPS, HSTS, Azure Key Vault / User Secrets for dev.

- Hardening: CORS allowlist, input validation, anti-forgery where relevant, rate limiting, secure headers.

- Operational: Centralized logging, audit trails, security scans in CI/CD.

  1) Program.cs — Configure auth, CORS, endpoints (minimal .NET 6+ style)
     
``` 
  var builder = WebApplication.CreateBuilder(args);

// ----- CORS -----
builder.Services.AddCors(options =>
{
    options.AddPolicy("AllowOnlyMyFrontend", policy =>
    {
        policy.WithOrigins("https://mycompany-portal.com")
              .AllowAnyHeader()
              .AllowAnyMethod();
    });
});

// ----- Authentication: JWT -----
builder.Services.AddAuthentication(options =>
{
    options.DefaultAuthenticateScheme = JwtBearerDefaults.AuthenticationScheme;
    options.DefaultChallengeScheme = JwtBearerDefaults.AuthenticationScheme;
})
.AddJwtBearer(options =>
{
    options.TokenValidationParameters = new TokenValidationParameters
    {
        ValidateIssuer = true,
        ValidateAudience = true,
        ValidateLifetime = true,
        ValidateIssuerSigningKey = true,
        ValidIssuer = builder.Configuration["Jwt:Issuer"],
        ValidAudience = builder.Configuration["Jwt:Audience"],
        IssuerSigningKey = new SymmetricSecurityKey(
            Encoding.UTF8.GetBytes(builder.Configuration["Jwt:Key"]))
    };
});

// ----- Authorization: role & policy example -----
builder.Services.AddAuthorization(options =>
{
    options.AddPolicy("RequireAdmin", policy =>
        policy.RequireRole("Admin"));
    options.AddPolicy("OrderManager", policy =>
        policy.RequireClaim("department", "orders"));
});

builder.Services.AddControllers();

var app = builder.Build();

app.UseHttpsRedirection();
app.UseCors("AllowOnlyMyFrontend");
app.UseAuthentication();
app.UseAuthorization();

app.MapControllers();

app.Run();
```
Simple JWT token generation (server-side token issuer)

```
public class TokenService
{
    private readonly IConfiguration _cfg;
    public TokenService(IConfiguration cfg) => _cfg = cfg;

    public string CreateToken(string userId, IEnumerable<string> roles, IDictionary<string,string> claims = null)
    {
        var claimsList = new List<Claim>
        {
            new Claim(JwtRegisteredClaimNames.Sub, userId),
            new Claim(JwtRegisteredClaimNames.Jti, Guid.NewGuid().ToString())
        };

        foreach (var r in roles) claimsList.Add(new Claim(ClaimTypes.Role, r));
        if (claims != null)
            foreach (var kv in claims)
                claimsList.Add(new Claim(kv.Key, kv.Value));

        var key = new SymmetricSecurityKey(Encoding.UTF8.GetBytes(_cfg["Jwt:Key"]));
        var creds = new SigningCredentials(key, SecurityAlgorithms.HmacSha256);

        var token = new JwtSecurityToken(
            issuer: _cfg["Jwt:Issuer"],
            audience: _cfg["Jwt:Audience"],
            claims: claimsList,
            expires: DateTime.UtcNow.AddHours(1),
            signingCredentials: creds);

        return new JwtSecurityTokenHandler().WriteToken(token);
    }
}```
3) Controller usage (authorization attributes)
```
[ApiController]
[Route("api/[controller]")]
public class OrdersController : ControllerBase
{
    // Any authenticated user
    [HttpGet]
    [Authorize] 
    public IActionResult GetOrders() { ... }

    // Only users with Admin role
    [HttpDelete("{id}")]
    [Authorize(Roles = "Admin")]
    public IActionResult DeleteOrder(int id) { ... }

    // Policy-based
    [HttpPost("assign")]
    [Authorize(Policy = "OrderManager")]
    public IActionResult AssignOrder([FromBody] AssignDto dto) { ... }
}

```
