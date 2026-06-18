<div align="center">
<sub>Instituição: FIAP</sub>
</div>

# Classificação de Variedades de Grãos de Trigo — Seeds Dataset

## 👨‍🎓 Integrante

- Lucas Michels Kuntz - RM 570050

## 👩‍🏫 Professores

### Tutor(a)
- <a href="#">Edson de Oliveira</a>

### Coordenador(a)
- <a href="#">André Godoi</a>

---

## 📜 Descrição

Em cooperativas agrícolas de pequeno porte, a classificação de grãos de trigo é realizada **manualmente por especialistas** — um processo lento e sujeito a erros humanos. Este projeto aplica a metodologia **CRISP-DM** para construir um modelo de aprendizado de máquina capaz de **classificar automaticamente** amostras de grão de trigo em três variedades (**Kama**, **Rosa** e **Canadian**) a partir de 7 características físicas mensuráveis por sensores ópticos.

**Dataset:** [Seeds Dataset — UCI Machine Learning Repository (id=236)](https://archive.ics.uci.edu/dataset/236/seeds) — 210 amostras, 7 features numéricas, 3 classes balanceadas (70 amostras/classe).

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

## 📁 Estrutura de Pastas

```
fase4-cap3-seeds/
│
├── LucasMichelsKuntz_RM570050_fase4_cap03_seeds.ipynb   # Notebook principal (CRISP-DM completo)
├── requirements.txt                                      # Dependências Python
└── README.md
```

---

## 🔧 Como Executar

### Pré-requisitos

- Python 3.10+
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

## 🗃 Conteúdo do Notebook (CRISP-DM)

| Seção | Fase CRISP-DM | Conteúdo |
|---|---|---|
| 1 | Entendimento do Negócio | Objetivo, critério de sucesso (Acurácia ≥ 90%), descrição dos atributos |
| 2.1–2.4 | Entendimento dos Dados | EDA: estatísticas descritivas, histogramas, boxplots, scatter plots, matriz de correlação |
| 2.5 | Preparação dos Dados | Split 70/30 estratificado, `StandardScaler` ajustado apenas no treino (sem data leakage) |
| 3 | Modelagem | KNN, SVM (RBF), Random Forest, Naive Bayes Gaussiano, Regressão Logística |
| 4 | Modelagem (iteração 2) | `GridSearchCV` com `StratifiedKFold(5)` para KNN, SVM e Random Forest |
| 5 | Avaliação e Implantação | Importância de features (Gini), coeficientes LR, pipeline `joblib` para produção |

---

## 📋 Licença

<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1"><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1">

<p xmlns:cc="http://creativecommons.org/ns#" xmlns:dct="http://purl.org/dc/terms/">
  Este projeto está licenciado sob
  <a href="http://creativecommons.org/licenses/by/4.0/?ref=chooser-v1" target="_blank">Attribution 4.0 International</a>.
</p>
