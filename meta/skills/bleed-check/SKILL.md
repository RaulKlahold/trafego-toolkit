---
name: bleed-check
description: Detecta conjuntos de anúncios Meta "sangrando" (gastando sem resultado) numa janela recente e propõe pausas — só pausa com confirmação. Triggers on "tá sangrando", "gastando sem lead", "gastando sem venda", "verifica sangramento", "o que está perdendo dinheiro".
argument-hint: "[--threshold-spend 50] [--window-hours 6]"
---

# /bleed-check — Detector de sangria
Carregar `account-conventions` e `performance-analysis`.

**Modo padrão: simulação.** Esta skill identifica e recomenda. Não pausa nada sozinha.

## Parâmetros
- `--threshold-spend`: gasto mínimo sem resultado para considerar sangria
  (padrão: valor da ficha, ou R$50)
- `--window-hours` (padrão 6): janela recente. Com CSV, usar o menor período disponível (ex.: hoje).
- `--threshold-results` (padrão 0)

## Workflow
1. Listar conjuntos ativos e os dados da janela: gasto, resultados, impressões, cliques, CPR.
2. Sangrando = gasto > threshold-spend **e** resultados ≤ threshold-results.
3. Para cada um, checar antes de recomendar:
   - Está em fase de aprendizado? → só recomendar pausa se a Regra 3x se aplicar;
     senão, marcar "observar".
   - Tem histórico bom (7d) e só um dia ruim? → marcar "observar", não pausar.
   - É remarketing com público pequeno? → considerar frequência antes de concluir.
4. Montar a lista: PAUSAR (recomendado) / OBSERVAR, com motivo.
5. Perguntar: "Quer que eu pause os conjuntos marcados como PAUSAR?"
   - Só pausar os que o usuário confirmar, um a um ou em lote nomeado.
   - Só pausar **conjuntos** — nunca a campanha inteira.
   - Sem conector com permissão de escrita: entregar a lista para pausar manualmente.
6. Registrar o que foi pausado em `./logs/acoes-meta.log`.

## Output
```
BLEED CHECK — {data hora} — janela {N}h

PAUSAR (recomendado)
- [Conjunto] — campanha [X] — gasto R$XX, 0 resultados — motivo: ...
OBSERVAR
- [Conjunto] — gasto R$XX, 0 resultados — em aprendizado / histórico bom

Total gasto sem resultado na janela: R$XX
```
