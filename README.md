# Ads Editor MCP: Meta Ads MCP and Google Ads MCP server

[![Ads Editor MCP connector](https://glama.ai/mcp/connectors/br.com.adseditor/mcp/badges/score.svg)](https://glama.ai/mcp/connectors/br.com.adseditor/mcp)

**Ads Editor MCP** is a remote [Model Context Protocol](https://modelcontextprotocol.io) server that connects **Meta Ads (Facebook and Instagram)** and **Google Ads** to AI assistants: **Claude, ChatGPT, Cursor, Claude Code, Codex, Grok, Gemini CLI, Windsurf and VS Code**. It has **354 tools** that read *and* change ad accounts in plain language: performance reports, cross-account campaign cloning, bulk ad uploads, audiences, budgets, negative keywords, automated rules, alerts and ad account balances.

| | |
|---|---|
| What it is | Remote MCP server of [Ads Editor](https://adseditor.app), a web platform for media buyers and agencies that run many Meta Ads and Google Ads accounts |
| Server URL (English accounts) | `https://mcp.adseditor.app/mcp` |
| Server URL (Portuguese accounts) | `https://mcp.adseditor.com.br/mcp` |
| Transport | Streamable HTTP (remote, nothing to install) |
| Authentication | OAuth 2.1 (recommended) or a personal bearer token |
| Tools | 354 in the server registry, counted on 25 Nov 2026 ([breakdown below](#the-354-tools-by-category)) |
| Ad platforms | Meta Ads and Google Ads, in one server |
| Official MCP Registry | [`br.com.adseditor/mcp`](https://registry.modelcontextprotocol.io/v0/servers?search=br.com.adseditor) |
| Tool catalog with every tool name | [adseditor.app/mcp](https://adseditor.app/mcp) (English) · [adseditor.com.br/mcp](https://adseditor.com.br/mcp) (Português) |
| Price | MCP is included from the Pro plan (US$39/month or R$197/month), 7-day free trial |

Ads Editor is an independent product. It is **not** Google Ads Editor and not a Meta or Google product; it connects through the official Meta Marketing API and Google Ads API.

## Contents

- [What it does](#what-it-does)
- [The 354 tools by category](#the-354-tools-by-category)
- [Connect your AI client](#connect-your-ai-client) (Claude, ChatGPT, Cursor, Claude Code and others)
- [Example prompts](#example-prompts)
- [Security and permissions](#security-and-permissions)
- [Plans and limits](#plans-and-limits)
- [FAQ](#faq)
- [Links](#links)
- [Português](#português)

## What it does

You ask, the assistant picks the Ads Editor tools it needs, and you get the numbers back or the change happens in the ad account. One request can cover several accounts and both platforms.

- **Reporting across accounts:** spend, results, CPA and ROAS by campaign, ad set or ad, with breakdowns by age, gender, placement, device and day.
- **Cross-account cloning:** copy a Meta campaign to another ad account and swap the Facebook Page, Instagram account, pixel and WhatsApp number in the same step. Google Ads campaigns can be duplicated to the same or another account.
- **Bulk work:** upload creatives through the same publishing queue the web editor uses, create the same audiences in several accounts, pause or activate many objects, edit UTMs, targeting, budgets and end dates in one call.
- **Google Ads:** Search, Performance Max and Shopping campaigns, ad groups and responsive search ads, keywords, search terms, shared negative keyword lists, assets (sitelinks, callouts, snippets), audiences, schedules, device bids, conversions (including offline), labels and experiments.
- **Platform guardrails from chat:** automated rules, metric alerts, balance monitor and spend alerts, shareable client reports and sales attributed by UTM from 33 checkout and e-commerce platforms.

For comparison: Google's own [Google Ads MCP server](https://github.com/googleads/google-ads-mcp) exposes three read-only tools (`search`, `get_resource_metadata`, `list_accessible_customers`, checked on 17 Oct 2026). Ads Editor MCP covers Meta Ads and Google Ads together and can write to the accounts, within each user's permissions.

## The 354 tools by category

Counted by loading the server's tool registry on 25 Nov 2026. "Read" tools only query data; "action" tools change something. What each user sees depends on the plan and on team permissions; 3 of the 354 are internal tools for the Ads Editor team and are not available to customers. The [public catalog](https://adseditor.app/mcp) lists every tool name.

### Meta Ads (Facebook and Instagram): 122 tools

| Category | Tools | What the assistant can do |
|---|---:|---|
| Accounts and insights | 15 | List and activate ad accounts, connection status, dashboards, account metrics and breakdowns, charges, account notes and the account profile the AI uses |
| Campaigns | 23 | List, inspect, create (paused), rename, pause, activate, delete, change budget (including step-by-step increases), clone within or across accounts, switch between campaign and ad set budget (CBO/ABO), pixel custom conversions, placements and Advantage+ audience |
| Ad sets | 11 | List, inspect, pause, activate, delete, clone with or without ads, bid cap, end date, insights |
| Ads | 26 | List with insights, edit copy, headline, URL, UTMs and CTA, turn off Advantage+ creative enhancements, bulk pause and activate, clone, upload images and videos (from chat, Google Drive or Instagram links), publishing queue status, free up space in a full ad set, scheduled ads |
| Lead forms | 5 | List forms, see which ads use them, swap the form of an ad, duplicate and create instant forms |
| Audiences | 12 | Custom, engagement, customer list and lookalike audiences, size and diagnostics, suggestions from the account, clone to other accounts, delete |
| Targeting | 9 | Search locations, interests and behaviors, read and update locations, detailed targeting and device targeting across ad sets, audience size estimate |
| Pages, Instagram, pixels and catalogs | 18 | Pages, Instagram accounts and followers, page and Instagram videos, pixel events, catalogs, product sets and products, catalog ads, scheduled catalog media swaps |
| Batch operations | 3 | Update many campaigns, ad sets or ads in one call, with async jobs for large batches |

### Google Ads: 124 tools

| Category | Tools | What the assistant can do |
|---|---:|---|
| Accounts and recommendations | 11 | List accounts and manager (MCC) access, account selection, optimization score, apply or dismiss Google's recommendations |
| Campaigns | 34 | List, inspect, create Search and Performance Max campaigns (paused), draft a campaign with AI from a website, budgets, bidding, status, rename, locations, final URL suffix (UTMs), asset groups, images and YouTube videos, duplicate in the same or another account, campaign templates |
| Ad groups and ads | 16 | Create, rename, pause, activate and duplicate ad groups and ads, target CPA per ad group, edit responsive search ads |
| Keywords and search terms | 15 | Add, edit and remove keywords, change match type, keyword ideas, search terms, negative keywords and shared negative lists |
| Demographics | 2 | Read and adjust age, gender, household income and parental status |
| Schedule, devices and segments | 4 | Performance by segment, ad schedule, device bid adjustments |
| Audiences | 11 | Remarketing lists, custom segments (with competitor site suggestions), combined lists, audience targeting and bid adjustments |
| Assets | 7 | Sitelinks, callouts and structured snippets: create, edit, remove |
| Conversions | 9 | Conversion actions, campaign conversion goals, offline conversion upload and settings |
| Dates, labels and experiments | 12 | Campaign start and end dates, labels, experiments (create, end, apply, remove) |
| Shopping | 3 | Linked Merchant Center accounts, link Merchant Center to Performance Max, create Shopping campaigns |

### Ads Editor platform: 108 tools

| Category | Tools | What the assistant can do |
|---|---:|---|
| AI optimization | 31 | Automatic budget optimization for Meta and Google: create, edit, pause, history and the reason for each decision, suggestions to approve or dismiss (Business plan and above) |
| Reports | 19 | Create and edit shareable client reports (Meta, Google and Instagram, including Stories), templates, AI period analysis, access logs |
| Monitor and balance | 18 | Ad account balance and status across accounts, account groups, hide accounts, spend alerts above or below a daily reference |
| AI analyses | 14 | Account diagnosis, creative analysis, competitor ads from the Meta Ad Library and the Google Ads Transparency Center, Google ads strength analysis |
| Alerts and notifications | 10 | Alerts on CPA, CPC, CPM, CTR, spend or ROAS thresholds and in-app notifications |
| Automated rules | 8 | Create, edit, toggle and delete rules that pause, activate or change budgets by condition, with execution history |
| Sales and UTMs | 3 | Apply UTMs to Meta campaigns and read sales from checkout platforms (Hotmart, Kiwify, Shopify, Stripe and others) matched to campaigns by UTM |
| Team | 3 | Team members, activity history and team dashboard |
| Internal | 2 | Support tools for the Ads Editor team, not available to customers |

## Connect your AI client

The steps mirror the connection screen inside the app (`/mcp`). Use `https://mcp.adseditor.app/mcp` for accounts created on adseditor.app and `https://mcp.adseditor.com.br/mcp` for accounts on adseditor.com.br. Menu names change between client versions; if a label differs, look for "connectors", "plugins" or "MCP servers".

Before you start: create an Ads Editor account (7-day free trial) and connect at least one Meta or Google ad account at [adseditor.app](https://adseditor.app).

### Claude (claude.ai and Claude Desktop)

1. Open **Customize → Connectors**, click **+ Add** and then **Add custom connector**. (The free Claude plan allows one custom connector.)
2. Name: `Ads Editor`. Remote MCP server URL: `https://mcp.adseditor.app/mcp`.
3. Click **Continue**. The browser opens the Ads Editor authorization screen: log in and click **Authorize**.
4. In a chat, enable Ads Editor under **+ → Connectors**.

On Team or Enterprise, the organization owner adds the connector under **Organization settings → Connectors**, then each person clicks **Connect**.

### ChatGPT

Requires a paid ChatGPT plan, in the browser (the free plan and the mobile app do not have this option). On Business or Enterprise, an admin has to allow MCP plugins first.

1. Click **Plugins** in the left sidebar (or open `chatgpt.com/plugins`).
2. Click **Add** and choose **Add custom MCP server**.
3. Name: `Ads Editor`. Server URL: `https://mcp.adseditor.app/mcp`. Keep Authentication on **OAuth**, tick **I understand and want to continue** and click **Create as a plugin**.
4. Authorize in the Ads Editor screen that opens.
5. Enable the Ads Editor plugin in a new conversation.

### Cursor

Add the server to `~/.cursor/mcp.json` (global) or `.cursor/mcp.json` (project):

```json
{
  "mcpServers": {
    "adseditor": {
      "url": "https://mcp.adseditor.app/mcp"
    }
  }
}
```

`adseditor` appears in the MCP server list (under **Customize** in Cursor's sidebar). When Cursor asks you to log in, authorize in the browser. This repository also ships a Cursor plugin package ([`.cursor-plugin/plugin.json`](.cursor-plugin/plugin.json) and [`mcp.json`](mcp.json)) that points to the same remote server.

### Claude Code

```bash
claude mcp add --transport http adseditor https://mcp.adseditor.app/mcp
```

Then run `/mcp`, choose `adseditor` and **Authenticate**. The browser opens the Ads Editor authorization screen.

### Other clients

<details>
<summary>Codex, Grok, Gemini CLI, Windsurf, VS Code and clients without OAuth</summary>

**Codex CLI**

```bash
codex mcp add adseditor --url https://mcp.adseditor.app/mcp
codex mcp login adseditor
```

**Grok:** on grok.com open **Settings → Connect Apps**, scroll to **Add a custom connector**, name it `ads-editor`, paste `https://mcp.adseditor.app/mcp`, click **Add MCP** and authorize.

**Gemini CLI**

```bash
gemini mcp add --transport http adseditor https://mcp.adseditor.app/mcp
```

Then run `/mcp auth adseditor` and authorize in the browser.

**Windsurf** (`mcp_config.json`, opened from the Cascade MCP list with **Open MCP config file**):

```json
{
  "mcpServers": {
    "adseditor": {
      "serverUrl": "https://mcp.adseditor.app/mcp"
    }
  }
}
```

**VS Code** (GitHub Copilot agent mode), `.vscode/mcp.json`:

```json
{
  "servers": {
    "adseditor": {
      "type": "http",
      "url": "https://mcp.adseditor.app/mcp"
    }
  }
}
```

**Clients without OAuth:** generate a personal token on the app's MCP page (**New Token**) and send `Authorization: Bearer YOUR_TOKEN`. For stdio-only clients, use the `mcp-remote` bridge (requires Node.js):

```json
{
  "mcpServers": {
    "adseditor": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mcp.adseditor.app/mcp", "--header", "Authorization:Bearer YOUR_TOKEN"]
    }
  }
}
```

</details>

Open a **new** conversation after connecting: a chat opened before the connector was added does not see the tools.

## Example prompts

**Reporting**
- "List the active campaigns in account X with spend, CPA and ROAS for the last 7 days, sorted by spend."
- "Compare Meta and Google results for client Y this month and tell me where the cost per lead is lower."
- "Which ads have rising frequency and falling CTR this week?"

**Balance and alerts**
- "Which of my ad accounts will run out of balance before the end of the week at the current daily spend?"
- "Create an alert if any campaign in account X spends more than $200 in a day."

**Bulk changes (Meta)**
- "Clone campaign Y from account A to account B, swapping the Page, Instagram, pixel and WhatsApp number for account B's. Keep it paused."
- "Upload these 3 videos as new ads in every active ad set of campaign Z, with the same copy as the current best ad."
- "Create website visitor audiences for 30, 90 and 180 days, plus a 1% lookalike of each, in accounts A, B and C."
- "Increase the budget of campaign Z by 20% in two steps."

**Google Ads**
- "Show the search terms that spent the most without conversions in the last 30 days and add the irrelevant ones as negatives."
- "Add this list of negative keywords to every Search campaign in account X."
- "Set our standard UTMs in the final URL suffix of all campaigns in account Y."

**Rules and sales**
- "Create a rule that pauses any ad set with CPA above twice the target for 2 days in a row."
- "How many Hotmart sales came from campaign Z this week, and what was the cost per sale?"

## Security and permissions

- **One identity per person.** Each user authorizes with their own Ads Editor login (OAuth 2.1, discovery at `/.well-known/oauth-protected-resource`) or a personal token that can be revoked on the MCP page, with an activity log.
- **Per-account permissions.** Team members only see and act on the ad accounts released to them. Tools from an area the member has no access to are hidden from the list and refused on call.
- **Writes with brakes.** Campaigns, ad sets and ads created or cloned by the assistant start **paused**, and large budget changes ask for confirmation.
- **Platform credentials stay on the server.** Meta and Google tokens are stored encrypted (AES-256) on the Ads Editor side and never pass through the AI client.
- **Two-factor authentication** is available to every Ads Editor account.

## Plans and limits

MCP is included from the **Pro** plan: US$39/month on [adseditor.app/pricing](https://adseditor.app/pricing) or R$197/month on [adseditor.com.br/pricing](https://adseditor.com.br/pricing), 20% off on yearly billing. The 7-day free trial includes MCP. AI optimization tools need the Business plan or above. The pricing pages are the source of truth.

## FAQ

**Is there a Meta Ads MCP server that also manages Google Ads?**
Yes. Ads Editor MCP is one remote server for Meta Ads and Google Ads, so the same assistant can compare and act on both platforms in one conversation.

**Can it write, or only read?**
Both. Most categories have read and action tools. New campaigns, ad sets and ads are created paused, and team permissions apply to every call.

**Do I need to install anything?**
No. It is a remote Streamable HTTP server: add the URL to your client and authorize in the browser. A token or the `mcp-remote` bridge is only needed for clients without OAuth.

**Which Meta and Google features are not covered?**
Ads Editor works with Meta Ads and Google Ads only (no TikTok, LinkedIn or other networks). Google Video (YouTube) campaigns cannot be created or edited.

**Is the server open source?**
No. This repository holds the public connection package (`server.json`, `mcp.json`, Cursor plugin metadata, logo) and documentation. The server runs on Ads Editor infrastructure.

**Is Ads Editor the same as Google Ads Editor?**
No. Google Ads Editor is Google's free desktop app for Google Ads only. Ads Editor is an independent web and iPhone platform for Meta Ads and Google Ads across many accounts.

## Links

- Product: [adseditor.app](https://adseditor.app) (English) · [adseditor.com.br](https://adseditor.com.br) (Português)
- Tool catalog: [adseditor.app/mcp](https://adseditor.app/mcp)
- Pricing: [adseditor.app/pricing](https://adseditor.app/pricing)
- Help center: [help.adseditor.app](https://help.adseditor.app/help) · [help.adseditor.com.br](https://help.adseditor.com.br/ajuda)
- Guides: [Meta Ads MCP: connect Claude and ChatGPT to your ad accounts](https://adseditor.app/blog/meta-ads-mcp-claude-chatgpt) · [Meta Ads MCP usage data](https://adseditor.app/blog/meta-ads-mcp-usage-data) · [AI for media buying](https://adseditor.app/blog/ai-for-media-buying)
- Official MCP Registry: [`br.com.adseditor/mcp`](https://registry.modelcontextprotocol.io/v0/servers?search=br.com.adseditor)
- Glama: [glama.ai/mcp/connectors/br.com.adseditor/mcp](https://glama.ai/mcp/connectors/br.com.adseditor/mcp)
- iPhone app: [App Store](https://apps.apple.com/app/ads-editor/id6761736675)
- Open-source examples with the Meta Marketing API: [meta-ads-balance-alert](https://github.com/theusmyep/meta-ads-balance-alert) · [meta-bulk-custom-audiences](https://github.com/theusmyep/meta-bulk-custom-audiences)

---

## Português

O **Ads Editor MCP** é o servidor MCP remoto do [Ads Editor](https://adseditor.com.br): **354 ferramentas** (contadas em 25/11/2026) para consultar e operar **Meta Ads e Google Ads** pelo Claude, ChatGPT, Cursor, Claude Code, Codex, Grok, Gemini CLI, Windsurf e VS Code. Relatórios, clone de campanha entre contas, subida de anúncios em massa, públicos, orçamento, negativas, regras, alertas e saldo das contas.

- **URL:** `https://mcp.adseditor.com.br/mcp` (contas em português). Transporte HTTP (Streamable), OAuth ou token pessoal.
- **Claude:** Personalização → Conectores → + Adicionar → Adicionar conector personalizado → nome `Ads Editor`, cole a URL → Continuar → Autorizar.
- **ChatGPT** (plano pago, no navegador): Plugins → Adicionar → Adicionar servidor MCP personalizado → URL, autenticação OAuth → Criar como plugin.
- **Claude Code:** `claude mcp add --transport http adseditor https://mcp.adseditor.com.br/mcp` e depois `/mcp` → Authenticate.
- **Cursor:** o mesmo `mcp.json` da seção em inglês, com a URL `.com.br`.
- **Plano:** MCP a partir do Pro (R$ 197 por mês), 7 dias de teste. Catálogo completo em [adseditor.com.br/mcp](https://adseditor.com.br/mcp).

O Ads Editor é uma plataforma independente. Não é o Google Ads Editor nem produto da Meta ou do Google.

## About this repository

- `server.json`: metadata for the official MCP Registry.
- `mcp.json`: remote server address for clients and the Cursor plugin, without credentials.
- `.cursor-plugin/plugin.json`: Cursor plugin metadata.
- `assets/logo.svg`: Ads Editor icon.

The server source code, tool implementations, database and credentials are not distributed here. Downloading these files does not let anyone run a copy of the Ads Editor server, and the public connection package grants no access to the service or license to the private code or the brand.
