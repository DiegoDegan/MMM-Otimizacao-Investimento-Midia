# Estratégia e Roadmap para a Versão 2 (MMM V2)

Este documento servirá como um guia estratégico para a criação da **Versão 2** do nosso Marketing Mix Modeling (MMM). O objetivo central desta nova iteração é solucionar os gargalos estatísticos descobertos na V1 e implementar as melhores práticas recomendadas pela indústria.

---

## Limitações Encontradas na V1 (O Que Precisamos Corrigir)

1. **Retornos Constantes (Infinitos):** A Regressão Linear Simples assumiu que cada $1 investido sempre geraria o mesmo retorno. Na vida real, existe o limite de Saturação de Mercado (Retornos Decrescentes).
2. **Resíduos Não-Normais:** O Teste de Shapiro-Wilk comprovou que os erros do modelo não seguem uma curva normal perfeita. Isso distorce os p-valores e o Teste-t, tirando o rigor absoluto da atribuição de cada canal.
3. **Falta de Dimensão Temporal:** O dataset V1 era "transversal" (amostras sem uma ordem cronológica exata), impossibilitando a medição do "efeito memória" que uma propaganda tem nas cabeças dos consumidores ao longo das semanas.

---

## Plano de Ação: O Que Implementar na V2

Abaixo estão os 5 pilares fundamentais para transformar este projeto e elevá-lo a um nível altamente profissional:

### Passo 1: Aquisição de Dados Temporais (Time-Series)
- **Ação:** Buscar (ou adaptar) um dataset onde cada linha represente um período de tempo (ex: Semanas ou Dias).
- **Por que:** Para podermos mapear tendências, sazonalidades (Black Friday, Natal) e, principalmente, calcular o quanto um comercial de TV veiculado hoje continua gerando vendas nas semanas seguintes.

### Passo 2: Engenharia de Variáveis (Adstock & Saturação)
A maior mudança técnica será aplicar transformações nas variáveis de investimento ($) ANTES de enviá-las ao modelo:
- **Curva de Adstock (Efeito Memória):** Aplicar uma taxa de decaimento (ex: distribuição Weibull ou Exponencial). Se passou na TV segunda-feira, ainda gera 50% do impacto na terça, 25% na quarta, etc.
- **Transformação de Saturação (Retornos Decrescentes):** Aplicar transformações Logarítmicas (Log) ou a função de *Hill* aos orçamentos reais. Isso vai ensinar o modelo matematicamente que gastar o dobro não significa vender o dobro.

### Passo 3: Avaliação Rígida de Multicolinearidade (VIF)
- **Ação:** Rodar testes de VIF (*Variance Inflation Factor*) em todas as colunas de mídia no dataset.
- **Por que:** Certificar-nos matemática de que dois canais de mídia não estão tão correlacionados que forcem o modelo a roubar mérito de um para entregar ao outro.

### Passo 4: Evolução do Algoritmo de Regressão
Substituir o `sklearn.linear_model.LinearRegression` por algoritmos que lidam nativamente com penalização ou incerteza:
- **Opção A (Regressão Robusta):** `Ridge` ou `Lasso`. Algoritmos que penalizam canais pouco eficientes (jogando o coeficiente deles muito perto de zero, perfeito para o caso do *Jornal/Newspaper*).
- **Opção B (Padrão Ouro - Inferência Bayesiana):** Mudar para o ecossistema `PyMC` na linguagem Python e adotar uma abordagem probabilística (Bayesiana) para as métricas, permitindo colocar um "limite de saturação realista" para cada canal de maneira probabilística.

### Passo 5: Otimização Científica do Budget (What-If V2)
- **Ação:** Em vez de pegar a verba de um canal e dividir de forma aritmética com outros (50/50), usaremos a biblioteca `Scipy.Optimize`.
- **Por que:** Criaremos uma função matemática de "Otimizador Não-Linear" para achar o "pico ótimo matemático" da curva de investimento. Ele vai mastigar a Saturação e cuspir exatamente a quantia (R$) que devemos colocar em TV e Rádio sem desperdiçar um único centavo.

---

## Stack Tecnológica Atualizada (Estimada para V2)
- Engenharia e Exploração: `Pandas`, `NumPy`
- Visualização de Dados e Curvas: `Seaborn`, `Matplotlib`
- Machine Learning Clássico: `Scikit-Learn` (Ridge/Lasso)
- **(Novo)** Matemática e Otimização: `SciPy` (Optimize e Stats)
- **(Novo)** Modelagem Bayesiana: `PyMC` ou bibliotecas open-source específicas (ex: *LightweightMMM* do Google ou *Robyn* da Meta)
