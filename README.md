# Dinheiro e Desempenho no Brasileirão 2026

Análise da relação entre o que os clubes da Série A gastam (contratações e folha salarial), o que recebem de patrocínio de casas de apostas e o que entregam em campo.

O projeto ganhou um contexto extra com a **MP 1.394/2026**, de 25/09/2026, que proíbe as bets no Brasil e obriga a retirada das marcas até 05/10. Os notebooks 03 e 04 medem o quanto cada clube dependia desse dinheiro.

> Dados atualizados até a **28ª rodada** (26/09/2026). Valores em R$ milhões.

---

## Perguntas

| Notebook | Pergunta |
|---|---|
| `01_pontos_por_investimento` | Quantos pontos cada clube somou por milhão gasto em contratações? |
| `02_pontos_por_folha` | Quantos pontos cada clube somou por real pago em salários? |
| `03_bets_x_gastos` | Quanto dos gastos de cada clube o patrocínio de bet cobria? |
| `04_patrocinio_por_ponto` | Quanto dinheiro de bet estava associado a cada ponto conquistado? |

## Principais resultados

![Cobertura das bets](graficos/03a_cobertura_bets.png)

- A folha salarial acompanha bem o desempenho (correlação de 0,70 com pontos por jogo). Os maiores desvios são o **Athletico-PR** (muito acima da tendência com folha baixa) e o **Corinthians** (muito abaixo com a 3ª maior folha).
- A **Chapecoense** é o clube mais exposto à proibição das bets: o patrocínio da Zeroum Bet equivale a cerca de **51% da folha**, seguida por Vitória (41%) e Flamengo (39%).
- O **Corinthians** tinha cerca de **R$ 3,5 milhões de patrocínio de bet por ponto conquistado**, o maior valor da Série A.

![Folha x pontos](graficos/02a_folha_x_pontos.png)

---

## Como rodar

1. Abra o [Google Colab](https://colab.research.google.com) e faça upload de `notebooks/00_dados.ipynb`.
2. Rode todas as células e autorize o acesso ao Google Drive. O notebook cria a pasta `MeuDrive/analise_futebol/` com o arquivo `dados/clubes_2026.csv`.
3. Rode qualquer um dos notebooks 01 a 04. Gráficos e tabelas são salvos em `graficos/` e `tabelas/`.

Os notebooks também funcionam fora do Colab (Jupyter local), criando a pasta `analise_futebol/` no diretório atual. Bibliotecas: `pandas`, `numpy`, `matplotlib`.

## Estrutura

```
├── notebooks/   00_dados + 4 análises
├── dados/       clubes_2026.csv (base única lida por todos os notebooks)
├── graficos/    PNGs gerados
└── tabelas/     CSVs com os resultados de cada análise
```

---

## Metodologia e fontes

A transparência sobre a origem de cada número é parte central do projeto. A coluna `metodo_folha` do CSV indica de onde veio cada valor, e os gráficos usam cores diferentes para cada método.

### Classificação
Tabela após a 28ª rodada (26/09/2026). Como alguns clubes têm jogos a menos, as comparações usam **pontos por jogo**.

### Contratações
Valores de transferência **divulgados pela imprensa** nas duas janelas de 2026. Clubes com contratações sem valor divulgado estão marcados como `transf_parcial = sim`: o gasto real deles é maior.
- **Chapecoense:** 1ª janela obtida no balancete oficial do 1º trimestre (R$ 1,25 mi em direitos econômicos + R$ 2,8 mi em taxas de empréstimo).

### Folha salarial
Base principal: estimativa mensal de folha dos 20 clubes, usando o **ponto médio** das faixas. Para anualizar, multiplica-se por **13** (12 salários + 13º), mesma regra usada na origem dos números do topo da tabela. Nas métricas por ponto, usa-se a folha **acumulada até agora** (mensal × 9 meses), para comparar com os pontos também acumulados.

| Método | Clubes | Observação |
|---|---|---|
| Balanço ÷ 13 (Lance!) | Flamengo, Palmeiras, Corinthians, Fluminense, São Paulo, Atlético-MG, Santos, Botafogo, Vasco | Custo anual com salários, imagem e bonificações publicado pelo Lance! em 26/09/2026 |
| Apuração jornalística | Cruzeiro | R$ 35 mi/mês segundo Jorge Nicola (ago/2026); o clube não confirma |
| Balancete oficial | Chapecoense | Salários + encargos + direito de imagem do 1º tri/2026 ≈ R$ 2,25 mi/mês. **Luvas** (R$ 8 mi no trimestre) ficaram fora por não serem recorrentes |
| Derivado de orçamento | Coritiba | Orçamento do futebol 2026 de até R$ 170 mi × ~64% (peso típico de pessoal) ÷ 13 ≈ R$ 8 a 9 mi/mês |
| Julgamento do analista | Bragantino | Faixa de R$ 6,4 a 9 mi/mês, sem fonte oficial localizada. Contraponto: os custos totais do futebol em 2025 (R$ 427,8 mi, Sports Value) sugerem que o valor real pode ser maior |
| Estimativa de plataforma | Demais clubes | Estimativas de mercado, com maior incerteza |

### Patrocínio de bets
- Valores do **Lance! (26/09/2026)** para os clubes com bet.
- **Chapecoense:** R$ 3,75 mi de receita da Zeroum Bet no balancete do 1º trimestre × 4 ≈ R$ 15 mi/ano (supõe pagamento linear).
- **Grêmio:** patrocinador de bet sem valor informado, fica fora das análises 03 e 04.
- **Sem bet** (segundo o Metrópoles, 25/09/2026): Athletico-PR, Bahia, Bragantino, Coritiba, Internacional e Mirassol.
- Os valores de patrocínio não são necessariamente destinados a salários; as comparações servem para dimensionar o peso dos contratos.

### Documentos oficiais
- Chapecoense: Balancete e Orçamento do 1º trimestre de 2026, com parecer do Conselho Fiscal, disponíveis no site do clube.

## Limitações

- Folhas salariais de clubes brasileiros raramente são divulgadas mensalmente; a maioria dos valores é estimativa, com metodologias diferentes entre fontes.
- Valores de transferência divulgados pela imprensa podem incluir ou não bônus, comissões e parcelas futuras.
- Os balanços oficiais de 2026 só serão publicados em 2027. Quando saírem, os números devem ser substituídos.
- A MP 1.394/2026 ainda precisa ser analisada pelo Congresso, e o impacto real depende das renegociações de cada contrato.



---

**Autor:** Enrique Froes Nepomuceno · [LinkedIn](https://www.linkedin.com/in/enrique-froes-nepomuceno) · Projeto de estudo em análise de futebol e finanças.
