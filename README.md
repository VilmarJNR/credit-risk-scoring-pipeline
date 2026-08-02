## 📌 Visão Geral do Projeto

Este projeto consiste na construção de uma solução end-to-end para **previsão de risco de crédito e inadimplência financeira**, simulando um ambiente real de concessão de crédito. 

O objetivo principal é classificar transações/clientes com alta probabilidade de atraso no pagamento (inadimplência definida como atraso ≥ 5 dias ou não pagamento), auxiliando na tomada de decisão estratégica para minimização de perdas financeiras e manutenção da carteira saudável.

---

## 🛠️ Tecnologias e Ferramentas

* **Linguagem:** Python
* **Manipulação e Engenharia de Dados:** `Pandas`, `NumPy`
* **Machine Learning:** `LightGBM`, `Scikit-Learn`
* **Visualização de Dados:** `Matplotlib`, `Seaborn`
* **Métricas de Avaliação:** ROC-AUC, Log-Loss, Matriz de Confusão e Feature Importance

---

## ⚙️ Arquitetura e Metodologia

O pipeline do projeto foi desenvolvido seguindo as melhores práticas da indústria de dados:

### 1. Pré-processamento e Construção da Target
- Integração de bases cadastrais, histórico financeiro e informações de pagamento.
- **Definição da Target (`TARGET`):** Atribuído `1` para pagamentos com atraso ≥ 5 dias em relação ao vencimento ou com registro de pagamento ausente (`NaN`), e `0` para adimplentes.

### 2. Engenharia de Features (*Feature Engineering*)
Criação de métricas comportamentais, financeiras e temporais de alto poder discriminativo:
- **Ratios Financeiros:** Comprometimento do valor da parcela em relação à renda do mês anterior (`RATIO_VALOR_RENDA`) e renda por funcionário (`RENDA_POR_FUNC`).
- **Métricas Temporais:** Prazo concedido para pagamento (`PRAZO_PAGAMENTO_DIAS`) e tempo de relacionamento do cliente com a instituição (`TEMPO_RELACIONAMENTO_DIAS`).
- **Encoding:** Tratamento nativo de variáveis categóricas (como segmento industrial, porte, DDD e estado/CEP) via suporte do LightGBM.

### 3. Validação Out-Of-Time (OOT)
Para evitar o *data leakage* (vazamento de dados) e garantir generalização em ambiente produtivo, a estratégia de validação utilizou estritamente a **última safra temporal** disponível no conjunto de desenvolvimento.

---

## 📊 Resultados e Diagnósticos

### 📉 Desempenho do Modelo
- **ROC-AUC (Validação OOT):** `0.9455` (Alta capacidade discriminativa entre clientes bons e maus pagadores).
- **Log-Loss (OOT):** `0.1120` (Calibração sólida das probabilidades preditas).

### 🔍 Destaques dos Diagnósticos Visuais

1. **Feature Importance:** As variáveis mais determinantes para a pontuação de risco foram o **tempo de relacionamento**, **CEP (região)** e **prazo de pagamento**, evidenciando que o histórico comportamental supera dados cadastrais estáticos.
2. **Distribuição Preditiva:** O modelo isolou com alta precisão o grupo adimplente próximo a $0\%$ de probabilidade de risco, permitindo automação de crédito rápido para a maioria dos clientes.
3. **Matriz de Confusão (Cutoff = 0.30):** 
   - Captura de **59% dos inadimplentes** na safra OOT.
   - Geração de apenas **1.5% de falsos alarmes** na base de bons pagadores, preservando a experiência do cliente adimplente.

## 🛠️ Como Reproduzir este Projeto
1. Clone o repositório:
   ```bash
   git clone [https://github.com/VilmarJNR/credit-risk-scoring-pipeline.git](https://github.com/VilmarJNR/credit-risk-scoring-pipeline.git)
