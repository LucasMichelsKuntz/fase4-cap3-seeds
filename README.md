# FIAP - Faculdade de Informática e Administração Paulista

<p align="center">
<a href="https://www.fiap.com.br/"><img src="assets/logo-fiap.png" alt="FIAP - Faculdade de Informática e Administração Paulista" border="0" width=40% height=40%></a>
</p>

<br>

# Classificação de Variedades de Grãos de Trigo (Seeds Dataset)

## 👨‍🎓 Integrantes:
- <a href="https://www.linkedin.com/in/">Lucas Michels Kuntz</a> (RM 570050)

## 👩‍🏫 Professores:
### Tutor(a)
- <a href="https://www.linkedin.com/in/">Sabrina Otoni</a>
### Coordenador(a)
- <a href="https://www.linkedin.com/in/">André Godoi</a>

---

## Descrição

Hoje, em boa parte das cooperativas de pequeno porte, a separação dos grãos de trigo por variedade ainda depende de um especialista olhando amostra por amostra. É um trabalho lento, cansativo e que varia de pessoa para pessoa, o que abre espaço para erro de classificação justamente nos lotes que mais importam.

A proposta aqui é mostrar que dá para resolver isso com aprendizado de máquina. A partir de sete medidas físicas do grão, todas obtidas por sensores ópticos, treino modelos que dizem a qual das três variedades aquele grão pertence: Kama, Rosa ou Canadian. Todo o trabalho segue a metodologia CRISP-DM, então o notebook não pula direto para o modelo: ele começa entendendo o problema de negócio, passa pela análise dos dados e só depois chega na parte de treinar e comparar algoritmos.

Os dados vêm do [Seeds Dataset](https://archive.ics.uci.edu/dataset/236/seeds) do UCI Machine Learning Repository. São 210 amostras no total, com sete atributos numéricos cada, divididas igualmente entre as três variedades (70 grãos de cada). Esse equilíbrio perfeito entre as classes é uma sorte que raramente se tem em dados reais e que simplifica bastante a avaliação, porque a acurácia deixa de ser uma métrica enganosa.

As sete medidas usadas são:

| Atributo | O que mede |
|---|---|
| Área | Tamanho da seção transversal do grão |
| Perímetro | Comprimento do contorno externo |
| Compacidade | $4\pi \cdot \text{Área} / \text{Perímetro}^2$, indica o quão próximo de um círculo o grão é |
| Comprimento do Núcleo | Eixo maior da elipse equivalente ao grão |
| Largura do Núcleo | Eixo menor dessa mesma elipse |
| Coeficiente de Assimetria | Quão torto ou irregular é o formato |
| Comprimento do Sulco | Tamanho do sulco central, a "ranhura" do grão |

Vale notar que área, perímetro e os comprimentos andam muito juntos, já que todos descrevem, de um jeito ou de outro, o tamanho do grão. A compacidade e a assimetria são as que trazem informação mais independente, e acabam sendo decisivas para separar as variedades de tamanho parecido.

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

## Como o trabalho foi conduzido (CRISP-DM)

O notebook está organizado nas fases do CRISP-DM, na ordem em que elas fazem sentido.

**Entendimento do negócio.** Antes de qualquer linha de código de modelo, defino o que conta como sucesso: acurácia de pelo menos 90% no conjunto de teste, com o F1 equilibrado entre as três classes. Esse último ponto é importante porque não adianta o modelo acertar muito Rosa e errar Kama; ele precisa ser parelho.

**Entendimento e preparação dos dados.** Aqui mora a parte mais densa da análise exploratória. Calculo as estatísticas descritivas por variedade e gero histogramas, boxplots, gráficos de dispersão e a matriz de correlação. É olhando esses gráficos que fica visível, por exemplo, que Rosa é claramente a variedade de grão maior e Canadian a menor, enquanto Kama fica no meio do caminho e por isso é a mais fácil de confundir. Na preparação, separo 70% para treino e 30% para teste de forma estratificada (para manter a proporção das classes nos dois conjuntos) e aplico o `StandardScaler`. Um cuidado que faço questão de respeitar: o scaler é ajustado só no treino e depois aplicado no teste, nunca no conjunto inteiro de uma vez. Ajustar no dataset completo vazaria informação do teste para dentro do treino e inflaria os resultados de forma artificial.

**Modelagem.** Treino cinco algoritmos para comparar de verdade, não só os três pedidos: KNN, SVM com kernel RBF, Random Forest, Naive Bayes Gaussiano e Regressão Logística. KNN e SVM rodam sobre os dados normalizados, porque são sensíveis à escala das features. O Random Forest roda sobre os dados brutos, já que algoritmos baseados em árvore não se importam com a escala. Cada modelo é avaliado por acurácia, precisão, recall e F1, além de validação cruzada com cinco folds para garantir que o resultado não foi sorte de uma única divisão dos dados.

**Otimização.** Numa segunda passada, uso `GridSearchCV` com `StratifiedKFold` de cinco folds para procurar os melhores hiperparâmetros do KNN, do SVM e do Random Forest. Como o dataset é limpo e bem separável, o ganho da otimização tende a ser pequeno, e isso por si só já é uma conclusão: os modelos padrão já resolvem bem o problema, e investir em mais dados renderia mais do que torcer os hiperparâmetros.

**Avaliação e implantação.** No fim, interpreto o que o modelo aprendeu olhando a importância das features pelo índice de Gini no Random Forest e os coeficientes da Regressão Logística. O modelo escolhido é empacotado num `Pipeline` do scikit-learn junto com o scaler e exportado via `joblib`, pronto para receber uma amostra nova e devolver a variedade com a probabilidade de cada classe.

---

## Como executar

### Pré-requisitos

- Python 3.10 ou superior
- Jupyter Notebook ou Google Colab

### Instalação

```bash
pip install -r requirements.txt
```

### Rodando localmente

```bash
jupyter notebook LucasMichelsKuntz_RM570050_fase4_cap03_seeds.ipynb
```

### No Google Colab

Basta subir o arquivo `.ipynb`. O notebook tenta carregar os dados pelo pacote `ucimlrepo` e, se não conseguir, cai automaticamente no download direto do UCI, então funciona sem nenhuma configuração extra.

---

## Histórico de lançamentos

* 1.0.0 (18/06/2026)
    * Notebook CRISP-DM completo: análise exploratória, cinco classificadores comparados, otimização por Grid Search e pipeline de produção exportado

---

## Licença

<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1"><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1">

<p xmlns:cc="http://creativecommons.org/ns#" xmlns:dct="http://purl.org/dc/terms/">
  Este projeto está licenciado sob
  <a href="http://creativecommons.org/licenses/by/4.0/?ref=chooser-v1" target="_blank">Attribution 4.0 International</a>.
</p>
