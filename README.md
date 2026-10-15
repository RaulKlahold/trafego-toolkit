# trafego-toolkit

Skills de tráfego pago para o Claude Code — **Meta Ads** e **Google Ads** — adaptadas de
[ronydrop/ads-toolkit](https://github.com/ronydrop/ads-toolkit).

## O que mudou em relação ao original
- **Sem dados do autor**: nada de IDs de conta, produtos ou metas fixos. Tudo vem de uma
  ficha `CONFIG-CONTAS.md` que você preenche (uma por cliente, se quiser).
- **Modo seguro**: nenhuma skill pausa, ativa ou mexe em orçamento sem você confirmar aquela
  ação específica. O `/bleed-check` agora só recomenda.
- **Funciona sem API**: enquanto você não conecta as contas, as skills trabalham com
  relatórios exportados (CSV/XLSX) do Gerenciador de Anúncios e do Google Ads.
- **Leads ou vendas**: a métrica principal (CPL, CPA ou ROAS) vem da ficha.
- **Sem servidores MCP de terceiros embutidos**: a conexão com as APIs fica para você decidir.
- **/spy corrigido**: a API da Biblioteca de Anúncios não retorna anúncios comerciais do Brasil,
  então a skill usa o site da Biblioteca.

## Instalação
Na pasta onde está este README:
```bash
claude plugin marketplace add ./
claude plugin install meta-ads@trafego-toolkit
claude plugin install google-ads@trafego-toolkit
```
Abra uma nova sessão do Claude Code depois de instalar.

Para atualizar depois de editar as skills:
```bash
claude plugin marketplace update trafego-toolkit
```

## Configuração (pode fazer depois)
1. Copie `CONFIG-CONTAS.exemplo.md` como `CONFIG-CONTAS.md`:
   - na pasta de cada cliente (onde você abre o Claude Code), **ou**
   - em `~/.claude/ads-toolkit/CONFIG-CONTAS.md` como ficha padrão.
2. Preencha o que já souber. O que ficar `PREENCHER` o Claude pergunta quando precisar.
3. **Nunca** coloque tokens ou senhas na ficha.

## Comandos
### Meta Ads (`/meta-ads:...`)
| Comando | O que faz |
|---|---|
| `meta-performance` | Panorama da conta: CPR, CTR, frequência, alertas, ranking |
| `bleed-check` | Conjuntos gastando sem resultado → lista para pausar (com confirmação) |
| `fatigue-scan` | Fadiga criativa semana a semana + brief de substituição |
| `rebalance` | Plano de realocação de orçamento entre conjuntos ABO |
| `audience-audit` | Funil de públicos, sobreposição e exclusões faltando |
| `spy` | Anúncios dos concorrentes na Biblioteca de Anúncios |
| `copy-meta` | 3 variações de copy (A/B/C) |
| `hooks` | Dezenas de variações de gancho por framework, em CSV |
| `deploy-ads` | Cria campanhas em massa a partir de JSON — sempre pausadas |

### Google Ads (`/google-ads:...`)
| Comando | O que faz |
|---|---|
| `google-performance` | Panorama: CPA, CPC, CTR, parcela de impressões |
| `weekly-review` | Revisão semanal completa |
| `mine-search-terms` | Termos para negativar / manter / virar palavra-chave, em CSV |
| `rsa` | 15 títulos + 4 descrições com caracteres validados |
| `audit-ad-copy` | Nota 0–10 dos anúncios e sugestões |
| `budget-optimize` | Plano de redistribuição de orçamento |
| `investigate-campaign` | Diagnóstico de causa raiz de uma campanha |

Você também pode só pedir em linguagem natural ("tá sangrando alguma coisa no Meta?",
"quais termos eu negativo essa semana?") que a skill certa é carregada.

## Usando sem API (CSV)
Exporte o relatório e diga onde está o arquivo, por exemplo:
> "Analisa o fatigue-scan com o arquivo `exports/meta-anuncios-14d.csv`"

Se faltar alguma coluna, a skill diz quais exportar.

## Conectando as APIs (opcional, depois)
Para o Claude ler os dados direto das contas é preciso um conector (servidor MCP) para cada
plataforma, mais as credenciais:
- **Meta**: token de acesso de um app no Meta for Developers (de preferência de um
  usuário do sistema no Business Manager, com permissão `ads_read`; `ads_management` só se quiser
  que o Claude também aplique mudanças).
- **Google**: developer token (pedido pela conta MCC e sujeito a aprovação), OAuth client ID/secret
  e refresh token.

O original usava os pacotes npm `facebook-ads-mcp-server` e `@weppa-cloud/mcp-google-ads`.
São de terceiros e recebem suas credenciais — avalie antes de usar, principalmente em contas de
clientes. Comece com permissão **só de leitura**.
