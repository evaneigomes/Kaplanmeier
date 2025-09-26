---

## MVP – Ciência de Dados: Análise de Sobrevivência de Incidentes de Violação de Dados

**Discente:** *\[[Evanei Gomes dos Santos e Caroline Nazare Dos Santos Chucre Kappel]*
**Data:** *\[26/09/2025]*

---

## 1. Definição do Problema

O objetivo deste projeto é desenvolver um **Mínimo Produto Viável (MVP)** para a análise de **recorrência de incidentes de violação de dados** em diferentes tipos de organizações, utilizando o método **Kaplan-Meier**, da estatística de sobrevivência.

A tarefa consiste em estimar a **probabilidade de uma organização permanecer sem novos incidentes** após um primeiro evento, permitindo compreender padrões de reincidência e auxiliar na tomada de decisões sobre **políticas de segurança da informação e priorização de recursos**.

### Hipótese

Organizações de diferentes setores apresentam **padrões distintos de reincidência de incidentes** de violação de dados ao longo do tempo.
Acredita-se que setores como Saúde ou Governo possam ter curvas de sobrevivência mais íngremes (maior risco de novas violações) em comparação a outros setores.

---

## 2. Dataset

* **Fonte:** Data Breach Chronology Dataset
* **Atributos Principais:**

  * `breach_date`: data do incidente
  * `organization_type`: categoria da organização (Saúde, Governo, Setor Financeiro etc.)
  * `breach_type`: tipo de violação (Hacking, Malware, Phishing etc.)
* **Período Analisado:** de 2010 a 2023
* O dataset foi filtrado para incluir **somente organizações com pelo menos 10 incidentes**, garantindo relevância estatística das curvas.

---

## 3. Configuração do Ambiente

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from lifelines import KaplanMeierFitter
from google.colab import files
```

* **pandas**: leitura e manipulação de dados
* **numpy**: operações numéricas auxiliares
* **matplotlib**: visualização gráfica
* **lifelines**: modelagem de sobrevivência (Kaplan-Meier)
* **google.colab.files**: upload de arquivos no Colab

> **Observação:** Instalação da biblioteca `lifelines` no Colab:

```bash
!pip install lifelines
```

---

## 4. Preparação dos Dados

Nesta etapa, realizamos as operações de carga, limpeza e transformação dos dados para análise temporal.

### Operações Realizadas

1. **Carga do Dataset:** upload manual do arquivo Excel no ambiente do Colab.
2. **Ajuste de Datas:** tratamento de formatos incompletos (ano, ano-mês) para `datetime`.
3. **Filtragem por Período:** mantidos apenas registros de 2010 a 2023.
4. **Definição do Índice:** a coluna `breach_date` foi definida como índice temporal do DataFrame.
5. **Criação da Série Temporal:** uso de `resample('M')` para gerar frequência mensal de incidentes.

---

## 5. Modelagem e Análise

A abordagem escolhida foi a **Análise de Sobrevivência com Kaplan-Meier**, que estima a probabilidade cumulativa de não ocorrência de novos incidentes ao longo do tempo.

### Operações

1. **Agrupamento por Organização:** contagem de incidentes por `organization_type`.
2. **Filtragem de Grupos:** mantidos apenas grupos com ≥10 incidentes.
3. **Cálculo de Intervalos:** obtido o tempo (em dias) desde a última violação usando `diff().dt.days`.
4. **Ajuste do Modelo:** aplicado `KaplanMeierFitter` para cada grupo, gerando uma curva de sobrevivência individual.
5. **Visualização:** plotagem das curvas para comparar os padrões entre os setores.

---

## 6. Resultados Obtidos

* Foram geradas **curvas de sobrevivência** para cada tipo de organização.
* O eixo **X** mostra os dias desde a última violação (limite configurável, ex.: 0–500 dias).
* O eixo **Y** indica a **probabilidade de não ocorrência de novo incidente**.
* Organizações com curvas que decaem mais rápido apresentam maior risco de reincidência em curtos períodos.

---

## 7. Visualizações

* **Gráfico Kaplan-Meier:** compara a evolução da probabilidade de sobrevivência (sem novos incidentes) entre os tipos de organização.
* Configurações:

  * Curvas coloridas por setor
  * Legenda posicionada externamente
  * Grade e limites de eixos ajustados

---

## 8. Conclusões e Considerações Finais

Este MVP demonstrou como a **Análise de Sobrevivência** pode revelar **padrões temporais de recorrência** de incidentes de segurança em diferentes setores, permitindo priorizar medidas preventivas e otimizar recursos de cibersegurança.

### Principais Resultados

* **Identificação de Setores Críticos:** setores com maior probabilidade de novas violações em períodos curtos.
* **Insights Temporais:** compreensão do intervalo médio entre incidentes.

### Próximos Passos

* Aplicar **Modelos de Risco Proporcional de Cox** para incluir mais variáveis explicativas (ex.: tipo de violação).
* Investigar fatores de risco específicos por setor.
* Atualizar os dados periodicamente e monitorar tendências.

---

## 9. Desenvolvido por

* **Autor:** *\[Seu Nome ou Equipe]*
* **MVP:** Análise de Sobrevivência com Kaplan-Meier
* **Data de Conclusão:** *\[Data do Projeto]*

---

Quer que eu inclua no README **uma imagem do gráfico gerado** (por exemplo, usando um screenshot) para deixar a documentação mais visual?
