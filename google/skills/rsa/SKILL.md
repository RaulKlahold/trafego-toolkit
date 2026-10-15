---
name: rsa
description: Cria ou renova copy de anúncio responsivo de pesquisa (RSA) — 15 títulos e 4 descrições com contagem de caracteres validada e CSV pronto para importar. Triggers on "cria RSA", "copy Google Ads", "títulos para anúncio de pesquisa", "renova anúncio".
argument-hint: "[produto] [palavra-chave principal] [ângulo]"
---

# /rsa — Copy de RSA
Carregar `account-conventions` e `ad-copy-principles`.

## Workflow
1. Confirmar: produto/oferta, campanha/grupo, palavra-chave principal e ângulo
   (prova social, urgência real, técnico, dor). Usar a ficha; perguntar só o que faltar.
2. Se houver dados: puxar os anúncios atuais do grupo e os recursos com melhor desempenho,
   para não repetir o que já existe e manter o que funciona.
3. Gerar 15 títulos (≤ 30) e 4 descrições (≤ 90) seguindo a composição de `ad-copy-principles`,
   mais 2 caminhos de URL (≤ 15).
4. **Validar caracteres** de cada linha e mostrar a contagem ao lado.
5. Revisar conceitos repetidos e erros de português.
6. Oferecer CSV para importação (Google Ads Editor):
   `campanha, grupo, titulo_1..titulo_15, descricao_1..descricao_4, caminho_1, caminho_2, url_final`

## Output
```
RSA — [produto] — palavra-chave: [..]
TÍTULOS
1. Texto (28) — [keyword]
2. Texto (24) — [proposta de valor]
...
DESCRIÇÕES
1. Texto (87)
...
Caminhos: /xxx /yyy
```
