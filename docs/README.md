# Medidas DAX – Projeto NPS Analytics

Este documento reúne as principais medidas DAX utilizadas no dashboard de
análise de NPS da agência bancária fictícia.

As medidas foram desenvolvidas com foco em:
- clareza de leitura
- respeito ao contexto de filtro
- reutilização em diferentes visuais
- apoio à análise comparativa

---

## 📊 Métricas de Base

### Total de Respostas
```DAX
Total_Respostas =
COUNTROWS('NPS')

---

Media_NPS =
AVERAGE('NPS'[Nota_NPS])

---

Rank_Gerente =
RANKX(
    ALL('NPS'[Gerente]),
    [Media_NPS],
    ,
    DESC,
    DENSE
)


Rank_Visual =
SWITCH(
    TRUE(),
    [Rank_Gerente] = 1, "#1 🏆",
    [Rank_Gerente] = 2, "#2 🏆",
    [Rank_Gerente] = 3, "#3 🏆",
    "#" & FORMAT([Rank_Gerente], "0")
)

NPS =
DIVIDE(
    [Qtd_Promotores] - [Qtd_Detratores],
    [Total_Respostas]
) * 100

