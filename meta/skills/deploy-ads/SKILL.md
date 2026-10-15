---
name: deploy-ads
description: Cria campanhas Meta Ads em massa a partir de um manifest JSON — sempre valida antes e cria tudo PAUSADO. Exige conector Meta com permissão de escrita. Triggers on "cria campanhas em massa", "sobe campanhas do manifest", "deploy de anúncios".
argument-hint: "--manifest caminho.json [--validar]"
---

# /deploy-ads — Criação em massa (sempre pausado)
Carregar `account-conventions`.

## Regras
- Passo 1 é **sempre** validar e mostrar o resumo. Só cria depois do usuário confirmar.
- Tudo é criado com status **PAUSADO**. Ativar é sempre manual, no Gerenciador.
- Exige conector Meta com escrita. Sem ele: validar o manifest e gerar uma planilha
  para importação em massa no Gerenciador (Exportar/Importar anúncios).
- ID da conta e Page ID vêm da ficha. Se o manifest tiver outra conta, parar e perguntar.

## Formato do manifest
```json
{
  "campanha": "Nome da campanha",
  "objetivo": "OUTCOME_LEADS",
  "categoria_especial": [],
  "conjuntos": [
    {
      "nome": "Nome do conjunto",
      "orcamento_diario_brl": 50,
      "segmentacao": {
        "geo_locations": { "countries": ["BR"] },
        "age_min": 25,
        "age_max": 55
      },
      "otimizacao": "LEAD_GENERATION",
      "anuncios": [
        {
          "nome": "Nome do anúncio",
          "imagem": "./criativos/arquivo.jpg",
          "titulo": "Título",
          "texto": "Texto principal",
          "cta": "LEARN_MORE",
          "link": "https://seusite.com.br"
        }
      ]
    }
  ]
}
```
Objetivos válidos (ODAX): OUTCOME_LEADS, OUTCOME_SALES, OUTCOME_TRAFFIC,
OUTCOME_ENGAGEMENT, OUTCOME_AWARENESS, OUTCOME_APP_PROMOTION.

## Workflow
1. **Validar**: campos obrigatórios, arquivos de imagem existem, orçamento ≥ mínimo da ficha,
   copy contra `ad-copy-principles`, conta/página conferem com a ficha.
   Mostrar resumo (N campanhas, N conjuntos, N anúncios, orçamento diário total) e perguntar.
2. Após "sim": subir imagens → criar campanha → conjuntos → criativos → anúncios, todos PAUSADOS.
   Erro 429: esperar 60s e tentar de novo. Erro 400: registrar, pular o item, continuar.
   Erro 5xx: tentar até 3x.
3. Relatório em `./relatorios/deploy-AAAA-MM-DD-HHmm.md` e registro em `./logs/acoes-meta.log`.

## Output
```
DEPLOY — {data} — conta {id} — tudo PAUSADO
Campanha: [ID] [nome] | Conjuntos: N | Anúncios: N | Erros: N
Revise e ative manualmente no Gerenciador de Anúncios.
```
