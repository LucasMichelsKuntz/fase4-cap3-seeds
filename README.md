<div align="center">
<sub>Instituição: FIAP</sub>
</div>

# Classificação de Variedades de Grãos de Trigo — Seeds Dataset

**Fase 04 — CTWP — Cap 03: Implementando Algoritmos de Machine Learning com Scikit-learn**

## Aluno

| Nome | RM |
|---|---|
| Lucas Michels Kuntz | 570050 |

## Professores

### Tutor(a)
- Edson de Oliveira

### Coordenador(a)
- André Godoi

---

## Descrição

Projeto de classificação supervisionada aplicando a metodologia **CRISP-DM** ao Seeds Dataset (UCI Machine Learning Repository, id=236). O objetivo é classificar automaticamente amostras de grão de trigo em três variedades — **Kama**, **Rosa** e **Canadian** — a partir de 7 características físicas mensuráveis por sensores ópticos, simulando a automação de triagem em cooperativas agrícolas.

### Características do Dataset

| # | Atributo | Descrição |
|---|---|---|
| 1 | Área | Medida da área da seção transversal do grão |
| 2 | Perímetro | Comprimento do contorno do grão |
| 3 | Compacidade | $4\pi \cdot \text{Área} / \text{Perímetro}^2$ |
| 4 | Comprimento do Núcleo | Comprimento do eixo principal da elipse equivalente |
| 5 | Largura do Núcleo | Comprimento do eixo secundário da elipse |
| 6 | Coeficiente de Assimetria | Medida de assimetria do grão |
| 7 | Comprimento do Sulco | Comprimento do sulco central do grão |

- **210 amostras**, **7 features**, **3 classes** (70 amostras/classe — balanceado)

---

## Estrutura do Projeto

```
fase4-cap3-seeds/
├── LucasMichelsKuntz_RM570050_fase4_cap03_seeds.ipynb   # Notebook principal
├── requirements.txt                                      # Dependências Python
└── README.md
```

---

## Metodologia (CRISP-DM)

| Fase | Conteúdo no Notebook |
|---|---|
| 1. Entendimento do Negócio | Seção 1 — objetivo, critério de sucesso, atributos |
| 2. Entendimento dos Dados | Seção 2.1–2.4 — EDA, estatísticas, histogramas, boxplots, scatter, correlação |
| 3. Preparação dos Dados | Seção 2.5 — split 70/30 estratificado, StandardScaler (sem data leakage) |
| 4. Modelagem | Seção 3 — KNN, SVM, Random Forest, Naive Bayes, Regressão Logística |
| 4 (iter 2) | Seção 4 — Grid Search CV (KNN, SVM, Random Forest) |
| 5. Avaliação | Seção 5 — importância de features, coeficientes, resumo final |
| 6. Implantação | Seção 5 — Pipeline exportado via joblib |

---

## Modelos Implementados

| Modelo | Dados de entrada | Observação |
|---|---|---|
| K-Nearest Neighbors (KNN) | Normalizados | k=5, métrica euclidiana (baseline) |
| Support Vector Machine (SVM) | Normalizados | Kernel RBF, C=1, gamma=scale |
| Random Forest | Brutos | 200 árvores (tree-based, não precisa de escala) |
| Naive Bayes Gaussiano | Normalizados | Baseline probabilístico |
| Regressão Logística | Normalizados | Baseline linear |

---

## Como Executar

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

Faça upload do arquivo `.ipynb` no Colab — o notebook carrega o dataset automaticamente via `ucimlrepo` ou download direto do UCI.

---

## Resultados

Todos os modelos atingem **acurácia ≥ 90%** no conjunto de teste (meta do negócio). O melhor modelo (SVM com Grid Search) é exportado como pipeline scikit-learn via `joblib` para uso em produção.

---

## Licença

<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1"><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1">

Este projeto está licenciado sob [Attribution 4.0 International](http://creativecommons.org/licenses/by/4.0/?ref=chooser-v1).
