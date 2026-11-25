# Mailing Engineer — Official Remote MCP Server

**60-Tool Model Context Protocol (MCP) Server for E-Commerce Email Marketing, Deliverability & Store Automations.**

Connect **Claude**, **ChatGPT**, **Cursor**, **VS Code**, **Windsurf**, or **Google Antigravity** directly to your [Mailing Engineer](https://mailing-engineer.com) workspace over **Streamable HTTP** with **OAuth 2.1 + PKCE (`S256`)** — zero local server setup, zero API keys pasted into chat, and strict per-tenant isolation.

- **Remote MCP Endpoint:** `https://mailing-engineer.com/mcp`
- **Transport:** Streamable HTTP (JSON-RPC 2.0)
- **Authentication:** OAuth 2.1 with mandatory PKCE (`S256`), RFC 8707 Resource Indicators, RFC 9728 Protected Resource Metadata, RFC 8414 Authorization Server Metadata, and Dynamic Client Registration (`/oauth/register`)
- **Documentation:** [https://mailing-engineer.com/mcp/docs](https://mailing-engineer.com/mcp/docs)
- **Create Free Account (10,000 Bonus Emails):** [https://portal.mailing-engineer.com/register](https://portal.mailing-engineer.com/register)
- **EU Cloud & GDPR:** Hosted in the European Union (Germany — Frankfurt & Nuremberg), powered by AWS (`eu-central-1`), operated by **BSNS AGENCY ONLINE S.R.L.**

---

## Why Use Mailing Engineer via MCP?

Instead of switching tabs between your store admin, DNS panel, and email dashboard, your AI assistant can manage your entire email retention stack safely through typed, scope-checked tools:

- **Audience & Hygiene (15 tools):** Query subscribers, run MX & Global Bounce hygiene checks, segment by ISP (Gmail, Yahoo, Outlook, Corporate), migrate lists from Klaviyo / Mailchimp / Brevo, and process GDPR unsubscribes or erasures.
- **E-Commerce & Revenue Attribution (10 tools):** Inspect synced Shopify, WooCommerce, Gomag, MerchantPro, PrestaShop, and OpenCart products, orders, attributed revenue, active clickers, and promotional coupons.
- **Deliverability & DNS Engineering (9 tools):** Audit SPF, 2048-bit DKIM, DMARC, Custom MAIL FROM, and BIMI live; provision Amazon SES domains; auto-configure Cloudflare DNS; and run Gmail/Yahoo complaint diagnostics.
- **Campaign Operations (8 tools):** Draft, schedule, update, test-send, pause (with automatic credit refund), resume, and inspect campaign performance reports.
- **AI Studio & EU Localization (6 tools):** Generate responsive 600px newsletters directly from live store products, test spam triggers, suggest subject lines, and localize campaigns into EN, DE, FR, IT, ES, PL, or HU.
- **Analytics, Transactional, Automations & Loyalty (11 tools):** Pull executive ROI reports, send 1-to-1 transactional emails, create abandoned cart / welcome / win-back automation drafts, and inspect VIP loyalty segments.

---

## Quick Setup (Zero Local Install)

### 1. Claude (Claude.ai Web & Claude Desktop)
1. Open **Settings -> Connectors** (or **Integrations**) in Claude.
2. Click **Add custom connector**.
3. Enter:
   - **Name:** `Mailing Engineer`
   - **Remote MCP Server URL:** `https://mailing-engineer.com/mcp`
4. Click **Connect** and approve access via the Mailing Engineer OAuth 2.1 consent screen.

### 2. ChatGPT (Connectors / Developer Mode)
1. Open **Settings -> Connectors -> Create**.
2. Set **MCP Server URL** to `https://mailing-engineer.com/mcp` with **OAuth** authentication.
3. Authorize your Mailing Engineer account and start prompting.

### 3. Cursor (`~/.cursor/mcp.json` or `.cursor/mcp.json`)
```json
{
  "mcpServers": {
    "mailing-engineer": {
      "url": "https://mailing-engineer.com/mcp"
    }
  }
}
```

### 4. VS Code (`.vscode/mcp.json`)
```json
{
  "servers": {
    "mailing-engineer": {
      "type": "http",
      "url": "https://mailing-engineer.com/mcp"
    }
  }
}
```

### 5. Windsurf / Generic Streamable HTTP Clients
Point your MCP client's remote HTTP server configuration to:
```text
https://mailing-engineer.com/mcp
```
OAuth 2.1 discovery endpoints are published automatically at:
- `https://mailing-engineer.com/.well-known/oauth-protected-resource`
- `https://mailing-engineer.com/.well-known/oauth-authorization-server`

---

## Example Prompts

- *"Verify my Mailing Engineer connection and summarize my last 30 days of email revenue and deliverability health."*
- *"Check all 9 DNS records (SPF, 2048-bit DKIM, DMARC, Custom MAIL FROM, BIMI) for my sending domain and tell me if anything is misaligned."*
- *"Segment my audience by ISP (Gmail, Yahoo, Outlook) and analyze complaint risk before our Black Friday send."*
- *"Pull our top discounted products from the store, generate a responsive newsletter draft, and send a test email to my inbox."*
- *"Create an abandoned cart automation flow draft and attach coupon code `WELCOME10`."*

---

## Core Tool Reference

Access levels: `read` (read-only query), `write` (non-destructive state change or draft), `destructive` (sends email, modifies/deletes subscriber data, or updates live schedules).

### 1. Audience & List Hygiene (15 tools)
| Tool | Access | Summary |
| :--- | :--- | :--- |
| `list_contacts` | `read` | List or count contacts matching search, segment, or consent filters. |
| `get_contact_details` | `read` | Retrieve full profile, segment membership, and subscription status for a subscriber. |
| `create_contact` | `write` | Add a subscriber with automatic Anti-Bounce and Global DNC verification. |
| `update_contact` | `destructive` | Update an existing subscriber name, segment, or subscription status. |
| `unsubscribe_contact` | `destructive` | Immediately mark a subscriber as opted out across future campaigns. |
| `delete_contact` | `destructive` | Permanently delete a contact from the workspace database (GDPR erasure). |
| `import_contacts` | `destructive` | Bulk import subscribers into a segment with MX and Global Bounce filtering. |
| `validate_email_hygiene` | `read` | Validate email syntax, disposable domains, MX records, and global bounce history. |
| `list_segments` | `read` | List all audience segments with total and active subscriber counts. |
| `create_segment` | `write` | Automatically segment contacts by ISP (Gmail, Yahoo, Outlook, Corporate) or batches. |
| `get_audience_evolution` | `read` | Track subscriber growth, new additions, and unsubscribes over a lookback window. |
| `get_audience_breakdown` | `read` | Break down the subscriber base by ISP provider and consent status. |
| `analyze_audience` | `read` | Perform a strategic audience health analysis and list hygiene review. |
| `get_audience_options` | `read` | Return available segments, consent statuses, and ISP groups for filtering. |
| `migrate_contacts_from_esp` | `write` | Import subscribers from Klaviyo, Mailchimp, Brevo, or CSV exports with automatic hygiene checks. |

### 2. E-Commerce & Attribution (10 tools)
| Tool | Access | Summary |
| :--- | :--- | :--- |
| `list_products` | `read` | List products from the connected store or extract live catalog items from the store URL. |
| `get_product_details` | `read` | Inspect pricing, discount percentage, image proxy URL, and metadata for a product. |
| `get_product_options` | `read` | Return available product collections and brand metadata from the connected store. |
| `list_orders` | `read` | List synced e-commerce orders and attributed campaign revenue. |
| `get_order_trend` | `read` | Analyze click-to-order conversion trends and attributed campaign performance over time. |
| `list_coupons` | `read` | List active discount codes used across campaigns and automations. |
| `save_coupon` | `write` | Register a promotional discount code for newsletters and abandoned cart flows. |
| `get_ecommerce_stats` | `read` | Calculate attributed e-commerce revenue, ROI multiple, conversion funnel, and cost per email. |
| `get_realtime_visitors` | `read` | Inspect real-time email opens, active link clickers, and throughput over the last 60 minutes. |
| `sync_shopify_customers` | `read` | Inspect connected Shopify / WooCommerce store status, synced customer count, and feed health. |

### 3. Domain, DNS & Deliverability (9 tools)
| Tool | Access | Summary |
| :--- | :--- | :--- |
| `verify_connection` | `read` | Verify MCP OAuth authentication and return the connected workspace profile. |
| `list_domains` | `read` | List configured sending domains, default sender addresses, and tracking subdomains. |
| `get_sending_domain` | `read` | Inspect all 9 DNS records (3x 2048-bit DKIM, `nl.` tracking subdomain, SPF, DMARC, bounce MX/TXT, BIMI). |
| `validate_domain` | `write` | Provision a domain in Amazon SES (2048-bit Easy DKIM + Custom MAIL FROM) and verify live DNS. |
| `audit_store_domain_live` | `read` | Run a live technical and deliverability DNS audit on an e-commerce domain. |
| `auto_configure_cloudflare_dns` | `write` | Automatically create and align DKIM, SPF, DMARC, bounce, BIMI, and tracking records in Cloudflare. |
| `yahoo_gmail_complaint_doctor` | `read` | Analyze Gmail/Yahoo audience share, unsubscribe visibility, and complaint risk (< 0.1% SES threshold). |
| `get_costs` | `read` | Check available email credits, wallet balance, bonus status, and recent billing transactions. |
| `get_integration_health` | `read` | Check overall workspace health: SES tier status, DNS alignment, list hygiene, and store sync. |

### 4. Campaigns (8 tools)
| Tool | Access | Summary |
| :--- | :--- | :--- |
| `list_campaigns` | `read` | List recent, scheduled, or sent campaigns with delivery, open, and click counts. |
| `get_campaign_details` | `read` | Retrieve full metadata, sender configuration, target segment, and HTML preview snippet. |
| `get_campaign_report` | `read` | Retrieve delivery, open rate, CTR, bounce rate, and unsubscribe metrics for a campaign. |
| `create_campaign` | `destructive` | Create and dispatch or schedule an email campaign to a target segment. |
| `update_campaign` | `destructive` | Update the name, subject, schedule, or HTML content of a scheduled campaign before sending. |
| `send_test_campaign` | `destructive` | Send a live DNS alignment or HTML test email to a specified inbox. |
| `pause_campaign` | `write` | Pause an active campaign or cancel a scheduled campaign and refund unused credits. |
| `resume_campaign` | `destructive` | Trigger immediate sending for a scheduled or paused campaign. |

### 5. AI Studio & Localization (6 tools)
| Tool | Access | Summary |
| :--- | :--- | :--- |
| `generate_ai_newsletter_from_store` | `write` | Extract live store products (images, prices, discounts) and generate a responsive HTML newsletter. |
| `suggest_ai_subject_lines` | `read` | Generate 5 high-open-rate subject lines and preheaders tailored to an e-commerce offer. |
| `list_email_templates` | `read` | List pre-built responsive e-commerce email templates available in Mailing Engineer Studio. |
| `check_spam_score_and_deliverability` | `read` | Evaluate subject and HTML body for spam triggers, image-to-text ratio, and unsubscribe compliance. |
| `rewrite_email_copy_ai` | `read` | Rewrite raw promotional notes into conversion-focused Romanian or English e-commerce copy. |
| `translate_campaign_for_eu_markets` | `write` | Translate and localize a newsletter into EN, DE, FR, IT, ES, PL, or HU with currency conversion. |

### 6. Reports & Analytics (4 tools)
| Tool | Access | Summary |
| :--- | :--- | :--- |
| `get_report` | `read` | Complete account overview: total contacts, campaigns, sent volume, open/click rates, and deliverability score. |
| `get_audience_history` | `read` | Historical contact growth across segments over time. |
| `list_analytics_reports` | `read` | List available performance, bounce/complaint safety, and ROI reports. |
| `get_analytics_report` | `read` | Compare top-performing campaigns by open rate, CTR, and segment responsiveness. |

### 7. Transactional Email & Sender Profile (4 tools)
| Tool | Access | Summary |
| :--- | :--- | :--- |
| `send_transactional_email` | `destructive` | Send an immediate 1-to-1 transactional email via Amazon SES from your verified domain. |
| `get_transactional_credits` | `read` | Return exact available credits, used credits, and wallet balance. |
| `list_transactional_messages` | `read` | List credit top-ups, bonus grants, and recent sending activity. |
| `update_sender_profile` | `write` | Update company name, default From name/email, or Reply-To address. |

### 8. Automations & Loyalty (3 tools)
| Tool | Access | Summary |
| :--- | :--- | :--- |
| `list_automations` | `read` | List configured e-commerce automation flows (Welcome, Abandoned Cart, Win-Back, Post-Purchase). |
| `create_automation_flow` | `write` | Create a draft automated email flow from a proven e-commerce template. |
| `get_loyalty_program` | `read` | Inspect VIP / Champions subscriber counts and loyalty tier distribution. |

---

## Security & Compliance

- **OAuth 2.1 + PKCE (`S256`):** Authorization codes require SHA-256 PKCE verification and strict RFC 8707 `resource` audience binding (`https://mailing-engineer.com/mcp`).
- **Scope & Tenant Isolation:** Every request executes strictly within the authenticated tenant scope (`read` vs. `write`), with token revocation support in the Mailing Engineer Client Portal.
- **EU Data Residency & GDPR:** Core infrastructure and EU subscriber storage are hosted in Germany (EU) under **BSNS AGENCY ONLINE S.R.L.** (CUI `49810182` · VAT `RO55688951`).
- **Vulnerability Disclosure:** See [SECURITY.md](./SECURITY.md) or contact `security@mailing-engineer.com`.

---

## Official Links

- Website: [https://mailing-engineer.com](https://mailing-engineer.com)
- MCP Interactive Documentation: [https://mailing-engineer.com/mcp/docs](https://mailing-engineer.com/mcp/docs)
- Client Portal: [https://portal.mailing-engineer.com](https://portal.mailing-engineer.com)
- Agency Partner Portal: [https://agency.mailing-engineer.com](https://agency.mailing-engineer.com)
- Privacy Policy (GDPR): [https://mailing-engineer.com/privacy](https://mailing-engineer.com/privacy)
- Terms of Service: [https://mailing-engineer.com/terms](https://mailing-engineer.com/terms)
- Security & SLA: [https://mailing-engineer.com/security](https://mailing-engineer.com/security)
