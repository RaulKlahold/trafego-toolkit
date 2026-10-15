---
name: fatigue-scan
description: Monitora fadiga criativa no Meta Ads comparando semana a semana (frequência, CTR, CPR, CPM) e gera briefs de substituição para os criativos em risco. Triggers on "criativo fatigado", "frequência alta", "CTR caindo", "criativo cansado", "hora de trocar criativo".
argument-hint: "[--lookback 14] [--min-spend 100]"
---

# /fatigue-scan — Monitor de fadiga criativa
Carregar `account-conventions`, `performance-analysis` e `ad-copy-principles`.

## Parâmetros
- `--lookback` (padrão 14 dias, dividido em 2 semanas)
- `--min-spend` (padrão R$100 no período): abaixo disso, dados insuficientes
- Limite de frequência: o da ficha (padrão 2,5 frio / 5,0 remarketing)

## Workflow
1. Puxar dados por anúncio, por dia, do período (conector ou CSV com detalhamento diário).
2. Para cada anúncio com gasto ≥ min-spend: semana 1 vs semana 2 de CTR, CPR, CPM e frequência.
3. Classificar:
   - **ALTO RISCO** (trocar agora): frequência acima do limite, OU CTR caiu > 20%,
     OU CPR subiu > 30%, OU CPM subiu > 30%
   - **MÉDIO** (observar): frequência a até 0,5 do limite, OU CTR caiu 10–20%, OU CPR subiu 15–30%
   - **SAUDÁVEL**: estável ou melhorando
4. Para cada ALTO RISCO, escrever um brief de substituição: ângulo, gancho e visual originais;
   o que manter (o ângulo que funcionou) e o que mudar; 3 ganchos novos.

## Output
```
FATIGUE SCAN — {data} — {lookback} dias
Saudáveis: N | Médio: N | Alto risco: N

ALTO RISCO
[Anúncio]
- Frequência X.X (limite X.X) | CTR X% → X% | CPR R$X → R$X
- Brief: manter ângulo [..], trocar [..]. Ganchos: 1) .. 2) .. 3) ..
```
