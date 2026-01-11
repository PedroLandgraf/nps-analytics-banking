# Medidas DAX – NPS Analytics (Agência Bancária)

Este documento apresenta as principais **medidas DAX** utilizadas no dashboard
de análise de NPS de uma agência bancária fictícia.

O objetivo é documentar a lógica de cálculo e facilitar o entendimento
das métricas utilizadas no relatório.

---

## 📊 Métricas Básicas

### Total de Respostas
```DAX
Total_Respostas =
COUNTROWS('NPS')

NPS =
DIVIDE(
    [Qtd_Promotores] - [Qtd_Detratores],
    [Total_Respostas]
) * 100

---


