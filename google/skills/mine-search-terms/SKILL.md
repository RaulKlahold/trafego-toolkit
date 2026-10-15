---
name: mine-search-terms
description: Minera termos de pesquisa do Google Ads e gera CSV com o que negativar, manter ou adicionar como palavra-chave, priorizado por custo. Só aplica negativas com confirmação. Triggers on "analisa termos de pesquisa", "quais palavras negativar", "search terms", "negativação", "mineração de keywords".
argument-hint: "[período, padrão 30d] [campanha]"
---

# /mine-search-terms — Mineração de termos de pesquisa
Carregar `account-conventions` e `search-term-methodology`.

## Workflow
1. Puxar termos do período (padrão 30 dias), sem ação, com ≥ 1 clique, ordenados por custo —
   consulta em `search-term-methodology`, ou relatório exportado.
2. Para cada termo, cruzar termo + palavra-chave + tema da campanha/grupo.
3. Classificar: NEGAR / MANTER / ADICIONAR_KEYWORD, com justificativa curta.
4. Para NEGAR: sugerir nível (lista compartilhada / campanha / grupo) e correspondência
   (exata / frase). Agrupar padrões repetidos numa única negativa de frase quando seguro.
5. Para ADICIONAR_KEYWORD: sugerir grupo e correspondência.
6. Priorizar pelos de maior custo sem conversão.
7. Perguntar se quer aplicar as negativas. Sem conector com escrita, o CSV serve para
   colar no Google Ads Editor ou na interface.

## Output
CSV `negativas-AAAA-MM-DD.csv`:
`termo, acao, justificativa, nivel_sugerido, correspondencia, campanha, grupo, custo, cliques, conversoes`

Resumo: X para negar (R$X gastos) | Y oportunidades de palavra-chave | Z mantidos.
