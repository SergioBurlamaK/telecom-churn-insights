# Análise de Evasão de Clientes (Churn) - TelecomX

## 📄 Visão Geral do Projeto

Este projeto tem como objetivo principal analisar e compreender os fatores que levam à evasão de clientes (churn) em uma empresa de telecomunicações fictícia, a TelecomX. Através da análise de dados de clientes, buscamos identificar padrões e tendências que possam auxiliar na retenção de clientes e na formulação de estratégias de negócio mais eficazes.

O notebook `TelecomX_BR.ipynb` detalha todo o processo, desde a extração e transformação dos dados até a análise exploratória e visualização dos resultados.

## 📊 Dados

Os dados utilizados nesta análise foram obtidos de um arquivo JSON disponível publicamente. O dataset contém informações detalhadas sobre os clientes da TelecomX, incluindo:

*   **Informações do Cliente:** ID do cliente, gênero, status de idoso (SeniorCitizen), se possui parceiro (Partner), se possui dependentes (Dependents) e tempo de permanência (tenure).
*   **Serviços de Telefone:** Se possui serviço telefônico (PhoneService) e múltiplas linhas (MultipleLines).
*   **Serviços de Internet:** Tipo de serviço de internet (InternetService), segurança online (OnlineSecurity), backup online (OnlineBackup), proteção de dispositivo (DeviceProtection), suporte técnico (TechSupport), streaming de TV (StreamingTV) e streaming de filmes (StreamingMovies).
*   **Informações da Conta:** Tipo de contrato (Contract), faturamento sem papel (PaperlessBilling), método de pagamento (PaymentMethod), encargos mensais (Charges.Monthly) e encargos totais (Charges.Total).
*   **Churn:** Indica se o cliente evadiu (Yes/No).

**Fonte dos Dados:** `https://raw.githubusercontent.com/alura-cursos/challenge2-data-science/refs/heads/main/TelecomX_Data.json`

## 🚀 Estrutura do Projeto

```
telecom-churn-insights/
├── TelecomX_BR.ipynb
├── outputs  # Gráficos Usados/Gerados no Projeto
└── README.md
```

## 🛠️ Tecnologias Utilizadas

*   **Python:** Linguagem de programação principal.
*   **Pandas:** Biblioteca para manipulação e análise de dados.
*   **Plotly Express:** Biblioteca para criação de visualizações interativas.

## ⚙️ Como Executar o Projeto

Para replicar a análise, siga os passos abaixo:

1.  **Clone o Repositório:**
    ```bash
    git clone git@github.com:SergioBurlamaK/telecom-churn-insights.git
    cd telecom-churn-insights
    ```
    (Caso contrário pode apenas baixe o arquivo `.ipynb`).

2.  **Abra o Notebook no Google Colab:**
    *   Vá para [Google Colab](https://colab.research.google.com/).
    *   Clique em `File` > `Upload notebook` e selecione o arquivo `TelecomX_BR.ipynb`.

3.  **Execute as Células:**
    *   Execute as células do notebook sequencialmente. O notebook está dividido em seções para facilitar a compreensão:
        *   **Extração:** Carrega os dados do JSON.
        *   **Transformação:** Realiza a limpeza e o pré-processamento dos dados.
        *   **Carga e Análise:** Apresenta as visualizações e insights.

## 🔍 Análise e Resultados

A análise exploratória de dados revelou insights importantes sobre a evasão de clientes:

### **1. Extração e Normalização dos Dados**

*   Os dados foram extraídos de um arquivo JSON e normalizados para um formato tabular usando `pd.json_normalize()`.
*   O DataFrame inicial possui 7267 linhas e 6 colunas, que foram expandidas para 21 colunas após a normalização.

### **2. Qualidade dos Dados**

*   **Valores Duplicados:** Não foram encontrados registros duplicados no dataset.
*   **Valores Nulos:** Não foram encontrados valores nulos explícitos.
*   **Valores Vazios/Em Branco:**
    *   A coluna `Churn` continha 224 valores vazios, que foram removidos para garantir a integridade da análise de churn.
    *   A coluna `account.Charges.Total` continha 11 valores vazios, que foram convertidos para `NaN` durante a conversão de tipo e posteriormente tratados pela remoção das linhas com `Churn` vazio.
*   **Tipos de Dados:** A coluna `account.Charges.Total` foi convertida para o tipo numérico (`float64`) para permitir cálculos.

### **3. Análise de Churn por Gênero**

*   **Visualização:** Um histograma foi gerado para mostrar a distribuição de churn por gênero.
*   **Insight:** A distribuição de churn entre homens e mulheres é relativamente equilibrada, sugerindo que o gênero, por si só, não é um fator predominante na decisão de evasão.

### **4. Análise de Churn por Senior Citizen**

*   **Visualização:** Um histograma foi gerado para mostrar a distribuição de churn por status de Senior Citizen (0 para não idoso, 1 para idoso).
*   **Insight:** Clientes idosos (Senior Citizen = 1) apresentam uma taxa de churn visivelmente maior em comparação com clientes não idosos (Senior Citizen = 0). Isso indica que este grupo demográfico pode ser mais propenso a evadir.

### **5. Análise de Churn por Tempo de Permanência (Tenure)**

*   **Visualização:**
    *   Um histograma mostra a distribuição de churn ao longo do tempo de permanência.
    *   Um gráfico de linha exibe a taxa de churn percentual para cada mês de permanência.
*   **Insight:**
    *   A taxa de churn é significativamente alta nos primeiros meses de permanência do cliente, atingindo um pico em torno de 62% no primeiro mês.
    *   A taxa de churn diminui drasticamente à medida que o tempo de permanência aumenta, estabilizando-se em níveis baixos para clientes com mais de 60 meses de permanência. Isso sugere que clientes de longo prazo são mais leais.
    *   Foi criada uma nova coluna `Total.Day` para representar o custo diário do serviço, calculada a partir dos encargos totais e do tempo de permanência.

### **6. Relação entre Tempo de Permanência e Encargos Mensais**

*   **Visualização:** Um gráfico de dispersão foi utilizado para explorar a relação entre o tempo de permanência e os encargos mensais, colorindo os pontos pelo status de churn.
*   **Insight:**
    *   Clientes com contratos de curto prazo (Month-to-month) e encargos mensais mais altos tendem a ter uma maior taxa de churn, especialmente nos primeiros meses.
    *   Clientes com contratos de longo prazo (One year, Two year) e encargos mensais variados demonstram menor propensão ao churn, independentemente do valor mensal.
    *   Há uma concentração de clientes com churn nos primeiros meses de contrato, independentemente do valor do encargo mensal, reforçando o insight anterior sobre a importância dos primeiros meses.

## 💡 Conclusões e Recomendações

Com base na análise, as seguintes conclusões e recomendações podem ser feitas:

*   **Foco na Retenção de Clientes Recém-Adquiridos:** A alta taxa de churn nos primeiros meses de permanência indica a necessidade de programas de onboarding robustos, acompanhamento proativo e ofertas especiais para novos clientes.
*   **Atenção aos Clientes Idosos:** O segmento de Senior Citizens apresenta maior propensão ao churn. Estratégias de comunicação e ofertas personalizadas para este grupo podem ser eficazes.
*   **Análise de Contratos:** Clientes com contratos mensais (Month-to-month) são mais suscetíveis ao churn. Incentivar contratos de longo prazo com benefícios adicionais pode ser uma estratégia de retenção.
*   **Monitoramento de Encargos Mensais:** Embora não seja o único fator, a combinação de altos encargos mensais e curto tempo de permanência está associada a maior churn. É importante avaliar a competitividade dos preços e o valor percebido pelos clientes.

## 🤝 Contribuições

Contribuições são bem-vindas! Sinta-se à vontade para abrir issues ou pull requests para melhorias, correções ou novas análises.

## 👨‍💻 Autor  

|  |  |
|--|--|
| ✨ **Nome** | Sergio Burlamaqui |
| 📌 **GitHub** | [![GitHub](https://img.shields.io/badge/-SergioBurlamaK-181717?style=flat&logo=github&logoColor=white)](https://github.com/SergioBurlamaK) |
| 📧 **E-mail** | [![Outlook](https://img.shields.io/badge/-sergio_o.b_junior@hotmail.com-0078D4?style=flat&logo=microsoft-outlook&logoColor=white)](mailto:sergio_o.b_junior@hotmail.com) |
| 💼 **LinkedIn** | [![LinkedIn](https://img.shields.io/badge/-Sergio_Burlamaqui-0077B5?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/sergioburlamaqui/) |

---