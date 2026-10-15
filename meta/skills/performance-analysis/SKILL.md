---
name: performance-analysis
description: Metodologia padrão de análise de performance Meta Ads (métricas, sinais de alerta, quality gates como Regra 3x, fase de aprendizado e suficiência de orçamento). Carregada pelas skills de análise e otimização. Triggers on "analisa performance", "métricas", "CPL", "CPA", "ROAS", "CTR", "frequência".
user-invocable: false
---

# Metodologia de análise — Meta Ads
Carregar `account-conventions` antes (metas, limites, métrica principal).

## Métricas prioritárias (nesta ordem)
1. **CPR** — métrica principal da ficha (CPL, ou CPA + ROAS)
2. **CTR (link)** = cliques no link / impressões
3. **Frequência** = impressões / alcance
4. **CPM** = custo por mil impressões (pressão de leilão)
5. **Taxa de conversão** = resultados / cliques no link (qualidade da landing page / oferta)

## Referências genéricas
Use só quando a ficha não tiver meta e a conta não tiver histórico. Variam muito por nicho —
sempre preferir o histórico da própria conta.
- CTR (link): > 1,5% bom | < 0,5% ruim
- Taxa de conversão da LP: < 1% indica problema de página ou oferta
- Frequência: ver limites da ficha (padrão 2,5 frio / 5,0 remarketing)
- Vida útil típica de criativo: 3–4 semanas em frio, 6–7 semanas em remarketing

## Fluxo de análise
1. Puxar dados de 7d e 30d (ou o período pedido)
2. Calcular as métricas acima por campanha / conjunto
3. Comparar 7d vs 30d e 7d vs 7d anterior → melhorando ou piorando?
4. Aplicar sinais de alerta e quality gates
5. Cruzar: quem tem o melhor CPR vs quem leva mais verba
6. Fechar com ranking e recomendações priorizadas (o que fazer primeiro e por quê)

## Sinais de alerta
- CPR > 1,5x a meta por 2 dias seguidos → sugerir revisão/pausa
- Gasto ≥ 2x a meta sem nenhum resultado → alertar
- Frequência acima do limite da ficha → trocar criativo
- CTR < 0,5% → problema de criativo ou público
- Taxa de conversão < 1% → problema de landing page ou oferta
- CPM subindo > 30% semana a semana → leilão mais caro ou público saturando
- Orçamento acabando (campanha vai parar sozinha)

## Quality gates
### Regra 3x
Conjunto/campanha com CPR > 3x a meta, com gasto ≥ 3x a meta → recomendar pausa imediata,
mesmo na fase de aprendizado e mesmo sem os dias mínimos de dados.
Ex.: meta CPL R$40 → CPL acima de R$120 com R$120+ gastos.
Continua sendo **recomendação**: só executa com confirmação do usuário.

### Fase de aprendizado (< ~50 resultados na semana do conjunto)
Não pausar, não mudar orçamento > 20%, não trocar criativo nem público — exceto Regra 3x.

### Suficiência de orçamento
O ideal é o conjunto (ABO) ou a campanha (CBO) gastar por dia algo próximo de **5x o CPR alvo**
para o algoritmo aprender. Bem abaixo disso: recomendar consolidar conjuntos ou aumentar verba,
em vez de concluir que "o público não funciona".

### Atribuição
Padrão Meta: 7 dias clique / 1 dia visualização. Não comparar períodos ou campanhas com janelas
de atribuição diferentes.

### Compliance
Se a ficha marcar categoria especial (crédito, emprego, moradia, política), lembrar das
restrições de segmentação e evitar promessa de resultado financeiro na copy.

## Nota A–F (para auditorias)
A 90–100 excelente | B 75–89 bom | C 60–74 atenção | D 40–59 ruim | F < 40 crítico
