# Previsão de Inadimplência com Machine Learning
![image](https://github.com/user-attachments/assets/9517bf50-02e0-4870-92c9-526318479e13)



Este projeto tem como objetivo prever a inadimplência de clientes no momento da solicitação de um cartão de crédito, utilizando técnicas de Machine Learning aplicadas a dados cadastrais, comportamentais e socioeconômicos. A solução visa auxiliar uma fintech na tomada de decisões mais seguras e eficazes na concessão de crédito.

---

## 📌 Contexto

A análise de crédito é essencial para fintechs que atuam em ambientes altamente competitivos e orientados por dados. Com o avanço da ciência de dados, modelos preditivos vêm sendo usados para reduzir perdas com inadimplência e promover inclusão financeira, possibilitando aprovações mais justas e seguras.

---

## 🎯 Objetivo do Projeto

Identificar, com base em dados históricos e cadastrais, quais clientes têm maior probabilidade de não pagarem suas dívidas, permitindo que a fintech:

- Reduza riscos financeiros;
- Otimize limites e condições de crédito;
- Tome decisões mais precisas na aprovação de clientes.

---

## 🧩 Bases de Dados Utilizadas

Foram utilizados três datasets principais, posteriormente unificados no dataframe `df_unique`:

- `application_train_dataset.csv`: Dados demográficos, socioeconômicos e comportamentais dos clientes.
- `customers_target_and_decision_dataset.csv`: Contém a variável alvo (`default`) e a decisão sobre o crédito.
- `unstructured_dataset.csv`: Dados não estruturados que complementam o perfil do cliente.

---

## 🛠️ Pré-Processamento

As principais etapas foram:

1. **Conversão de datas e extração de componentes temporais** (ano, mês, dia da semana, etc.);
2. **Criação da variável `days_diff`**: diferença em dias entre a data de score e a data do pagamento;
3. **Tratamento de valores ausentes**:
   - `flag_document_A`: preenchido com a moda;
4. **Transformações categóricas**:
   - `gender`: binarizado (`m=1`, `f=0`);
   - `flag_document_A`: convertido para inteiro;
5. **One-Hot Encoding**: aplicado a colunas categóricas com poucos níveis (ex: `ext_score_2`);
6. **Target Encoding com validação cruzada**: aplicado à variável `occupation_type`;
7. **Remoção de colunas irrelevantes**: `channel`, `ids`, `score_date`, `date`.

---

## ⚙️ Modelos Aplicados

### 🔹 Baseline
- Alto desempenho nas métricas convencionais (acurácia: 99%), mas AUC de apenas **0.489**.
- Fraca capacidade de separação entre classes → necessidade de modelos mais robustos.

### 🔹 Regressão Logística
- AUC: **0.978**
- F1-score: 0.84 (classe 1)
- Recall da classe 1: 0.78
- **Boa separação entre as classes**, mas perde alguns inadimplentes.

### 🔹 Random Forest
- AUC: **1.0000**
- Acurácia: 100%
- Falsos positivos: 11 | Falsos negativos: 108
- Desempenho excelente, mas precisa de avaliação quanto a **possível overfitting**.

### 🔹 XGBoost
- AUC: **0.9933**
- F1-score: 0.94 (média macro)
- MAE (probabilidades): **0.0550**
- Baixo número de falsos positivos e **alta confiabilidade nas previsões**.

---

## 📊 Importância das Variáveis

Para todos os modelos foram gerados gráficos de **feature importance**. As variáveis mais relevantes incluem:

- occupation_type
- flag_document_A
- start_hour
- score_weekofyear
- credit_card_initial_line
- payment

---

## 📈 Avaliação de Performance

| Modelo            | Acurácia | Recall (Classe 1) | F1-score (Classe 1) | AUC    |
|-------------------|----------|-------------------|----------------------|--------|
| Baseline          | 0.99     | 0.93              | 0.96                 | 0.489  |
| Regressão Logística | 0.95   | 0.78              | 0.84                 | 0.978  |
| Random Forest     | 1.00     | 0.99              | 0.99                 | 1.000  |
| XGBoost           | 0.97     | 0.83              | 0.91                 | 0.9933 |

---


## 📁 Estrutura do Projeto

A estrutura de diretórios do projeto foi organizada da seguinte forma:


```bash
credit_fintech/
├── data/                    # Dados brutos e processados
│   ├── raw/
│   └── processed/
├── notebooks/               # Notebooks com análises e modelagens
├── models/                  # Modelos treinados (.pkl)
├── reports/                 # Relatórios e figuras
│   └── figures/
├── src/                     # Código-fonte do projeto
│   ├── preprocessing.py     # Pipeline de pré-processamento
│   └── train_models.py      # Treinamento dos modelos
├── requirements.txt         # Dependências do projeto
├── README.md                # Documentação do projeto
└── .gitignore
```

---

## ✅ Conclusões

- O modelo Random Forest apresentou desempenho quase perfeito, mas precisa ser testado em produção para evitar overfitting.
- O XGBoost combinou alta performance e boa generalização, sendo uma excelente alternativa de produção.
- O modelo de Regressão Logística pode servir como benchmark por sua interpretabilidade e desempenho sólido.
- Métricas como AUC, análise da distribuição dos scores e análise de erro foram fundamentais para avaliar os modelos de forma profunda.

---

## 📈 Próximos Passos

- Monitoramento do modelo em produção com foco em **drift detection**
- Calibração de probabilidades
- Teste de modelos mais avançados (e.g. reinforcement learning)
- Inclusão de dados comportamentais em tempo real

---

## 🧪 Tecnologias Utilizadas

- Python 3.11  
- Pandas, NumPy  
- Scikit-learn  
- XGBoost  
- Matplotlib, Seaborn  
- SHAP  
- Jupyter Notebook  

---

## 🤝 Contribuições

Contribuições são bem-vindas!  
Abra uma *issue* ou envie um *pull request* com sugestões ou melhorias.

---

## 👩‍💻 Autora

**Josiele Ferreira**  
*Cientista de Dados*  
🔗 [LinkedIn](https://https://www.linkedin.com/in/josiele-ferreira-90686a1b2/)

---



