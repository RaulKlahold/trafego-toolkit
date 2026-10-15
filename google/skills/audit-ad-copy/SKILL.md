---
name: audit-ad-copy
description: Auditoria da copy dos anúncios ativos (Google RSA e, se pedido, Meta) com nota 0–10, problemas e sugestões de substituição. Triggers on "audita copy", "analisa anúncios", "revisão de anúncios", "copy fraca", "nota dos anúncios".
---

# /audit-ad-copy — Auditoria de copy
Carregar `account-conventions` e `ad-copy-principles`.
Somente leitura.

## Quando usar
CTR caindo, copy sem renovação há 30+ dias, antes de criar variações, revisão de qualidade.

## Google Ads (RSA)
1. Puxar os RSAs ativos (texto dos recursos, Força do anúncio, desempenho por recurso se houver,
   CTR, conversões).
2. Para cada anúncio, checar:
   - 3+ títulos com palavra-chave? 3+ com proposta de valor? 2+ com CTA? 2+ com diferencial?
   - Conceitos repetidos? Erros de português (grave)? Limites de caracteres?
   - Recursos com desempenho "Baixo" a substituir? Fixações em excesso?
3. Nota 0–10 por anúncio e lista de melhorias específicas.

## Meta Ads (se o usuário pedir e houver dados)
Por anúncio ativo: gancho na 1ª linha, proposta de valor clara, CTA, ângulo coerente com o
público do conjunto, frequência acima do limite, CTR (link) < 1%.

## Output
- Nota por anúncio (0–10) e nota geral (A–F)
- Top 3 melhores e 3 piores, com o motivo
- Problemas encontrados
- Textos sugeridos para substituir (já com contagem de caracteres)
- Prioridade: urgente / pode esperar / ok
