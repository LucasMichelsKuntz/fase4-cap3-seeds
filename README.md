# FIAP - Faculdade de Informática e Administração Paulista

<p align="center">
<a href="https://www.fiap.com.br/"><img src="assets/logo-fiap.png" alt="FIAP - Faculdade de Informática e Administração Paulista" border="0" width=40% height=40%></a>
</p>

<br>

# Classificação de Variedades de Grãos de Trigo — Seeds Dataset

## 👨‍🎓 Integrantes:
- <a href="https://www.linkedin.com/in/">Lucas Michels Kuntz</a> — RM 570050

## 👩‍🏫 Professores:
### Tutor(a)
- <a href="https://www.linkedin.com/in/">Sabrina Otoni</a>
### Coordenador(a)
- <a href="https://www.linkedin.com/in/">André Godoi</a>

---

## Descrição

Projeto de classificação supervisionada aplicando a metodologia **CRISP-DM** ao [Seeds Dataset](https://archive.ics.uci.edu/dataset/236/seeds) (UCI Machine Learning Repository, id=236). O objetivo é classificar automaticamente amostras de grão de trigo em três variedades — **Kama**, **Rosa** e **Canadian** — a partir de 7 características físicas mensuráveis por sensores ópticos, simulando a automação de triagem em cooperativas agrícolas.

**Dataset:** 210 amostras, 7 features numéricas, 3 classes perfeitamente balanceadas (70 amostras/classe).

| # | Atributo | Descrição |
|---|---|---|
| 1 | Área | Medida da área da seção transversal do grão |
| 2 | Perímetro | Comprimento do contorno do grão |
| 3 | Compacidade | Calculada como $4\pi \cdot \text{Área} / \text{Perímetro}^2$ |
| 4 | Comprimento do Núcleo | Comprimento do eixo principal da elipse equivalente |
| 5 | Largura do Núcleo | Comprimento do eixo secundário da elipse |
| 6 | Coeficiente de Assimetria | Medida de assimetria do grão |
| 7 | Comprimento do Sulco | Comprimento do sulco central do grão |

---

## Estrutura de pastas

```
fase4-cap3-seeds/
│
├── assets/
│   └── logo-fiap.png
│
├── LucasMichelsKuntz_RM570050_fase4_cap03_seeds.ipynb   # Notebook principal (CRISP-DM completo)
├── requirements.txt
└── README.md
```

---

## Metodologia (CRISP-DM)

| Seção | Fase | Conteúdo |
|---|---|---|
| 1 | Entendimento do Negócio | Objetivo, critério de sucesso (Acurácia ≥ 90%), descrição dos atributos |
| 2.1–2.4 | Entendimento dos Dados | EDA: estatísticas descritivas, histogramas, boxplots, scatter plots, matriz de correlação |
| 2.5 | Preparação dos Dados | Split 70/30 estratificado, `StandardScaler` ajustado apenas no treino (sem data leakage) |
| 3 | Modelagem | KNN, SVM (RBF), Random Forest, Naive Bayes Gaussiano, Regressão Logística |
| 4 | Modelagem (iteração 2) | `GridSearchCV` com `StratifiedKFold(5)` para KNN, SVM e Random Forest |
| 5 | Avaliação e Implantação | Importância de features (Gini), coeficientes LR, pipeline `joblib` para produção |

---

## Como executar o código

### Pré-requisitos

- Python 3.10 ou superior
- Jupyter Notebook ou Google Colab

### Instalação

```bash
pip install -r requirements.txt
```

### Execução local

```bash
jupyter notebook LucasMichelsKuntz_RM570050_fase4_cap03_seeds.ipynb
```

### Google Colab

Faça upload do arquivo `.ipynb` no Colab — o notebook carrega o dataset automaticamente via `ucimlrepo` (com fallback para download direto do UCI).

---

## Histórico de lançamentos

* 1.0.0 — 18/06/2026
    * Notebook CRISP-DM completo: EDA, 5 classificadores, Grid Search CV e pipeline de produção

---

## Licença

<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1"><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1">

<p xmlns:cc="http://creativecommons.org/ns#" xmlns:dct="http://purl.org/dc/terms/">
  Este projeto está licenciado sob
  <a href="http://creativecommons.org/licenses/by/4.0/?ref=chooser-v1" target="_blank">Attribution 4.0 International</a>.
</p>
