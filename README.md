# 📊 Operação Tanque Cheio — Análise de Preços de Combustíveis

Projeto desenvolvido em **Power BI** com foco em análise exploratória, modelagem dimensional e geração de insights estratégicos sobre preços de combustíveis no Brasil.

---

## 🎯 Objetivo

Analisar o comportamento dos preços de combustíveis no país e responder questões estratégicas:

- Preço médio da gasolina comum por estado no último mês  
- Quantidade de revendas acima da média nacional  
- Bandeira com menor preço médio por combustível  
- Diferença percentual entre maior e menor preço do diesel por estado  
- Tendência de preços ao longo do tempo  
- Estado com maior preço médio da gasolina comum  
- Total de amostras analisadas  
- Período do mês com maiores preços  

---

## 🛠 Stack Utilizada

- **Power BI**
- **Power Query (ETL)**
- **DAX**
- **Modelagem Dimensional (Star Schema)**

---

## 🔄 ETL — Power Query

Principais etapas de transformação:

- Padronização de tipos de dados (datas e valores monetários)
- Remoção de duplicidades
- Tratamento de valores nulos
- Criação de colunas derivadas (Ano, Mês, Dia)
- Classificação do período do mês (Início, Meio, Fim)
- Padronização de nomes de combustíveis
- Ajustes para otimização de performance no modelo

---

## 🧠 Modelagem de Dados

Modelo dimensional estruturado em estrela.

### 🔹 Tabela Fato

**fPrecos**
- Data  
- IdRevenda  
- IdProduto  
- IdEstado  
- IdBandeira  
- PrecoVenda  
- Amostras  

### 🔹 Tabelas Dimensão

- **dRevenda**
- **dProdutos**
- **dEstados**
- **dBandeiras**

Relacionamentos 1:N das dimensões para `fPrecos`, com filtro unidirecional para manter consistência e desempenho.

---

## 📐 Principais Métricas (DAX)

### Preço Médio

```DAX
Preco Medio = AVERAGE(fPrecos[PrecoVenda])
```

### Preço Médio Nacional

```DAX
Preco Medio Nacional =
CALCULATE(
    [Preco Medio],
    ALL(dEstados)
)
```

### Revendas Acima da Média Nacional

```DAX
Revendas Acima Media =
CALCULATE(
    DISTINCTCOUNT(dRevenda[Revenda]),
    FILTER(
        fPrecos,
        fPrecos[PrecoVenda] > [Preco Medio Nacional]
    )
)
```

### Diferença Percentual — Diesel

```DAX
Dif Percentual Diesel =
VAR PrecoMax = MAX(fPrecos[PrecoVenda])
VAR PrecoMin = MIN(fPrecos[PrecoVenda])
RETURN
DIVIDE(PrecoMax - PrecoMin, PrecoMin)
```

Funções utilizadas: `CALCULATE`, `FILTER`, `ALL`, `DISTINCTCOUNT`, `VAR`, `DIVIDE`.

---

## 📊 Estrutura do Dashboard

Baseado no relatório final desenvolvido:

### 🔹 Visão Executiva
- KPI: Revendas acima da média (4.185)
- KPI: Total de amostras (421 mil)
- Preço médio da gasolina por estado (último mês)

### 🔹 Análise por Bandeira
- Ranking de preço médio
- Identificação da bandeira mais competitiva

### 🔹 Análise por Estado
- Preço máximo e mínimo
- Diferença percentual do diesel
- Comparativo entre estados

### 🔹 Análise Temporal
- Média geral por dia
- Linha de tendência
- Avaliação do comportamento ao longo do mês

---

## 📈 Principais Insights

- Diferenças percentuais superiores a 40% no diesel entre estados.
- Concentração relevante de revendas operando acima da média nacional.
- Tendência de aumento de preços ao longo do mês.
- Estados com pressão sistemática de preços acima da média.
- Bandeiras com posicionamento mais competitivo por combustível.

---

## 🚀 Conclusão

O projeto demonstra:

- Aplicação prática de ETL com Power Query  
- Modelagem dimensional consistente  
- Desenvolvimento de métricas analíticas em DAX  
- Transformação de dados públicos em inteligência de mercado  

Foco não apenas na visualização, mas na geração de insight acionável para tomada de decisão.
