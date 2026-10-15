---
name: hooks
description: Gera muitas variações de gancho e copy a partir de um hook vencedor usando frameworks (PAS, BAB, AIDA, pattern interrupt, social proof, curiosidade), exportando CSV. Triggers on "gera variações", "variações de hook", "50 variações de anúncio", "PAS", "BAB", "AIDA".
argument-hint: "--seed \"hook semente\" --audience \"público\" [--count 30] [--frameworks PAS,BAB,AIDA]"
---

# /hooks — Motor de variações de copy
Carregar `account-conventions` e `ad-copy-principles`.

## Parâmetros
- `--seed` (obrigatório): hook ou ângulo vencedor
- `--audience`: público (se omitido, usar o da ficha)
- `--count` (padrão 30)
- `--frameworks` (padrão PAS,BAB,AIDA): também pattern-interrupt, social-proof, curiosity-gap, medo

## Frameworks
- **PAS** — Problema → Agitar → Solução
- **BAB** — Antes → Depois → Ponte (o produto)
- **AIDA** — Atenção → Interesse → Desejo → Ação
- **Pattern interrupt** — abrir quebrando o padrão ("Para.", número inesperado, pergunta direta)
- **Social proof** — abrir com resultado de cliente ou volume real (só provas da ficha)
- **Curiosity gap** — "O que ninguém te conta sobre…", "Por que [crença comum] está errada"
- **Medo** — custo realista de não agir, sem exagero

## Workflow
1. Ler seed, público e dores da ficha.
2. Distribuir `--count` entre os frameworks.
3. Variar em cada uma: intensidade, especificidade, ponto de vista (você/eu/eles), gatilho
   (dor / aspiração / curiosidade / prova).
4. Cada variação: texto principal (≤125 caracteres), título (≤40), descrição (≤30).
5. Validar contagem de caracteres e proibições.
6. Etiquetar: framework, registro emocional, funil (TOPO/MEIO/FUNDO), posicionamento sugerido.

## Output
CSV em `./criativos/hooks-AAAA-MM-DD.csv` com colunas:
`nome, texto_principal, titulo, descricao, framework, registro, funil, posicionamento`

Resumo: total, divisão por framework e top 3 para testar primeiro.
Sugestão de teste: 5–10 hooks em ABO por 3–4 dias, com orçamento que permita
pelo menos ~1 resultado por dia por conjunto, antes de escalar o vencedor.
