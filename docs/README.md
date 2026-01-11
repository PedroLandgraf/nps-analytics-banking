# Medidas DAX – Projeto NPS Analytics (Agência Bancária)

Este documento reúne as principais medidas DAX utilizadas no dashboard
de análise de NPS de uma agência bancária fictícia.

As medidas foram organizadas por finalidade para facilitar leitura
e manutenção.

---

## 📊 Métricas Básicas

### Total de Respostas
```DAX
Total_Respostas =
COUNTROWS('NPS')

Media_NPS =
AVERAGE('NPS'[Nota_NPS])

Qtd_Promotores =
CALCULATE(
    COUNTROWS('NPS'),
    'NPS'[Classificacao_NPS] = "Promotor"
)

Qtd_Neutros =
CALCULATE(
    COUNTROWS('NPS'),
    'NPS'[Classificacao_NPS] = "Neutro"
)

Qtd_Detratores =
CALCULATE(
    COUNTROWS('NPS'),
    'NPS'[Classificacao_NPS] = "Detrator"
)

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

CSAT_Radar =
SWITCH(
    SELECTEDVALUE(Dim_Categoria[Categoria]),
    "Equipe",          AVERAGE('NPS'[Equipe]),
    "Confiabilidade", AVERAGE('NPS'[Confiabilidade]),
    "Experiência",    AVERAGE('NPS'[Experiência]),
    "Site",           AVERAGE('NPS'[Site]),
    "Variedade",      AVERAGE('NPS'[Variedade]),
    "Inovação",       AVERAGE('NPS'[Inovação]),
    "Resolução",      AVERAGE('NPS'[Resolução])
)

Cor_Media_NPS =
SWITCH(
    TRUE(),
    [Media_NPS] >= 7, "#42C87A",
    [Media_NPS] >= 4, "#FFC145",
    "#FB4141"
)




