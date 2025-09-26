Aqui está um **README** bem estruturado para o código do arquivo **Kaplan-Meier.ipynb**, inspirado no estilo do exemplo do MVP dos vinhos que você compartilhou:

---

# Análise de Sobrevivência – Kaplan-Meier por Tipo de Organização

**Discente:** *\[Seu Nome ou da Equipe]*
**Data:** *\[Data do projeto]*

---

## 1. Definição do Problema

O objetivo deste projeto é aplicar técnicas de **Análise de Sobrevivência**, por meio do estimador **Kaplan-Meier**, para investigar o comportamento temporal de **incidentes de violação de dados** registrados em diferentes **tipos de organizações**.

A principal questão que buscamos responder é:

> *“Qual é a probabilidade de uma organização permanecer sem novas violações após um incidente inicial, e como isso varia entre os diferentes tipos de organização?”*

Essa análise é relevante para compreender padrões de recorrência de incidentes, apoiando estratégias de mitigação de riscos e políticas de segurança da informação.

---

## 2. Dataset

* **Fonte:** *Data Breach Chronology Dataset* (KaplanMeyer)
* **Principais Atributos Usados:**

  * `Date Breach` – Data de ocorrência do incidente
  * `organization_type` – Categoria da organização (saúde, governo, setor financeiro etc.)
* **Pré-requisitos:**

  * A coluna de data deve estar no formato **datetime** para permitir cálculos temporais.
  * A base foi filtrada para incluir **apenas organizações com ≥ 10 incidentes**, garantindo relevância estatística nas curvas.

---

## 3. Metodologia

### 3.1. Preparação dos Dados

* Conversão da coluna **Date Breach** para o tipo `datetime`.
* Definição da data como **índice do DataFrame**, possibilitando calcular intervalos entre incidentes.
* Cálculo da variável derivada `days_since_last`, representando os dias transcorridos desde o incidente anterior.

### 3.2. Modelo Utilizado

Foi aplicado o **Kaplan-Meier Fitter** (biblioteca [lifelines](https://lifelines.readthedocs.io/)) para estimar a **função de sobrevivência**, que mostra a probabilidade de não ocorrer um novo incidente ao longo do tempo.

---

## 4. Implementação – Principais Bibliotecas

```python
import pandas as pd
import matplotlib.pyplot as plt
from lifelines import KaplanMeierFitter
```

* **pandas:** manipulação e filtragem do dataset.
* **matplotlib:** criação de gráficos.
* **lifelines:** modelagem de sobrevivência (Kaplan-Meier).

---

## 5. Etapas do Código

1. **Contagem de incidentes** por `organization_type`.
2. **Filtragem** das organizações com ao menos 10 incidentes.
3. **Cálculo dos intervalos** (`days_since_last`) entre incidentes consecutivos.
4. **Ajuste do modelo Kaplan-Meier** para cada grupo de organização.
5. **Visualização** das curvas de sobrevivência no mesmo gráfico, comparando setores.

---

## 6. Resultados Esperados

* **Curvas de Sobrevivência** exibindo a probabilidade cumulativa de não ocorrência de novos incidentes conforme os dias desde a última violação.
* Setores com curvas mais inclinadas para baixo indicam **maior risco de recorrência rápida**.
* A comparação entre setores ajuda a identificar áreas que necessitam de **maior atenção em políticas de segurança**.

---

## 7. Visualizações

* **Gráfico Kaplan-Meier:** compara a sobrevivência (tempo sem novas violações) entre os tipos de organização.
* Ajustes aplicados:

  * Eixo **X:** Dias desde a última violação (limite configurável, ex.: 0 a 500 dias).
  * Eixo **Y:** Probabilidade de não ocorrência de nova violação.
  * **Legenda:** identifica os tipos de organização.

---

## 8. Conclusões e Próximos Passos

* O uso do Kaplan-Meier oferece insights valiosos sobre a **frequência e rapidez de reincidência de violações**.
* Permite **priorizar setores** para políticas preventivas e monitoramento.
* **Próximos passos sugeridos:**

  * Incluir covariáveis (ex.: tipo de violação) em modelos de **risco proporcional de Cox**.
  * Avaliar impacto de medidas de mitigação ao longo do tempo.
  * Aplicar testes estatísticos para comparar curvas entre setores.

---

## 9. Configuração do Ambiente

* Python 3.8+
* Instalar dependências:

```bash
pip install pandas matplotlib lifelines
```

---

## 10. Desenvolvido por

* **Autor:** *\[Evanei Gomes dos Santos e Caroline Nazare Dos Santos Chucre Kappel]*
* **Projeto:** Análise de Sobrevivência com Kaplan-Meier
* **Data de Conclusão:** *\[26/09/2025]*

---


