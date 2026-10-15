---
name: search-term-methodology
description: Critérios para avaliar termos de pesquisa do Google Ads por relevância ao tema da campanha (não só "zero conversão = ruim"). Carregada por mine-search-terms e weekly-review. Triggers on "termos de pesquisa", "search terms", "palavras negativas", "gasto desperdiçado".
user-invocable: false
---

# Metodologia de termos de pesquisa
O objetivo não é só "zero conversão = negativar": é **relevância ao tema da campanha**.

## Abordagem
1. Olhar só termos ainda sem ação (não adicionados como palavra-chave nem negativos).
2. Ordenar por custo (onde o dinheiro está indo).
3. Cruzar sempre três coisas: o **termo**, a **palavra-chave** que o ativou e o
   **tema da campanha/grupo** (pelo nome e pela nomenclatura da ficha).
   Pergunta-chave: o termo combina com o tema e com a oferta?

## Classificação
- **NEGAR (claro)**: fora do tema, busca de emprego/vaga, curso/"como fazer" quando a campanha
  é de conversão, "grátis"/"gratuito" quando o produto é pago, produto diferente,
  concorrente (a menos que a ficha diga que você faz campanha de concorrente).
- **NEGAR (provável)**: relacionado mas público errado; intenção só informativa; termo amplo demais.
- **MANTER**: no tema e com intenção de compra, mesmo sem conversão, se tiver < 5 cliques
  (dados insuficientes), ou se for termo de marca/produto.
- **ADICIONAR_KEYWORD**: converte e ainda não tem palavra-chave exata; variação de marca não capturada.

## Tabela de decisão
| Situação | Ação |
|---|---|
| Fora do tema, qualquer custo | NEGAR |
| Intenção errada + custo > R$10 | NEGAR |
| No tema, 0 conv., < 5 cliques | MANTER (pouco dado) |
| No tema, 0 conv., > 20 cliques | MANTER + investigar landing page/oferta |
| Converte e não é exata | ADICIONAR_KEYWORD (exata) |
| Variação de marca não capturada | ADICIONAR_KEYWORD (exata) |

## Nível e tipo da negativa
- Sugerir em que nível negativar: lista compartilhada (termos de toda a conta, ex.: "vagas"),
  campanha ou grupo de anúncios.
- Sugerir correspondência da negativa: exata para termos específicos; frase para padrões
  ("como fazer", "grátis"). Cuidado para não bloquear termos bons por uma negativa ampla.

## Consulta (API)
```sql
SELECT search_term_view.search_term, search_term_view.status,
       metrics.clicks, metrics.impressions, metrics.conversions,
       metrics.cost_micros, campaign.name, ad_group.name
FROM search_term_view
WHERE segments.date DURING LAST_30_DAYS
  AND search_term_view.status = 'NONE'
  AND metrics.clicks >= 1
ORDER BY metrics.cost_micros DESC
LIMIT 2000
```
Sem API: pedir o relatório "Termos de pesquisa" dos últimos 30 dias.
Campanhas Performance Max mostram só categorias de busca, sem termo a termo.
