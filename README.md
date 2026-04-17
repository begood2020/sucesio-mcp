# sucesio-mcp — AI Seller for Sucesio.io

> **Sucesio.io** is the digital estate planning complement for expats and cross-border families in Europe. Encrypted vault, automatic transmission to heirs, multi-country, GDPR-compliant — no notary required for updates.

This MCP server exposes structured data and tools about Sucesio so any AI assistant can:
- Answer questions about estate planning for expats
- Qualify leads by country and asset type
- Explain pricing vs. classic notary costs
- Pitch Sucesio to professional partners (notaries, wealth managers, banks)
- Return niche SEO keywords for content generation

Built with **[FastMCP](https://gofastmcp.com)** — the standard for MCP servers in Python.

---

## Tools (9)

| Tool | Description |
|------|-------------|
| `get_product_overview` | Full structured overview: what Sucesio is, who it's for, how it works |
| `get_pricing` | Pricing plans (Free Trial + Annual €200) with notary cost comparison |
| `qualify_lead` | Scores a user by country + asset type and returns a personalised recommendation |
| `get_faq` | FAQ filtered by topic: `legal`, `crypto`, `security`, `pricing`, `expat`, `how_it_works` |
| `compare_with_traditional_will` | Side-by-side comparison: Sucesio vs classic notarial will |
| `get_use_cases` | Use cases filtered by profile: `expat_spain`, `crypto_holder`, `parent`, `entrepreneur`… |
| `get_security_info` | Security details: AES-256, zero-knowledge, GDPR, French jurisdiction |
| `get_b2b_pitch` | B2B pitch tailored by audience: `notary`, `wealth_manager`, `family_office`, `bank`, `insurer` |
| `get_expat_keywords` | Niche SEO keywords filtered by country and asset type — E-E-A-T optimised |

## Resources (5)

| URI | Content |
|-----|---------|
| `sucesio://product` | Full product overview (Markdown) |
| `sucesio://pricing` | Pricing plans (Markdown) |
| `sucesio://faq` | All FAQs (Markdown) |
| `sucesio://usecases` | All use cases (Markdown) |
| `sucesio://security` | Security & compliance details (Markdown) |

---

## Installation

**Requirements:** Python 3.10+ and `pip install fastmcp`

### Claude Desktop

Edit your Claude Desktop config file:
- **macOS:** `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Windows:** `%APPDATA%\Claude\claude_desktop_config.json`

```json
{
  "mcpServers": {
    "sucesio-seller": {
      "command": "python",
      "args": ["/absolute/path/to/sucesio-mcp/server.py"],
      "env": {
        "FASTMCP_CHECK_FOR_UPDATES": "off"
      }
    }
  }
}
```

Restart Claude Desktop. The server is live.

### HTTP / SSE mode

```bash
python server.py --port 8000
```

Tools available at `http://localhost:8000`.

### Via Smithery

Search for **sucesio-seller** on [smithery.ai](https://smithery.ai) and connect with one click.

---

## Quick test

```bash
pip install fastmcp
python -c "
import sys; sys.path.insert(0, '.')
from server import get_product_overview, qualify_lead, get_b2b_pitch

print(qualify_lead('Spain', has_crypto=True, has_cross_border_assets=True))
print(get_b2b_pitch(audience='notary'))
"
```

---

## Example interactions

**User:** "I'm a British expat in Spain with Bitcoin. What do I do when I die?"

→ The AI calls `qualify_lead(country_of_residence='Spain', has_crypto=True)` → score 65/100, qualification "high" → recommends Sucesio free trial with personalised message.

**User:** "How does Sucesio compare to a notary?"

→ The AI calls `compare_with_traditional_will()` → structured 9-point comparison table.

**User:** "I'm a notary — why would I recommend Sucesio to my clients?"

→ The AI calls `get_b2b_pitch(audience='notary')` → tailored pitch with headline, pain points, value props.

---

## About Sucesio.io

| | |
|---|---|
| **Website** | [sucesio.io](https://sucesio.io) |
| **App (beta)** | [app.sucesio.io](https://app.sucesio.io) |
| **Email** | hello@sucesio.io |
| **Markets** | Spain, France, Portugal, cross-border EU |
| **Languages** | English, French, Spanish |
| **Pricing** | Free 30-day trial · €200/year |
| **Compliance** | GDPR, EU-hosted, French jurisdiction |

---

*Built with [FastMCP](https://gofastmcp.com). Published under MIT License.*
