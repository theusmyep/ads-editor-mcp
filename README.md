# Ads Editor MCP: Meta Ads e Google Ads por conversa

Servidor MCP (Model Context Protocol) do **Ads Editor**, plataforma independente de gestão de Meta Ads e Google Ads para gestores de tráfego e agências. Com ele, o Claude, o ChatGPT, o Codex e o Cursor consultam e executam ações nas suas contas de anúncio: listar campanhas, criar conjuntos, clonar entre contas, ajustar orçamento, criar regras, ler relatórios e vendas.

O Ads Editor não é o Google Ads Editor nem um produto da Meta ou do Google. Este repositório contém apenas a documentação; o servidor é remoto e roda em app.adseditor.com.br.

- Site: https://adseditor.com.br
- Catálogo das ferramentas e tela de conexão: https://adseditor.com.br/mcp
- Blog com guias: https://adseditor.com.br/blog
- Contagem atual: **212 ferramentas** (registro conferido em 23/09/2026)

## O que é

Um servidor MCP remoto (Streamable HTTP) que expõe as funções do Ads Editor como ferramentas para clientes de IA. Cada usuário conecta com a própria credencial e só enxerga as contas às quais tem permissão dentro do Ads Editor.

Diferença para os conectores oficiais: o conector da Meta cobre só a Meta e o do Google é só de leitura. O Ads Editor cobre Meta Ads e Google Ads, lê e escreve, e soma funções da própria plataforma (regras, escala, monitor de saldo, relatórios, vendas por UTM).

## Como conectar

Pré-requisito: conta no Ads Editor (7 dias de teste) com pelo menos uma conta de anúncio conectada. A URL e a forma de autenticação (OAuth ou token pessoal) aparecem em https://app.adseditor.com.br/mcp. Os passos abaixo seguem o formato genérico de servidor MCP remoto; a tela de cada cliente muda com a versão, então confira a documentação do cliente se algum menu tiver outro nome.

### Claude (Desktop e web)

1. Configurações > Conectores > Adicionar conector personalizado.
2. Nome: `Ads Editor`. URL: `https://app.adseditor.com.br/mcp`.
3. Autorize quando o Claude abrir a tela de login do Ads Editor.

Claude Code (terminal):

```bash
claude mcp add --transport http adseditor "https://app.adseditor.com.br/mcp"
```

### ChatGPT

1. Configurações > Conectores > Criar (é preciso ativar o modo de desenvolvedor).
2. Nome: `Ads Editor`. URL do servidor MCP: `https://app.adseditor.com.br/mcp`.
3. Autenticação: OAuth. Autorize na tela do Ads Editor.
4. Em uma conversa nova, ative o conector Ads Editor. Conversa aberta antes do cadastro não vê as ferramentas.

### Codex

```bash
codex mcp add adseditor --url "https://app.adseditor.com.br/mcp"
```

Ou em `~/.codex/config.toml`:

```toml
[mcp_servers.adseditor]
url = "https://app.adseditor.com.br/mcp"
```

### Cursor

Em `.cursor/mcp.json` (projeto) ou `~/.cursor/mcp.json` (global):

```json
{
  "mcpServers": {
    "adseditor": {
      "url": "https://app.adseditor.com.br/mcp"
    }
  }
}
```

Se a tela do Ads Editor entregar um token pessoal em vez de OAuth, acrescente `"headers": { "Authorization": "Bearer <token>" }` dentro de `adseditor`.

## Grupos de ferramentas (212 no total)

| Grupo | Ferramentas | O que faz |
|---|---|---|
| Meta: contas | 8 | Listar contas, páginas, pixels e ativos ligados |
| Meta: campanhas | 14 | Listar, criar, editar, pausar, ativar, clonar entre contas |
| Meta: conjuntos de anúncios | 10 | Segmentação, orçamento, posicionamento, clone |
| Meta: anúncios | 20 | Criar, editar, subir mídia, textos, UTM, pausar |
| Meta: formulários de lead | 5 | Listar e reaproveitar formulários |
| Meta: públicos | 10 | Criar públicos em massa, lookalike, listar |
| Meta: páginas | 7 | Página, Instagram e WhatsApp ligados à conta |
| Meta: lote | 3 | Operações em massa em várias contas |
| Meta: dispositivos | 2 | Segmentação por dispositivo |
| Meta: localizações | 3 | Busca de cidade, região e raio |
| Google: contas | 6 | Listar contas e MCC |
| Google: campanhas | 23 | Pesquisa, Performance Max, orçamento, UTM, status |
| Google: grupos de anúncios | 16 | Grupos, anúncios responsivos, ajustes |
| Google: palavras-chave | 9 | Adicionar, negativar, listar |
| Google: demografia | 2 | Ajustes por idade e gênero |
| Google: extensões | 7 | Sitelinks, frases de destaque e outros recursos |
| Google: conversões | 5 | Ações de conversão |
| Google: escala | 11 | Tetos, escala e pacing de orçamento |
| Relatórios | 12 | Métricas por período, relatório em link para o cliente |
| Regras | 8 | Criar, listar e editar regras automatizadas |
| Escala de orçamento (Meta) | 10 | Escala automática e histórico |
| Monitor | 7 | Saldo e estado das contas |
| Alertas | 10 | Alertas de métrica e de conta |
| Vendas | 2 | Vendas por UTM (webhooks das plataformas) |
| Plataforma | 2 | Estado da conexão e do plano |

A lista com o nome de cada ferramenta fica em https://adseditor.com.br/mcp.

## Exemplos de prompt

- "Liste as campanhas ativas da conta X com gasto e resultado dos últimos 7 dias."
- "Clone a campanha Y da conta A para a conta B trocando a página, o Instagram, o pixel e o WhatsApp pelos da conta B. Deixe pausada."
- "Crie 5 públicos de envolvimento no Instagram nas contas A, B e C, com os mesmos nomes."
- "Quais contas estão com saldo abaixo do gasto diário previsto?"
- "Crie uma regra que pause qualquer conjunto com CPA acima do dobro da meta por 2 dias seguidos."
- "No Google Ads, adicione estas palavras-chave negativas em todas as campanhas de pesquisa da conta X."
- "Quantas vendas da Hotmart vieram da campanha Z esta semana e qual foi o custo por venda?"

## Segurança

- **Identidade:** cada usuário conecta com a própria conta do Ads Editor, por OAuth ou token pessoal gerado na tela de MCP. O token é do usuário, não da empresa, e pode ser revogado ali.
- **Permissão por conta:** membro de equipe só enxerga e só age nas contas liberadas para ele no Ads Editor. A permissão vale também no MCP: ferramenta de uma área sem permissão não aparece na lista e é negada na chamada.
- **Escrita com freio:** campanhas, conjuntos e anúncios criados ou clonados pela IA nascem pausados; há teto de segurança para orçamento diário criado ou alterado por ferramenta.
- **Credenciais das plataformas:** os tokens da Meta e do Google ficam cifrados no servidor e nunca passam pelo cliente de IA.
- **2FA:** disponível para toda conta do Ads Editor.

## Preços

Planos de R$ 97 por mês (10 contas) a R$ 697 por mês (70 contas), 20% de desconto no anual, 7 dias de teste. O MCP está incluído nos planos; detalhes em https://adseditor.com.br/pricing.

---

## English

**Ads Editor MCP** is a remote MCP server (Streamable HTTP) for [Ads Editor](https://adseditor.com.br), an independent Meta Ads and Google Ads management platform for media buyers and agencies. It exposes 212 tools (count taken from the tool registry on 2026-09-23) so Claude, ChatGPT, Codex and Cursor can read and write to your ad accounts: list and create campaigns, clone campaigns between accounts while swapping Page, Instagram, pixel and WhatsApp, create audiences in bulk, adjust budgets, create automated rules, read reports and UTM-attributed sales, and manage Google Ads (Search, Performance Max, negative keywords).

Ads Editor is not Google Ads Editor and not a Meta or Google product.

**Connect:** get the server URL and credentials at https://app.adseditor.com.br/mcp, then add it as a remote MCP server in your client (Claude: Settings > Connectors > Add custom connector; ChatGPT: Settings > Connectors > Create, developer mode; Codex: `codex mcp add adseditor --url <URL>`; Cursor: `.cursor/mcp.json` with `"url"`).

**Security:** OAuth or per-user token, per-account permissions for team members, AI-created objects start paused, platform tokens encrypted server-side, 2FA available.

**Pricing:** from R$ 97/month (10 ad accounts) to R$ 697/month (70 ad accounts), 20% off yearly, 7-day trial. Interface in Portuguese (Brazil).

Tool catalog: https://adseditor.com.br/mcp. Guides: https://adseditor.com.br/blog.
