---
name: rebalance
description: Monta um plano de realocação de orçamento entre conjuntos Meta Ads (ABO) com base no CPR — tira dos piores, dá aos melhores, com limites de segurança. Só executa com confirmação. Triggers on "redistribui budget", "realoca orçamento", "tira verba de X e põe em Y", "orçamento dos melhores conjuntos".
argument-hint: "[--lookback 7] [--max-shift-pct 20] [--min-spend 100]"
---

# /rebalance — Realocação de orçamento
Carregar `account-conventions` e `performance-analysis`.

**Modo padrão: simulação.** Mostra o plano e para.

## Parâmetros
- `--lookback` (padrão 7 dias)
- `--max-shift-pct` (padrão: escala máxima da ficha, ou 20%)
- `--min-spend` (padrão R$100 no período)
- Orçamento mínimo por conjunto: o da ficha (padrão R$30/dia)

## Workflow
1. Puxar conjuntos ativos com orçamento diário, gasto, resultados e CPR do período.
   Ignorar gasto < min-spend.
2. Referências: CPR médio da conta = soma(gasto) / soma(resultados) e meta da ficha.
3. Classificar:
   - **RUIM**: CPR > meta (ou > 1,15x a média, sem meta)
   - **TOP**: CPR < 0,7x a média e ≤ meta
   - **MÉDIO**: o resto (não mexe)
4. Calcular:
   - RUIM perde até max-shift-pct do orçamento, sem ficar abaixo do mínimo
   - A verba liberada vai para os TOP, proporcional ao CPR (melhor recebe mais),
     nenhum subindo mais que max-shift-pct
   - Orçamento total não muda
5. Bloqueios — não mexer em:
   - conjuntos em fase de aprendizado
   - campanhas CBO (orçamento é da campanha; sugerir mudança na campanha, à parte)
   - conjuntos alterados nos últimos 7 dias (ver `./logs/acoes-meta.log`)
6. Apresentar a tabela e perguntar se quer aplicar. Sem conector com escrita,
   entregar a tabela para aplicar manualmente.
7. Após confirmação: aplicar, registrar no log.

## Output
```
PLANO DE REBALANCE — {data} — {lookback}d
CPR médio da conta: R$X | Meta: R$X

Conjunto   | Orçamento atual | Proposto | Variação | CPR    | Classe
...

Verba realocada: R$X/dia | Melhora estimada no CPR médio: ~X% (estimativa, não garantia)
Bloqueados: [conjunto] — motivo
```
