# Manuten-o-Preditiva-na-Ind-stria-4.0.ipynb
Projeto avaliativo da SCTEC desenvolvido no Google Colab.
markdown
# Manutenção Preditiva na Indústria 4.0

## 📋 Sobre o Projeto
Este projeto consiste no desenvolvimento de um Pipeline de Ciência de Dados ponta a ponta construído em Python e executado no ambiente Google Colab. O sistema é aplicado ao contexto da Indústria 4.0, utilizando dados históricos de sensores para prever de forma precoce quebras mecânicas em equipamentos de um parque fabril, reduzindo custos com paradas não planejadas na linha de produção. A variável alvo do projeto é binária: `Falha = 1` (avaria detectada) e `Falha = 0` (funcionamento normal).

## 📊 Estrutura do Pipeline de Machine Learning (Fases 1 a 7)

### Fase 1: Análise Exploratória (EDA)
Inspeção estrutural da base histórica para identificação das dimensões do dataset, tipos de dados e resumo estatístico descritivo gerado via método `.describe()`. A análise conta com três gráficos fundamentados:
* Histograma de distribuição das variáveis preditoras (sensores).
* Gráfico de barras avaliando a taxa de desbalanceamento severo da variável alvo.
* Mapa de calor com o coeficiente de correlação de Pearson para avaliar a colinearidade dos atributos.

### Fase 2: Limpeza e Tratamento de Dados (Data Prep)
* Identificação e remoção física de linhas duplicadas para mitigar redundâncias.
* Tratamento de dados ausentes utilizando a técnica de imputação pela **Mediana** (escolha justificada tecnicamente devido à forte presença de outliers isolados pelas caixas de *boxplot*, evitando a distorção que a média sofreria).

### Fase 3: Feature Engineering
Construção de uma nova variável numérica chamada **Potência**, obtida de forma vetorizada pela relação matemática entre colunas preexistentes sugerida pelo departamento de engenharia:
`potencia = velocidade_rotacao_rpm * torque_nm`

### Fase 4: Divisão e Balanceamento dos Dados
* Separação estrita dos atributos previsores (X) e da variável alvo (y).
* Divisão dos dados nos conjuntos de treino (80%) e teste (20%) utilizando amostragem estratificada (`stratify=y`) para preservar a proporção da classe minoritária.
* Aplicação da técnica de reamostragem **SMOTE** realizada exclusivamente nos dados de treino para evitar o vazamento de dados (*Data Leakage*).

### Fase 5: Escalonamento de Variáveis
Aplicação da padronização estatística `StandardScaler` apenas para as variáveis numéricas contínuas destinadas ao modelo KNN, executando `fit_transform` no treino e `transform` no teste. Os dados para a Árvore de Decisão foram mantidos em sua escala original, dado que o algoritmo de árvore realiza quebras ortogonais por limiares e é intrinsecamente imune à escala dos atributos.

### Fase 6: Ajuste de Parâmetros e Combate ao Overfitting
* **KNN**: Treinamento avaliado variando o parâmetro de vizinhos por três valores ímpares (K = 3, 5, 7).
* **Árvore de Decisão**: Treinamento avaliado variando o parâmetro de profundidade máxima em três limites (`max_depth = 3`, `5` e `None`). A configuração sem limite gerou um cenário clássico de *overfitting* (100% de acerto no treino e queda drástica no teste), corrigido por meio da técnica de poda.

### Fase 7: Avaliação da Acurácia e Veredito Final
Cálculo e exibição das métricas de acurácia de ambos os modelos utilizando o conjunto de testes isolado, gerando a conclusão comparativa que justifica qual modelo deve ser embarcado na fábrica.

## 🛠️ Tecnologias e Bibliotecas Utilizadas
* Python 3.10+
* Google Colab (Ambiente de Desenvolvimento)
* Pandas (Manipulação de DataFrames)
* NumPy (Operações matemáticas e vetorização)
* Matplotlib & Seaborn (Visualização de dados e gráficos)
* Scikit-Learn (Modelagem preditiva e pré-processamento)
* Imbalanced-Learn (Balanceamento via SMOTE)

## 🚀 Como Executar o Sistema
1. Acesse o [Google Colab](https://colab.research.google.com/drive/1RKa7TNKBlQPu4r9oSDLjcbfNx4p8HgAh#scrollTo=SXvIw_E86-Ax).
2. Abra o notebook Jupyter contendo o código estruturado.
3. O script fará a requisição automática dos dados diretamente do repositório estável da UCI Machine Learning Repository através da URL oficial, dispensando uploads manuais e eliminando falhas de arquivos locais ausentes.
4. Execute as células em ordem sequencial para processar o pipeline das 7 fases.

## 🎥 Vídeo de Demonstração
* [Link do vídeo explicativo hospedado no Google Drive](https://drive.google.com/file/d/1J4b1HSjK1vikC8GOc3y2HYdTc-OqBaYJ/view?usp=sharing)

---
*Projeto individual desenvolvido para a Situação de Aprendizagem de IA — SCTEC.*
*Módulo 01 - Semana 14.*
