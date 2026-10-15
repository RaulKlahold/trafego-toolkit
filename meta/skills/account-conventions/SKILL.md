---
name: account-conventions
description: Carrega a ficha CONFIG-CONTAS.md (contas, metas, produtos, nomenclatura) e as regras de segurança da operação Meta Ads. Carregar SEMPRE antes de qualquer outra skill deste plugin. Triggers on "qual conta", "nomenclatura", "prefixos", "minhas metas", "configuração".
user-invocable: false
---

# Convenções da conta e regras de operação — Meta Ads

## 1. Carregar a ficha da conta
Procurar, nesta ordem, e usar a primeira encontrada:
1. `CONFIG-CONTAS.md` na pasta de trabalho atual (ficha do cliente)
2. `~/.claude/ads-toolkit/CONFIG-CONTAS.md` (ficha padrão)

Dela tirar: Ad Account ID, Page ID, moeda, objetivo, métrica principal, metas por produto/público,
limites de segurança, propostas de valor, público, tom, nomenclatura e concorrentes.

Se não houver ficha, ou um campo necessário estiver `PREENCHER`:
- Perguntar ao usuário só o que for necessário para a tarefa atual (ex.: meta de CPL).
- Nunca inventar ID de conta, meta ou proposta de valor.
- Ao final, oferecer salvar as respostas na ficha.

Se não houver meta definida, a análise ainda pode rodar usando a **média da própria conta**
como referência — deixar isso explícito no relatório.

## 2. Métrica principal
- Objetivo `leads` → **CPL** = spend / leads
- Objetivo `vendas` → **CPA** = spend / compras e **ROAS** = receita / spend
- Objetivo `ambos` → reportar por campanha conforme o evento de otimização dela
Nos textos das skills, "CPR" (custo por resultado) significa a métrica principal acima.

## 3. Fontes de dados (nesta ordem)
1. **Conector Meta Ads (MCP)**, se estiver disponível na sessão.
2. **Arquivo exportado** do Gerenciador de Anúncios (CSV/XLSX) que o usuário indicar.
3. Se nenhum dos dois: pedir o export, explicando o que exportar:
   - Nível: campanha, conjunto de anúncios ou anúncio (conforme a tarefa)
   - Colunas: nome, status, valor usado, resultados, custo por resultado, impressões, alcance,
     frequência, cliques no link, CTR (link), CPM, orçamento
   - Detalhamento por dia (para tendência) e o período pedido pela skill

Valores vêm na moeda da conta. Se a conta não for BRL, perguntar a cotação a usar — não chutar.

## 4. Regras de segurança (absolutas)
- **Nunca** pausar, ativar, editar orçamento, lance, público ou criativo sem o usuário
  confirmar explicitamente aquela ação específica, naquela hora.
- Toda skill que muda algo roda em **modo simulação** por padrão: mostra o plano e para.
- Sempre mostrar os dados antes da recomendação.
- Mínimo de dados: ver "Limites de segurança" da ficha (padrão: 3 dias para pausar, 7 para escalar).
- Não mexer em conjuntos na **fase de aprendizado**, exceto pela Regra 3x (ver performance-analysis).
- Registrar toda ação executada em `./logs/acoes-meta.log` (data, objeto, antes → depois, motivo).

## 5. Nomenclatura
Usar a seção "Nomenclatura das campanhas" da ficha para interpretar nomes.
Se não houver, inferir pelo nome (ex.: "RMKT", "Remarketing", "LAL", "Frio", "CBO", "ABO") e
dizer no relatório quais suposições foram feitas.
