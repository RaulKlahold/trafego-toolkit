---
name: copy-meta
description: Cria copy para anúncios Meta Ads (3 variações A/B/C por ângulo) baseada nas propostas de valor da ficha e nos criativos que mais performaram. Triggers on "cria copy", "copy para Meta", "texto para anúncio", "copy para o Facebook/Instagram".
argument-hint: "[produto] [público] [ângulo]"
---

# /copy-meta — Copy para Meta Ads
Carregar `account-conventions` e `ad-copy-principles`.

## Workflow
1. Confirmar: produto/oferta, público (frio ou remarketing) e ângulo preferido.
   Pegar o que já estiver na ficha; perguntar só o que faltar.
2. Se houver dados (conector ou CSV de anúncios dos últimos 14–30 dias), identificar os
   3 anúncios com melhor CPR e o ângulo deles.
3. Gerar 3 variações (A/B/C), cada uma com:
   - Texto principal (gancho na 1ª linha, 2–4 linhas)
   - Título (até ~40 caracteres)
   - Descrição curta
   - CTA sugerido (botão)
   - Ângulo e nível de consciência a que se destina
4. Revisar contra as proibições de `ad-copy-principles` antes de entregar.
5. Indicar qual testar primeiro e por quê (histórico da conta > suposição).
