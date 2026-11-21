# Ads Editor MCP: Meta Ads MCP and Google Ads MCP server

**Ads Editor MCP** is a remote [Model Context Protocol](https://modelcontextprotocol.io) server that connects **Meta Ads (Facebook and Instagram Ads)** and **Google Ads** to AI assistants such as **Claude, ChatGPT, Cursor, Codex, Grok, Gemini CLI, Windsurf and VS Code**. It has **more than 350 tools** to read *and* run ad accounts in plain language: report on spend and results, clone campaigns between ad accounts, create audiences in bulk, adjust budgets, add negative keywords, set automated rules and follow ad account balances.

| | |
|---|---|
| Server URL (Portuguese accounts) | `https://mcp.adseditor.com.br/mcp` |
| Server URL (English accounts) | `https://mcp.adseditor.app/mcp` |
| Transport | Streamable HTTP (remote, nothing to install) |
| Authentication | OAuth 2.1 (recommended) or a personal bearer token |
| Registry name | [`br.com.adseditor/mcp`](https://registry.modelcontextprotocol.io/v0/servers?search=br.com.adseditor) in the official MCP Registry |
| Platforms | Meta Ads and Google Ads, in one server |
| Full tool catalog | [adseditor.app/mcp](https://adseditor.app/mcp) (English) · [adseditor.com.br/mcp](https://adseditor.com.br/mcp) (Português) |

Ads Editor is an independent platform for media buyers and agencies that manage many ad accounts. It is **not** Google Ads Editor and not a Meta or Google product; it connects through the official Meta Marketing API and Google Ads API.

> Português: [veja a versão em português abaixo](#português).

## Contents

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Connect your AI client](#connect-your-ai-client)
- [Tool categories](#tool-categories)
- [Example prompts](#example-prompts)
- [Security and OAuth](#security-and-oauth)
- [Plans](#plans)
- [FAQ](#faq)
- [Guides and help center](#guides-and-help-center)
- [Português](#português)

## What it does

You ask, the assistant calls the right Ads Editor tools, and the change happens in the ad account (or you get the numbers back). Examples of what one request can cover:

- **Reporting across accounts:** spend, results, CPA and ROAS by campaign, ad set or ad, with breakdowns (age, gender, placement, device, hour).
- **Cross-account cloning:** copy a Meta campaign to another ad account and swap the Facebook Page, Instagram account, pixel and WhatsApp number in the same step.
- **Bulk work:** create the same audiences in several ad accounts, pause or activate many objects, edit UTMs, upload creatives through the same publishing queue the web editor uses.
- **Google Ads:** Search and Performance Max campaigns, ad groups and responsive search ads, keywords, search terms, negative keyword lists, assets (sitelinks, callouts), audiences, schedules, conversions and Shopping.
- **Guardrails from the platform:** automated rules, alerts, balance monitor and UTM-attributed sales from checkout platforms, all reachable from chat.

Google's own [Google Ads MCP server](https://github.com/googleads/google-ads-mcp) exposes three retrieval tools (`search`, `get_resource_metadata`, `list_accessible_customers`, checked on 17 Oct 2026). Ads Editor MCP covers Meta Ads and Google Ads together and can write to the accounts, within each user's permissions.

## Quick start

1. Create an Ads Editor account (7-day free trial) and connect at least one Meta or Google ad account: [adseditor.app](https://adseditor.app) (English) or [adseditor.com.br](https://adseditor.com.br) (Português). MCP is part of the Pro plan and above.
2. Add the server URL to your AI client as a remote MCP server (Streamable HTTP).
3. Your browser opens the Ads Editor authorization screen. Log in and click **Authorize**.
4. Open a **new** chat and ask something like "list my active Meta campaigns with spend for the last 7 days".

Accounts created on adseditor.app use `https://mcp.adseditor.app/mcp`; accounts on adseditor.com.br use `https://mcp.adseditor.com.br/mcp`. The examples below use the English URL. The older address `https://app.adseditor.com.br/mcp` keeps working.

## Connect your AI client

The steps mirror the connection screen inside the app (`/mcp`). Menu names change between client versions; if a label differs, look for "connectors" or "MCP servers".

### Claude (claude.ai and Claude Desktop)

Pro, Max, Team or Enterprise plans:

1. **Settings → Connectors → Add custom connector**.
2. Name: `Ads Editor`. Remote MCP server URL: `https://mcp.adseditor.app/mcp`.
3. Click **Add**, then **Authorize** in the browser.

### Claude Code

```bash
claude mcp add --transport http adseditor https://mcp.adseditor.app/mcp
```

Then run `/mcp`, choose `adseditor` and **Authenticate**.

### ChatGPT

Requires ChatGPT Plus, Pro, Team or Enterprise (the free plan does not support MCP connectors).

1. **Settings → Connectors**, create a custom connector (some plans require **Developer mode** first).
2. Name: `Ads Editor`. MCP server URL: `https://mcp.adseditor.app/mcp`. Authentication: **OAuth**.
3. Click **Create**, then **Connect**, and authorize in the browser.
4. Enable the Ads Editor connector in a new conversation.

### Codex CLI

```bash
codex mcp add adseditor --url https://mcp.adseditor.app/mcp
codex mcp login adseditor
```

### Cursor

`~/.cursor/mcp.json` (global) or `.cursor/mcp.json` (project):

```json
{
  "mcpServers": {
    "adseditor": {
      "url": "https://mcp.adseditor.app/mcp"
    }
  }
}
```

Open Cursor's MCP settings and click **Connect** next to `adseditor`. This repository also ships a Cursor plugin package (`.cursor-plugin/plugin.json` + [`mcp.json`](mcp.json)) that points to the same remote server; it does not install a local server.

### Grok

1. Open [grok.com/connectors](https://grok.com/connectors) → **New Connector** → **Custom**.
2. Name: `Ads Editor`. URL: `https://mcp.adseditor.app/mcp`.
3. **Connect** and authorize.

### Gemini CLI

```bash
gemini mcp add --transport http adseditor https://mcp.adseditor.app/mcp
```

Inside Gemini CLI run `/mcp auth adseditor`, authorize in the browser, then `/mcp list`.

### Windsurf

`~/.codeium/windsurf/mcp_config.json`:

```json
{
  "mcpServers": {
    "adseditor": {
      "serverUrl": "https://mcp.adseditor.app/mcp"
    }
  }
}
```

### VS Code (GitHub Copilot agent mode)

Command palette → **MCP: Add Server** → **HTTP** → paste `https://mcp.adseditor.app/mcp`, name it `adseditor`, and authorize when asked. Or in `.vscode/mcp.json`:

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

### Clients without OAuth

Generate a personal token on the app's MCP page (**New Token**) and send it as a header:

```
Authorization: Bearer YOUR_TOKEN
```

For stdio-only clients, use the `mcp-remote` bridge (requires Node.js):

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

## Tool categories

More than 350 tools, grouped the same way as the public catalog. Read tools only query data; action tools change something in the account. The exact list a user sees depends on the plan and on team permissions, and the up-to-date catalog with every tool name is at [adseditor.app/mcp](https://adseditor.app/mcp).

**Meta Ads (Facebook and Instagram)**

| Category | What the assistant can do |
|---|---|
| Accounts and insights | List ad accounts, dashboards, account-level metrics, breakdowns by age, gender, placement, device and hour, charges |
| Campaigns | List, inspect, create (always paused), rename, pause, activate, change budget, clone within or across accounts |
| Ad sets | Targeting, budgets, bid caps and strategies, end dates, clone with or without ads |
| Ads and media | Create and edit ads, primary text, headline, URL, UTMs, CTA, upload images and videos, publishing queue status |
| Lead forms | List, duplicate and create instant forms, swap the form used by an ad |
| Audiences | Custom audiences, lookalikes, Instagram and engagement audiences, bulk creation across accounts |
| Locations and devices | Search cities, regions and radius targeting, device targeting |
| Pages, Instagram and pixels | Pages, Instagram accounts, WhatsApp numbers and pixels linked to each account |
| Batch operations | Update many campaigns, ad sets or ads in one call, with async jobs for large batches |

**Google Ads**

| Category | What the assistant can do |
|---|---|
| Accounts and recommendations | List accounts and manager (MCC) hierarchy, optimization score and recommendations |
| Campaigns | Search and Performance Max, creation, budgets, bidding, status, final URL suffix (UTMs) |
| Ad groups and ads | Ad groups, responsive search ads, Performance Max asset groups |
| Keywords and search terms | Add keywords, read search terms, negative keywords and shared negative lists |
| Demographics | Exclude or adjust bids by gender, age, household income and parental status |
| Hours, devices and segments | Performance by device, hour, weekday and landing page, schedule and device adjustments |
| Audiences | Remarketing, custom segments, combined audiences |
| Assets | Sitelinks, callouts and other assets |
| Conversions | List and create conversion actions (with the tag), campaign conversion goals, offline conversions |
| Dates, labels and experiments | Campaign start and end dates, labels across campaigns, ad groups and ads, experiments |
| Shopping and Merchant Center | Check the linked Merchant Center, link it to Performance Max, create standard Shopping campaigns |

**Ads Editor platform**

| Category | What the assistant can do |
|---|---|
| Reports | Metrics by period and shareable client report links |
| Automated rules | Create, list and edit rules that pause, activate or change budgets by condition |
| Monitor and balance | Ad account balance and status across accounts |
| Alerts and notifications | Alerts on CPA, CPC, CPM, CTR, spend or ROAS thresholds, in-app notifications |
| Sales and UTMs | Sales from checkout platforms (Hotmart, Kiwify and others) matched to campaigns by UTM |

Business and higher plans also unlock AI optimization tools (automatic budget scaling).

## Example prompts

- "List the active campaigns in account X with spend, CPA and ROAS for the last 7 days."
- "Which of my ad accounts will run out of balance before the end of the week at the current daily spend?"
- "Clone campaign Y from account A to account B, swapping the Page, Instagram, pixel and WhatsApp number for account B's. Keep it paused."
- "Create website visitor audiences for 30, 90 and 180 days, plus a 1% lookalike of each, in accounts A, B and C."
- "Pause every ad with CPA above $40 in the last 7 days and tell me what you paused."
- "Create a rule that pauses any ad set with CPA above twice the target for 2 days in a row."
- "In Google Ads, add these negative keywords to every Search campaign in account X."
- "Set our standard UTMs on all Google Ads campaigns in account Y."
- "How many Hotmart sales came from campaign Z this week, and what was the cost per sale?"

## Security and OAuth

- **One identity per person.** Each user authorizes with their own Ads Editor login (OAuth 2.1 with discovery at `/.well-known/oauth-protected-resource`) or a personal token that can be revoked on the MCP page.
- **Per-account permissions.** Team members only see and act on the ad accounts released to them. Tools from an area the member has no access to are hidden from the list and refused on call.
- **Writes with brakes.** Campaigns, ad sets and ads created or cloned by the assistant start **paused**, and there is a safety cap on budgets created or changed by a tool.
- **Platform credentials stay on the server.** Meta and Google tokens are stored encrypted on the Ads Editor side and never pass through the AI client.
- **Two-factor authentication** is available to every Ads Editor account.

## Plans

MCP is included from the **Pro** plan: US$39/month on [adseditor.app/pricing](https://adseditor.app/pricing) or R$197/month on [adseditor.com.br/pricing](https://adseditor.com.br/pricing), with a 7-day free trial. Prices checked on 17 Oct 2026; the pricing pages are the source of truth.

## FAQ

**Is there a Meta Ads MCP server that can also manage Google Ads?**
Yes. Ads Editor MCP is a single remote server for both Meta Ads and Google Ads, so one assistant can compare and act on both platforms in the same conversation.

**Do I need to install anything?**
No. It is a remote Streamable HTTP server. You add the URL to your client and authorize in the browser. A token or the `mcp-remote` bridge is only needed for clients without OAuth.

**Can the AI change my campaigns without me noticing?**
It only acts when you ask. New campaigns, ad sets and ads are created paused, and team permissions apply to every tool call.

**Is the server open source?**
No. This repository holds the public connection package (`server.json`, `mcp.json`, Cursor plugin metadata, logo) and documentation. The server runs on Ads Editor infrastructure.

**Is Ads Editor the same as Google Ads Editor?**
No. Google Ads Editor is Google's free desktop app for Google Ads only. Ads Editor is an independent web platform for Meta Ads and Google Ads across many accounts.

## Guides and help center

English:
- [Meta Ads MCP: connect Claude and ChatGPT to your ad accounts](https://adseditor.app/blog/meta-ads-mcp-claude-chatgpt)
- [Meta Ads MCP usage data: the tools media buyers actually call](https://adseditor.app/blog/meta-ads-mcp-usage-data)
- [AI for media buying](https://adseditor.app/blog/ai-for-media-buying)
- [Help center](https://help.adseditor.app/help) · [Can AI Copilot or MCP create rules and alerts in Google Ads?](https://help.adseditor.app/help/can-ai-copilot-or-mcp-create-rules-and-alerts-in-google-ads)

Português:
- [MCP de Meta Ads e Google Ads no Claude e no ChatGPT](https://adseditor.com.br/blog/mcp-meta-ads-google-ads-claude-chatgpt)
- [MCP em números: as ferramentas mais usadas](https://adseditor.com.br/blog/mcp-em-numeros-ferramentas-mais-usadas)
- [IA para gestor de tráfego](https://adseditor.com.br/blog/ia-para-gestor-de-trafego)
- [Central de ajuda](https://help.adseditor.com.br/ajuda) · [O Copiloto IA ou o MCP conseguem criar regras e alertas no Google Ads?](https://help.adseditor.com.br/ajuda/o-copiloto-ia-ou-o-mcp-conseguem-criar-regras-e-alertas-no-google-ads)

Open-source examples that use the Meta Marketing API directly:
- [meta-ads-balance-alert](https://github.com/theusmyep/meta-ads-balance-alert): low balance alerts for many Meta ad accounts.
- [meta-bulk-custom-audiences](https://github.com/theusmyep/meta-bulk-custom-audiences): create custom and lookalike audiences in bulk from a CSV.

---

## Português

O **Ads Editor MCP** é um servidor remoto de [Model Context Protocol](https://modelcontextprotocol.io) que liga **Meta Ads** e **Google Ads** a assistentes de IA como **Claude, ChatGPT, Cursor, Codex, Grok, Gemini CLI, Windsurf e VS Code**. São **mais de 350 ferramentas** para consultar e operar contas de anúncio por conversa: relatórios de gasto e resultado, clone de campanha entre contas, públicos em massa, orçamento, palavras-chave negativas, regras automatizadas e saldo das contas.

O Ads Editor é uma plataforma independente para gestores de tráfego e agências. Não é o Google Ads Editor nem produto da Meta ou do Google.

**Endereço do servidor:** `https://mcp.adseditor.com.br/mcp` (contas em português) ou `https://mcp.adseditor.app/mcp` (contas em inglês). Transporte HTTP (Streamable), autenticação por OAuth ou token pessoal. O endereço antigo `https://app.adseditor.com.br/mcp` continua funcionando.

### Como conectar

1. Crie a conta no [Ads Editor](https://adseditor.com.br) (7 dias de teste) e conecte uma conta da Meta ou do Google. O MCP faz parte do plano Pro em diante (R$ 197 por mês, conferido em 17/10/2026 em [adseditor.com.br/pricing](https://adseditor.com.br/pricing)).
2. **Claude:** Configurações → Conectores → Adicionar conector personalizado → nome `Ads Editor`, URL `https://mcp.adseditor.com.br/mcp` → Autorizar.
3. **ChatGPT** (Plus, Pro, Team ou Enterprise): Settings → Connectors → criar conector (em alguns planos ative o Developer mode) → URL `https://mcp.adseditor.com.br/mcp`, autenticação OAuth → Create → Connect.
4. **Claude Code:** `claude mcp add --transport http adseditor https://mcp.adseditor.com.br/mcp`, depois `/mcp` → `adseditor` → Authenticate.
5. **Codex:** `codex mcp add adseditor --url https://mcp.adseditor.com.br/mcp` e `codex mcp login adseditor`.
6. **Cursor, Windsurf, VS Code, Grok e Gemini CLI:** os mesmos arquivos da seção em inglês, trocando a URL por `https://mcp.adseditor.com.br/mcp`.
7. Abra uma conversa **nova**: conversa aberta antes do cadastro não enxerga as ferramentas.

### Categorias de ferramentas

- **Meta:** contas e insights, campanhas, conjuntos, anúncios e mídia, formulários de lead, públicos, locais e aparelhos, páginas, Instagram e pixels, operações em lote.
- **Google:** contas e recomendações, campanhas (Pesquisa e Performance Max), grupos de anúncios e anúncios, palavras-chave e termos de pesquisa, listas de negativas, demografia, horários e aparelhos, públicos, extensões, conversões (inclusive offline), datas, rótulos e experimentos, Shopping e Merchant Center.
- **Plataforma:** relatórios, regras automatizadas, monitor de saldo, alertas e vendas por UTM.

O catálogo completo, com o nome de cada ferramenta, fica em [adseditor.com.br/mcp](https://adseditor.com.br/mcp).

### Exemplos de pedido

- "Liste as campanhas ativas da conta X com gasto, CPA e ROAS dos últimos 7 dias."
- "Quais contas vão ficar sem saldo antes do fim da semana no gasto diário atual?"
- "Clone a campanha Y da conta A para a conta B trocando página, Instagram, pixel e WhatsApp pelos da conta B. Deixe pausada."
- "Crie públicos de visitantes do site de 30, 90 e 180 dias e um semelhante de 1% de cada nas contas A, B e C."
- "No Google Ads, adicione estas palavras-chave negativas em todas as campanhas de pesquisa da conta X."
- "Quantas vendas da Hotmart vieram da campanha Z esta semana e qual foi o custo por venda?"

### Segurança

Cada pessoa autoriza com o próprio login (OAuth) ou token pessoal revogável. Membro de equipe só enxerga e só age nas contas liberadas para ele. O que a IA cria ou clona nasce pausado, há teto de segurança para orçamento alterado por ferramenta, os tokens da Meta e do Google ficam cifrados no servidor e o 2FA está disponível para toda conta.

### Guias

- [MCP de Meta Ads e Google Ads no Claude e no ChatGPT](https://adseditor.com.br/blog/mcp-meta-ads-google-ads-claude-chatgpt)
- [MCP em números: as ferramentas mais usadas](https://adseditor.com.br/blog/mcp-em-numeros-ferramentas-mais-usadas)
- [Central de ajuda](https://help.adseditor.com.br/ajuda)

## About this repository

- `server.json`: metadata for the official MCP Registry.
- `mcp.json`: remote server address for clients and the Cursor plugin, without credentials.
- `.cursor-plugin/plugin.json`: Cursor plugin metadata.
- `assets/logo.svg`: Ads Editor icon.

The server source code, tool implementations, database and credentials are not distributed here. Downloading these files does not let anyone run a copy of the Ads Editor server, and the public connection package grants no access to the service or license to the private code or the brand.
