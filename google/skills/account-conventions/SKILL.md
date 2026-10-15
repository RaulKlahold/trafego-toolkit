---
name: account-conventions
description: Carrega a ficha CONFIG-CONTAS.md (contas, metas, produtos, nomenclatura) e as regras de segurança da operação Google Ads. Carregar SEMPRE antes de qualquer outra skill deste plugin. Triggers on "qual conta", "nomenclatura", "prefixos", "minhas metas", "configuração".
user-invocable: false
---

# Convenções da conta e regras de operação — Google Ads

## 1. Carregar a ficha da conta
Procurar, nesta ordem, e usar a primeira encontrada:
1. `CONFIG-CONTAS.md` na pasta de trabalho atual (ficha do cliente)
2. `~/.claude/ads-toolkit/CONFIG-CONTAS.md` (ficha padrão)

Dela tirar: Customer ID (e MCC), moeda, objetivo, métrica principal, metas por produto/público,
limites de segurança, propostas de valor, público, tom, nomenclatura e concorrentes.

Se não houver ficha, ou um campo necessário estiver `PREENCHER`:
- Perguntar ao usuário só o que for necessário para a tarefa atual.
- Nunca inventar Customer ID, meta ou proposta de valor.
- Ao final, oferecer salvar as respostas na ficha.

Sem meta definida, usar a **média da própria conta** como referência e dizer isso no relatório.

## 2. Métrica principal
- Objetivo `leads` → **CPL** = custo / conversões de lead
- Objetivo `vendas` → **CPA** = custo / conversões de compra e **ROAS** = valor de conversão / custo
- Nos textos das skills, "CPA" significa a métrica principal acima.
- Conferir quais ações de conversão estão como **primárias**: conversão no Google nem sempre
  é lead qualificado ou venda. Se houver dúvida, perguntar.

## 3. Fontes de dados (nesta ordem)
1. **Conector Google Ads (MCP)**, se estiver disponível. A API retorna custo em **micros**
   (÷ 1.000.000 = valor na moeda da conta).
2. **Relatório exportado** da interface do Google Ads (CSV/XLSX) que o usuário indicar
   (valores já vêm na moeda, sem micros).
3. Se nenhum dos dois: pedir o export, dizendo qual relatório (Campanhas, Palavras-chave,
   Termos de pesquisa, Anúncios), o período e as colunas: custo, cliques, impressões, CTR,
   CPC médio, conversões, custo/conv., valor conv., parcela de impressões, Índice de qualidade.

## 4. Regras de segurança (absolutas)
- **Nunca** pausar, ativar, editar orçamento, lance, palavra-chave, negativa ou anúncio sem
  o usuário confirmar explicitamente aquela ação específica, naquela hora.
- Toda skill que muda algo roda em **modo simulação** por padrão: mostra o plano e para.
- Sempre mostrar os dados antes da recomendação.
- Mínimo de dados: ver "Limites de segurança" da ficha (padrão: 3 dias para pausar, 7 para escalar).
- Campanha com Smart Bidding em aprendizado (após mudança relevante): evitar novas mudanças
  por ~1–2 semanas, exceto pela Regra 3x.
- Registrar toda ação executada em `./logs/acoes-google.log` (data, objeto, antes → depois, motivo).

## 5. Nomenclatura
Usar a seção "Nomenclatura das campanhas" da ficha. Se não houver, inferir pelo nome
(ex.: "Search", "PMax", "Marca", "Institucional", "RMKT") e dizer quais suposições foram feitas.
