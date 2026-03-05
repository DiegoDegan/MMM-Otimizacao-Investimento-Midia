# Marketing Mix Modeling (MMM): Otimização de Investimento em Mídia

“Se aumentarmos 10% o investimento em cada canal, qual deles traz o maior retorno em vendas?”

Projeto de Marketing Mix Modeling (MMM) usando dados públicos de investimento em TV, Rádio e Jornal para estimar seu impacto nas vendas e recomendar a melhor alocação de orçamento para maximizar o ROI.



## Objetivo do projeto
Medir quanto cada canal de mídia contribui para as vendas.
Construir um modelo estatístico simples (regressão linear multivariada) que relacione investimento em mídia e vendas.
Simular cenários de aumento de investimento (+10% por canal) para apoiar decisões de budget.



## Contexto de negócio

Uma empresa fictícia investe regularmente em três canais de mídia:
- TV Ad Budget
- Radio Ad Budget
- Newspaper Ad Budget

Cada observação representa um período, com os respectivos investimentos e o resultado em Sales ($).

O foco do projeto é responder:
- Qual canal tem maior impacto marginal nas vendas?
- Faz sentido reduzir investimento em algum canal?
- Em qual canal devemos priorizar um aumento de 10% no budget?



## Dados

Fonte: Advertising Sales Dataset – Kaggle
Arquivo utilizado: Advertising-Budget-and-Sales.csv

Principais colunas:
- TV Ad Budget ($) – investimento em TV ($1k)
- Radio Ad Budget ($) – investimento em Rádio ($1k)
- Newspaper Ad Budget ($) – investimento em Jornal ($1k)
- Sales ($) – vendas/receita ($1M)
