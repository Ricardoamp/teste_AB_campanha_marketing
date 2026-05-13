# Teste A/B para Campanha de Marketing Digital

## 📌 Sobre o Projeto

Este projeto apresenta uma análise estatística completa de um experimento de **Teste A/B** realizado em campanhas de Marketing Digital.

A empresa responsável pela campanha realizou anúncios de um produto digital em diferentes regiões geográficas e desejava entender se existia diferença significativa na taxa de conversão entre os grupos analisados.

O projeto foi desenvolvido utilizando Python e técnicas de análise estatística para:

* Explorar os dados;
* Visualizar o comportamento dos grupos;
* Validar hipóteses estatísticas;
* Escolher o teste estatístico adequado;
* Interpretar os resultados;
* Gerar conclusões baseadas em evidências.

---

# 🎯 Objetivo

Avaliar se existe diferença estatisticamente significativa na taxa de conversão entre os grupos A e B da campanha de marketing.

A análise busca responder à seguinte pergunta:

> A região geográfica dos usuários influencia a conversão da campanha?

---

# 🛠️ Tecnologias Utilizadas

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* SciPy
* Jupyter Notebook

---

# 📂 Estrutura do Projeto

```bash
├── data/
│   └── dataset.csv
├── teste_ab.ipynb
└── README.md
```

---

# 📥 Carregamento dos Dados

Os dados foram carregados a partir de um arquivo CSV contendo informações sobre:

* Grupo do experimento (A ou B);
* Conversão dos usuários;
* Latitude;
* Longitude;
* Informações geográficas relacionadas à campanha.

Exemplo do carregamento:

```python
import pandas as pd

df = pd.read_csv('./data/dataset.csv')
```

---

# 🧹 Etapa 1 — Limpeza de Dados

Nesta etapa foi criada uma cópia do dataset original para garantir a integridade dos dados durante o processo de análise.

```python
df1 = df.copy()
```

A separação em etapas facilita:

* Organização do projeto;
* Reprodutibilidade;
* Segurança durante transformações;
* Clareza no fluxo analítico.

---

# 🔍 Etapa 2 — Exploração dos Dados

Foi realizada uma análise exploratória para compreender:

* Estrutura do dataset;
* Quantidade de linhas e colunas;
* Primeiros registros;
* Distribuição dos grupos.

Principais funções utilizadas:

```python
shape()
head()
```

Essa etapa é fundamental para entender:

* Possíveis inconsistências;
* Distribuição dos dados;
* Características do experimento.

---

# 📈 Etapa 3 — Visualização dos Dados

Foi construída uma visualização geográfica dos grupos A e B utilizando latitude e longitude.

## Objetivo da Visualização

Identificar visualmente:

* Distribuição geográfica dos grupos;
* Possíveis padrões regionais;
* Concentração de usuários;
* Diferenças entre os grupos.

## Gráfico Utilizado

```python
plt.scatter()
```

Os grupos foram representados por cores diferentes:

* Azul → Grupo A
* Vermelho → Grupo B

Essa etapa auxilia na interpretação visual antes da modelagem estatística.

---

# 🧠 Etapa 4 — Modelagem Estatística

A modelagem estatística foi utilizada para validar se as diferenças observadas entre os grupos possuem significância estatística.

---

## 4.1 Taxa Média de Conversão

Foi calculada a média de conversão para cada grupo.

```python
taxa_conversao = df4.groupby('grupo')['conversao'].mean()
```

Também foi realizada a separação dos grupos:

```python
grupo_A = df4[df4['grupo']=='A']
grupo_B = df4[df4['grupo']=='B']
```

O objetivo foi comparar:

* Taxa média de conversão do Grupo A;
* Taxa média de conversão do Grupo B.

---

# 🧪 Escolha do Teste Estatístico

Antes de aplicar qualquer teste estatístico, foi necessário validar as suposições dos testes paramétricos.

---

## 4.2.1 Teste t de Student

Inicialmente foi considerada a utilização do Teste t de Student.

Esse teste exige:

* Distribuição normal dos dados;
* Homogeneidade das variâncias.

Por isso, foram realizados testes de validação dessas suposições.

---

## ✅ Teste de Normalidade — Shapiro-Wilk

Foi aplicado o teste de Shapiro-Wilk para verificar se os dados seguiam distribuição normal.

```python
stats.shapiro()
```

### Hipóteses

* H0: Os dados são normalmente distribuídos;
* H1: Os dados não são normalmente distribuídos.

### Resultado

Os valores de p foram menores que 0.05 para ambos os grupos.

Portanto:

✅ Rejeitamos a hipótese nula.

Conclusão:

> Os dados dos grupos A e B não seguem distribuição normal.

---

## ✅ Teste de Homogeneidade das Variâncias — Levene

Foi utilizado o teste de Levene para verificar se as variâncias dos grupos eram homogêneas.

```python
stats.levene()
```

### Hipóteses

* H0: As variâncias são iguais;
* H1: As variâncias são diferentes.

### Resultado

O valor-p foi maior que 0.05.

Conclusão:

✅ Não rejeitamos a hipótese nula.

Isso indica que:

> As variâncias dos grupos podem ser consideradas homogêneas.

---

# 📌 Resumo das Validações Estatísticas

| Validação                    | Resultado      |
| ---------------------------- | -------------- |
| Normalidade                  | ❌ Não atendida |
| Homogeneidade das variâncias | ✅ Atendida     |

Como os dados não possuem distribuição normal, o Teste t de Student não é o mais adequado.

---

# 🔬 Teste Estatístico Escolhido

## 4.2.2 Teste de Mann-Whitney U

Devido à ausência de normalidade nos dados, foi utilizado o teste não paramétrico de Mann-Whitney U.

```python
stats.mannwhitneyu()
```

Esse teste é apropriado para:

* Comparar dois grupos independentes;
* Dados sem distribuição normal;
* Avaliar diferenças entre distribuições.

---

## Hipóteses do Teste

* H0: Não existe diferença significativa entre os grupos;
* H1: Existe diferença significativa entre os grupos.

---

# 📊 Resultado do Teste

Após a execução do teste:

```python
if p_val_mw < alpha:
    print("Rejeitamos a hipótese nula")
else:
    print("Não rejeitamos a hipótese nula")
```

O resultado indicou que:

✅ Não há diferença estatisticamente significativa entre os grupos A e B.

---

# ✅ Conclusão Final

Com base em toda a análise estatística realizada, não foram encontradas evidências suficientes para afirmar que existe diferença significativa na taxa de conversão entre os grupos analisados.

## Conclusão do Projeto

> A região geográfica dos usuários não apresentou influência significativa na taxa de conversão da campanha de marketing.

---
