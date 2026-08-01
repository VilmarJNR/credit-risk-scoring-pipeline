# 💳 Modelo Preditivo de Inadimplência de Crédito

## 📌 Contexto do Negócio
Projeto desenvolvido com o objetivo de prever a probabilidade de inadimplência em cobranças mensais de clientes, permitindo que a equipe de crédito e cobrança atue de forma proativa para reduzir perdas financeiras.

## ⚙️ Regra da Variável Alvo (Target)
A inadimplência foi definida segundo as diretrizes de negócio: cobranças com atraso *igual ou superior a 5 dias* em relação ao vencimento (ou não pagas) foram classificadas como inadimplentes (target = 1).

## 🚀 Abordagem Técnica e Destaques
- *Engenharia de Features*: Criação de índices de comprometimento financeiro (Razão Valor/Renda), renda por funcionário e prazos de relacionamento do cliente.
- *Validação Out-Of-Time (OOT): Separação estrita por safras temporais para simular o comportamento real do modelo em produção e evitar vazamentos de dados do futuro (*data leakage).
- *Algoritmo: Utilização do algoritmo **LightGBM*, otimizado para calibração de probabilidade.

## 📊 Resultados Obtidos
Na validação temporizada com a última safra disponível (OOT):
- *ROC-AUC*: 0.9455 (Alta capacidade de ordenamento do risco de clientes)
- *Log-Loss*: 0.1101 (Excelente calibração das probabilidades)

## 🛠️ Como Reproduzir este Projeto
1. Clone o repositório:
   ```bash
   git clone [https://github.com/VilmarJNR/credit-risk-scoring-pipeline.git](https://github.com/VilmarJNR/credit-risk-scoring-pipeline.git)