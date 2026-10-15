---
name: audience-audit
description: Auditoria da arquitetura de públicos do Meta Ads — mapa do funil, sobreposições entre conjuntos e exclusões faltando, com arquitetura recomendada. Triggers on "analisa públicos", "sobreposição de públicos", "públicos se sobrepondo", "lookalike", "exclusões faltando", "público canibalizando".
argument-hint: "[--include-inactive]"
---

# /audience-audit — Auditoria de públicos
Carregar `account-conventions` e `performance-analysis`.
Somente leitura: esta skill não altera nada.

## Dados necessários
- Conector: públicos personalizados, lookalikes e o targeting de cada conjunto ativo.
- Sem conector: pedir ao usuário a lista de conjuntos ativos com públicos incluídos/excluídos
  (print ou texto) e a lista de públicos da aba "Públicos" (nome, tipo, tamanho).

## Workflow
1. Categorizar públicos: lista de clientes, site (pixel), engajamento, vídeo, lookalike,
   interesses, aberto (broad / Advantage+).
2. Mapear cada conjunto no funil:
   - **TOPO (frio)**: broad, interesses, LAL 3–10%
   - **MEIO**: visitantes 30–180d, vídeo 25–75%, engajamento, LAL 1–2%
   - **FUNDO**: página de produto, checkout iniciado, carrinho abandonado
   - **RETENÇÃO**: clientes / compradores
3. Sobreposição: conjuntos ativos ao mesmo tempo, mesma região, mesmo evento de otimização,
   públicos logicamente sobrepostos e sem exclusão mútua → risco ALTO / MÉDIO / BAIXO.
4. Exclusões faltando (por impacto):
   - ALTO: clientes/leads atuais não excluídos da prospecção
   - MÉDIO: públicos quentes não excluídos do topo
   - BAIXO: sobreposição menor de interesses/LAL
5. Recomendar arquitetura: públicos por camada, regras de exclusão e sementes para LAL.
   Se a conta usa Advantage+ / broad, considerar que sobreposição pesa menos e focar em
   exclusão de clientes.

## Output
```
AUDITORIA DE PÚBLICOS — {data}
FUNIL ATUAL: [mapa em texto]
SOBREPOSIÇÕES: ALTO: ... | MÉDIO: ...
EXCLUSÕES FALTANDO: ...
ARQUITETURA RECOMENDADA: TOPO / MEIO / FUNDO — incluir / excluir
```
