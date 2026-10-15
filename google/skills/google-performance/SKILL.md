---
name: google-performance
description: Panorama de performance Google Ads — CPA, conversões, CPC, CTR, parcela de impressões por campanha, com alertas, ranking e recomendações. Triggers on "como está o Google", "panorama Google Ads", "performance do Google", "resumo das campanhas Google".
argument-hint: "[período, ex.: 7d | 30d]"
---

# /google-performance — Panorama Google Ads
Carregar `account-conventions` e `performance-analysis`.

## Workflow
1. Período do argumento, ou 7d + 30d por padrão. Conta: a da ficha (se houver várias, perguntar
   ou rodar todas).
2. Puxar por campanha: custo, cliques, impressões, CTR, CPC médio, conversões, custo/conv.,
   valor conv., parcela de impressões, perda por orçamento e por classificação.
3. Comparar 7d vs 30d.
4. Aplicar alertas e quality gates.
5. Ranquear por CPA (ou ROAS).
6. Fechar com no máximo 5 recomendações priorizadas. Nada é executado aqui.

## Consulta (API)
```sql
SELECT campaign.name, campaign.status, campaign.advertising_channel_type,
       campaign.bidding_strategy_type, metrics.cost_micros, metrics.clicks,
       metrics.impressions, metrics.ctr, metrics.average_cpc, metrics.conversions,
       metrics.cost_per_conversion, metrics.conversions_value,
       metrics.search_impression_share, metrics.search_budget_lost_impression_share,
       metrics.search_rank_lost_impression_share
FROM campaign
WHERE segments.date DURING LAST_30_DAYS AND campaign.status = 'ENABLED'
ORDER BY metrics.cost_micros DESC
```

## Output
```
PANORAMA GOOGLE ADS — {conta} — {período}
Custo: R$X | Conv.: N | CPA: R$X (meta R$X) | ROAS: X

Campanha | Tipo | Custo | Conv. | CPA | CPC | CTR | Parcela impr. | Perda orç./class.
...
ALERTAS: ...
RECOMENDAÇÕES: 1. ... — motivo — impacto esperado
```
