# Security Policy

## Reporting a Vulnerability

Mailing Engineer (operated by **BSNS AGENCY ONLINE S.R.L.**) takes the security of our Remote MCP Server (`https://mailing-engineer.com/mcp`), OAuth 2.1 implementation, and customer data seriously.

If you discover a security issue, please report it privately to:

- **Email:** `security@mailing-engineer.com`
- **Security Overview & SLA:** [https://mailing-engineer.com/security](https://mailing-engineer.com/security)
- **Abuse / Deliverability Incidents:** `abuse@mailing-engineer.com`

Please include reproduction steps, affected endpoint or tool name, and impact assessment. We acknowledge security reports within 24 hours.

## Remote MCP Authentication Architecture

- **Protocol:** OAuth 2.1 Authorization Code Flow with mandatory PKCE (`S256`).
- **Audience Binding:** RFC 8707 `resource` indicator strictly bound to `https://mailing-engineer.com/mcp`.
- **Origin & Multi-Tenant Isolation:** Strict `Origin` validation and per-tenant workspace isolation enforced on every JSON-RPC call.
- **Revocation:** Users can revoke active OAuth tokens immediately from [https://portal.mailing-engineer.com](https://portal.mailing-engineer.com).
