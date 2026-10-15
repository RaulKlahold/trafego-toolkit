---
name: performance-analysis
description: Metodologia padrão de análise de performance Google Ads (métricas, sinais de alerta, Regra 3x, Smart Bidding, Índice de qualidade). Carregada pelas skills de análise e otimização. Triggers on "analisa performance", "métricas", "CPA", "CPC", "CTR", "Índice de qualidade", "parcela de impressões".
user-invocable: false
---

# Metodologia de análise — Google Ads
Carregar `account-conventions` antes.

## Métricas prioritárias (nesta ordem)
1. **CPA** (ou CPL / ROAS, conforme a ficha)
2. **Taxa de conversão** = conversões / cliques
3. **CPC médio**
4. **CTR**
5. **Índice de qualidade** (1–10) nas palavras-chave com mais custo
6. **Parcela de impressões** e perda por orçamento vs. por classificação

## Referências genéricas (Rede de Pesquisa)
Use só sem meta na ficha e sem histórico. Variam muito por nicho e região.
- CTR: > 5% bom | < 2% ruim
- Taxa de conversão: > 3% bom | < 1% indica problema de landing page ou intenção
- Índice de qualidade < 6: anúncio, relevância ou página fracos
- Smart Bidding (CPA/ROAS desejado) funciona melhor com ~15–30+ conversões/mês na campanha

## Fluxo de análise
1. Puxar 7d e 30d (ou o período pedido)
2. Converter micros se vier da API
3. Calcular métricas por campanha
4. Comparar 7d vs 30d e 7d vs 7d anterior
5. Aplicar sinais de alerta e quality gates
6. Cruzar melhor CPA vs maior custo
7. Fechar com ranking e recomendações priorizadas

## Sinais de alerta
- CPC subindo > 30% semana a semana → leilão mais caro ou Índice de qualidade caindo
- Conversões caindo com o mesmo custo → página, oferta ou rastreamento de conversão
- Conversões zeradas de repente em várias campanhas → checar tag/rastreamento antes de tudo
- Parcela de impressões perdida por orçamento alta + CPA bom → oportunidade de escala
- Perda por classificação alta → lance ou qualidade
- Campanha ativa com zero impressões → reprovação, segmentação ou lance

## Quality gates
### Regra 3x
CPA > 3x a meta com custo ≥ 3x a meta → recomendar pausa/revisão imediata, sem esperar os dias
mínimos. Continua sendo recomendação: executa só com confirmação.

### Smart Bidding e correspondência
- Não recomendar correspondência ampla sem Smart Bidding ativo.
- Abaixo de ~15 conversões/mês: preferir Maximizar cliques ou CPC manual, ou consolidar campanhas.
- Mudanças de orçamento de no máximo ~20% por vez em campanhas com Smart Bidding.

### Atribuição e conversões
Não comparar períodos com modelos de atribuição ou ações de conversão primárias diferentes.

### Compliance
Se a ficha marcar categoria sensível (finanças, saúde etc.), lembrar de certificações/restrições
e evitar promessas de resultado na copy.

## Nota A–F (para auditorias)
A 90–100 excelente | B 75–89 bom | C 60–74 atenção | D 40–59 ruim | F < 40 crítico
