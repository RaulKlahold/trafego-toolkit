---
name: meta-performance
description: Panorama de performance da conta Meta Ads — CPR, CTR, frequência, CPM e alertas por campanha, com ranking e recomendações. Triggers on "como está o Meta", "panorama Meta Ads", "performance do Facebook", "resumo das campanhas Meta".
argument-hint: "[período, ex.: 7d | 14d | 30d]"
---

# /meta-performance — Panorama Meta Ads
Carregar `account-conventions` e `performance-analysis`.

## Workflow
1. Período: o do argumento, ou 7d + 30d por padrão.
2. Puxar dados por campanha (e por conjunto, se houver poucas campanhas) — fonte conforme
   account-conventions (conector ou CSV).
3. Para cada campanha ativa: gasto, resultados, CPR, CTR (link), frequência, CPM, taxa de conversão.
4. Comparar 7d vs 30d → tendência.
5. Aplicar sinais de alerta e quality gates de `performance-analysis`.
6. Ranquear do melhor para o pior CPR.
7. Fechar com no máximo 5 recomendações priorizadas. Nenhuma é executada aqui.

## Output
```
PANORAMA META ADS — {conta} — {período}
Gasto: R$X | Resultados: N | CPR médio: R$X (meta: R$X) | ROAS: X (se vendas)

Campanha            | Gasto  | Res. | CPR   | CTR  | Freq | Tendência 7d vs 30d
...

ALERTAS
- ...

RECOMENDAÇÕES (por prioridade)
1. ... — motivo: ... — impacto esperado: ...
```
