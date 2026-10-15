---
name: budget-optimize
description: Plano de redistribuição de orçamento entre campanhas Google Ads — escala as limitadas por orçamento com bom CPA, corta as ruins, com limites de segurança. Só executa com confirmação. Triggers on "otimiza orçamento", "redistribui verba", "limitada pelo orçamento", "escalar campanha", "cortar campanha".
argument-hint: "[--lookback 7]"
---

# /budget-optimize — Otimização de orçamento
Carregar `account-conventions` e `performance-analysis`.

**Modo padrão: simulação.**

## Princípios
1. Não cortar o que funciona: CPA bom + perda por orçamento → aumentar.
2. Dados mínimos da ficha (padrão 3 dias para cortar, 7 para escalar).
3. Realocar antes de cortar: tirar de campanhas ruins e pôr nas boas.
4. Escala gradual: no máximo a escala da ficha (padrão 20%) por rodada.

## Regras de decisão
| Situação | Recomendação |
|---|---|
| Perda por orçamento alta + CPA ≤ meta | Aumentar orçamento |
| Custo alto + 0 conversão em 7d | Pausar/revisar palavras-chave, termos e copy |
| Perda por classificação alta + CPA bom | Rever lance/qualidade antes de pôr mais verba |
| Índice de qualidade < 6 nas principais palavras | Não aumentar — corrigir antes |
| Smart Bidding com < 15 conv./mês | Consolidar ou mudar estratégia antes de escalar |
| Orçamento compartilhado | Tratar o grupo de campanhas em conjunto |

## Workflow
1. Puxar 7d (e 30d para contexto) por campanha: orçamento diário, custo, conversões, CPA,
   perdas de parcela de impressões, estratégia de lance, se o orçamento é compartilhado.
2. Ordenar por CPA, identificar limitadas por orçamento.
3. Montar o plano antes → depois mantendo o total (ou dizendo quanto aumenta).
4. Perguntar se quer aplicar. Executar só após confirmação e registrar no log.

## Consulta (API)
```sql
SELECT campaign.name, campaign.status, campaign.bidding_strategy_type,
       campaign_budget.amount_micros, campaign_budget.explicitly_shared,
       metrics.cost_micros, metrics.conversions, metrics.cost_per_conversion,
       metrics.search_budget_lost_impression_share,
       metrics.search_rank_lost_impression_share
FROM campaign
WHERE segments.date DURING LAST_7_DAYS AND campaign.status = 'ENABLED'
ORDER BY metrics.cost_micros DESC
```

## Output
```
PLANO DE ORÇAMENTO — {data}
Campanha | Orçamento atual | Proposto | Var. | CPA 7d | Perda orç. | Motivo
...
Total diário: R$X → R$X
```
