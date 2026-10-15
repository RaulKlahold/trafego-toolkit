---
name: weekly-review
description: Revisão semanal completa do Google Ads — semana vs semana anterior, orçamento, termos de pesquisa e qualidade dos anúncios, em um relatório com prioridades. Triggers on "revisão semanal", "weekly review", "como foi a semana", "relatório semanal".
---

# /weekly-review — Revisão semanal Google Ads
Carregar `account-conventions`, `performance-analysis` e `search-term-methodology`.
Ideal toda segunda-feira. Somente leitura: recomendações ficam para o usuário aprovar.

## Workflow
1. **Semana vs semana anterior** por campanha: custo, conversões, CPA, CPC, CTR — com variação %.
2. **Orçamento**: campanhas com perda por orçamento e CPA bom (escalar) vs CPA ruim há 3+ dias
   (cortar) — seguir a lógica de `budget-optimize`, sem executar.
3. **Termos de pesquisa**: versão rápida — só termos com custo > R$20 e 0 conversão na semana,
   classificados pela metodologia.
4. **Anúncios**: anúncios reprovados/limitados, Força do anúncio "Baixa", Índice de qualidade < 6
   nas palavras-chave com mais custo.
5. **Rastreamento**: conversões zeradas ou com queda brusca → alertar primeiro.

## Output
```
REVISÃO SEMANAL GOOGLE ADS — {semana}

RESUMO: Custo R$X (±X%) | Conv. N (±X%) | CPA R$X (±X%) vs meta R$X

POR CAMPANHA
[Campanha]: N conv | CPA R$X | CPC R$X | (±X% vs semana anterior)

ALERTAS: ...
DESTAQUES: ...
NEGATIVAS SUGERIDAS: N termos (R$X gastos) — lista
RECOMENDAÇÕES
1. [mais urgente] — motivo
2. ...
3. ...
```
No primeiro dia útil do mês, incluir também o fechamento do mês anterior.
