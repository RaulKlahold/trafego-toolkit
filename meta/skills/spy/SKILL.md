---
name: spy
description: Inteligência competitiva pela Biblioteca de Anúncios da Meta — classifica os anúncios ativos dos concorrentes por gancho, oferta, ângulo e tempo no ar, e sugere ângulos não explorados. Triggers on "o que o concorrente está anunciando", "espia concorrente", "anúncios da concorrência", "biblioteca de anúncios".
argument-hint: "--competitors \"marca1, marca2\""
---

# /spy — Inteligência competitiva
Carregar `account-conventions` e `ad-copy-principles`.

## Importante sobre a fonte
A API da Biblioteca de Anúncios (`ads_archive`) só retorna anúncios **comerciais** veiculados
na União Europeia; para o Brasil ela retorna apenas anúncios políticos/sociais.
Por isso esta skill usa o **site** da Biblioteca:
`https://www.facebook.com/ads/library/?active_status=active&ad_type=all&country=BR&q={marca}`

## Parâmetros
- `--competitors`: marcas/páginas (padrão: lista de concorrentes da ficha)

## Workflow
1. Para cada concorrente, abrir a Biblioteca de Anúncios:
   - Se houver navegador disponível na sessão, abrir a URL acima e ler os anúncios ativos.
   - Se não, mandar ao usuário os links e pedir que cole os textos ou envie prints.
2. Para cada anúncio, registrar:
   - **Gancho** (1ª linha / título) e **CTA**
   - **Tipo de oferta**: desconto, teste grátis, prova social, problema-solução, demo, urgência
   - **Ângulo / consciência**: problema, solução, produto, marca, remarketing
   - **Tempo no ar** (data de início): novo (0–7d), testando (8–30d), **vencedor (30d+)**
   - Formato (imagem, vídeo, carrossel) e número de variações do mesmo criativo
3. Comparar com a última análise em `./relatorios/spy-ultimo.md`, se existir → novos e parados.
4. Tendências: ângulos usados por 2+ concorrentes.
5. Recomendar 3–5 ângulos para testar que os concorrentes **não** estão explorando,
   coerentes com as propostas de valor da ficha.

## Output
`./relatorios/spy-AAAA-MM-DD.md` (e cópia como `spy-ultimo.md`):
- Resumo (concorrentes, anúncios ativos, novos, parados)
- Tabela: Página | Gancho | CTA | Oferta | Ângulo | Formato | Tempo no ar
- Tendências e ângulos recomendados
