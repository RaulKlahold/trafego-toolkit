---
name: investigate-campaign
description: Diagnóstico aprofundado de uma campanha (Google ou Meta) — causa raiz com evidências, ação recomendada e impacto esperado. Triggers on "investiga campanha", "diagnóstico", "por que o CPA subiu", "campanha sem resultado", "o que aconteceu com".
argument-hint: "[nome da campanha]"
---

# /investigate-campaign — Diagnóstico de campanha
Carregar `account-conventions` e `performance-analysis`.
Somente leitura.

## Quando usar
Performance inesperada (boa ou ruim), antes de escalar, CPA piorou sem motivo aparente,
campanha nova sem resultado.

## Workflow
1. Perguntar a campanha (e a plataforma, se não for óbvio).
2. Google — puxar 30d: campanha, grupos, palavras-chave (com Índice de qualidade),
   termos de pesquisa, anúncios, dispositivos, horários, histórico de alterações recentes.
   Meta — campanha, conjuntos, anúncios, quebra por idade/gênero/posicionamento/dispositivo.
3. Comparar o período bom com o ruim para achar **quando** mudou.
4. Rodar o checklist abaixo e ficar com a causa que os dados sustentam.

## Consultas (Google API)
```sql
-- Grupos
SELECT ad_group.name, metrics.clicks, metrics.conversions, metrics.cost_micros, metrics.average_cpc
FROM ad_group WHERE campaign.id = $ID AND segments.date DURING LAST_30_DAYS

-- Palavras-chave
SELECT ad_group_criterion.keyword.text, ad_group_criterion.keyword.match_type,
       ad_group_criterion.quality_info.quality_score,
       metrics.clicks, metrics.conversions, metrics.cost_micros
FROM keyword_view WHERE campaign.id = $ID AND segments.date DURING LAST_30_DAYS
ORDER BY metrics.cost_micros DESC

-- Termos de pesquisa
SELECT search_term_view.search_term, metrics.clicks, metrics.conversions, metrics.cost_micros
FROM search_term_view WHERE campaign.id = $ID AND segments.date DURING LAST_30_DAYS
ORDER BY metrics.cost_micros DESC LIMIT 100
```

## Checklist
**CPA piorou**
- [ ] Rastreamento de conversão mudou ou quebrou? (checar primeiro)
- [ ] Alguma alteração na conta na data da piora (lance, orçamento, anúncio, público)?
- [ ] Leilão mais caro? (CPC/CPM subindo, concorrente novo)
- [ ] Criativo/anúncio fatigado? (Meta: frequência alta, CTR caindo)
- [ ] Público saturado? (alcance caindo)
- [ ] Landing page mudou, ficou lenta ou fora do ar? (CTR estável, conversão caiu)
- [ ] Sazonalidade ou dia da semana?
- [ ] Termos de pesquisa novos e irrelevantes? (Google)

**CPA melhorou de repente**
- [ ] Qual grupo/conjunto/anúncio puxou? Qual público/termo? → replicar

**Não entrega**
- [ ] Anúncios reprovados ou limitados? Público pequeno demais? Lance baixo? Índice de qualidade baixo?

## Output
- Causa raiz (uma frase)
- Evidências (os números que sustentam)
- Ação recomendada
- Impacto esperado e como medir em 7 dias
