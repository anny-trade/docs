# Authentication

The MCP connector uses OAuth 2.1 with PKCE for authentication. Most MCP clients handle this automatically — you just click "Connect" and sign in.

## OAuth Flow

```
Client                    MCP Server               Anny Backend
  │                          │                          │
  ├─ GET /authorize ────────►│                          │
  │                          ├─ Show login page ───────►│
  │                          │◄─ Validate credentials ──┤
  │◄─ Redirect with code ───┤                          │
  │                          │                          │
  ├─ POST /token ───────────►│                          │
  │  (code + code_verifier)  │                          │
  │◄─ access_token ──────────┤                          │
  │   + refresh_token        │                          │
```

## Endpoints

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/.well-known/oauth-authorization-server` | GET | OAuth metadata discovery (RFC 8414) |
| `/authorize` | GET | Start authorization flow |
| `/authorize/login` | POST | Submit login credentials |
| `/token` | POST | Exchange auth code for tokens |
| `/register` | POST | Dynamic client registration (RFC 7591) |
| `/revoke` | POST | Revoke an access token |

## Token Lifecycle

| Token | Lifetime | Notes |
|-------|----------|-------|
| Access token | 1 hour | Passed as `Authorization: Bearer <token>` |
| Refresh token | 30 days | Used to get new access tokens |
| Authorization code | 5 minutes | Single-use, exchanged for tokens |

## Scopes

```
read:portfolio    — Access your portfolio positions and P&L
read:analysis     — Access indicator readings and scenario analysis
ask:anny          — Chat with Anny AI assistant
```

## PKCE Requirement

All authorization requests must include PKCE parameters:

- `code_challenge` — SHA-256 hash of the code verifier (Base64url encoded)
- `code_challenge_method` — Must be `S256` (plain also supported but not recommended)
- `code_verifier` — Sent with the token exchange request

Most MCP clients generate PKCE parameters automatically.

## For Tool Developers

If you're building a custom MCP client, here's the manual flow:

```bash
# 1. Register your client (optional — localhost clients auto-accepted)
curl -X POST https://mcp.anny.trade/register \
  -H "Content-Type: application/json" \
  -d '{"client_name": "My App", "redirect_uris": ["https://myapp.com/callback"]}'

# 2. Redirect user to authorize
# https://mcp.anny.trade/authorize?
#   response_type=code&
#   client_id=<client_id>&
#   redirect_uri=<redirect_uri>&
#   code_challenge=<challenge>&
#   code_challenge_method=S256

# 3. Exchange code for tokens
curl -X POST https://mcp.anny.trade/token \
  -H "Content-Type: application/json" \
  -d '{
    "grant_type": "authorization_code",
    "code": "<auth_code>",
    "code_verifier": "<verifier>",
    "client_id": "<client_id>"
  }'

# 4. Use the access token
# Include in MCP requests as: Authorization: Bearer <access_token>
```
