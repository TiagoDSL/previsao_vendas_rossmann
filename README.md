
![Rossmann_Logo svg](https://github.com/TiagoDSL/previsao_vendas_rossmann/assets/99509388/5386f439-16a9-4f6b-88e1-9b53a8f8f130)

# Previsão de Vendas da Rede de Farmácia ROSSMANN

## Descrição

A Rossmann é uma rede de farmácias e drogarias da Europa, fundada na Alemanha em 1972 por Dirk Rossman. A empresa oferece uma ampla gama de produtos, 
incluindo medicamentos, produtos de beleza, cuidados pessoais, higiene, entre outros. Com milhares de lojas espalhadas pela Alemanga e outros países europeus, 
a rede continua a expandir.

Esse projeto fictício foi inspirado no desafio "Rossmann Store Sales" (https://www.kaggle.com/c/rossmann-store-sales), 
onde a emporesa disponiblizou dados de vendas de suas filiais na plataforma Kaggle.

## Probleman de Negócio
O CEO da Rossmann planeja reformar as lojas para melhorar a estrutura e o atendimento. Para isso, ele informou que precisa das previsoes da receita das 
próximas 6 semanas de cada loja, para determinar o investimento necessário em cada uma delas.

Atualmente, as previsões são feitas pelos gerentes individualemnte e manualmente por loja, resultando em variações significativas devido a fatores como promoções, 
concorrencia, feriados e sazonalidades, o que torna os resultados inconsistentes.

Este projeto visa auxiliar o CEO na tomada de decisões, fornecendo previsões automaticas para cada loja e permitindo que ele 
consulte essas previsões através de um Bot no Telegram.

## Entendimento do Negócio

Tendo em vista que o CEO planeja realizar investimentos para reformar as lojas, é necessário obter uma previsão de quanto elas irão faturar nas 
próximas 6 semanas. O projeto caracteriza-se como um problema de predição.

### Premissas de Negócio
Para contruir a solução, as seguintes premissas foram consideradas:
- A previsão considerará apenas as lojas que tiveram vendas superiores a 0 nos dados disponíveis;
- os dias em que as lojas estiveram fechadas serão excluídos da previsão;
- Lojas sem informações sobre competidores próximos terão a distância fixada em 200.000 metros.


### Estreategia da solução 
Para assegurar uma entrega rápida e eficiente da primeira solução, agregando valor à empresa e permitindo decisões ágeis por parte do CEO,
foi adotado o método CRISP-DM.

![ciclo_CRISP](https://github.com/TiagoDSL/previsao_vendas_rossmann/assets/99509388/cd85b14b-09dd-4a67-bbdc-310c7ab13bd3)


O CRISP-DM (Cross-Industry Standard Process for Data Mining) é uma metodologia padrão amplamente utilizada para projetos de mineração de dados. 
Ele define seis fases principais:

- **Entendimento do Problema de Negócio:** Definir o problema a ser resolvido, como solicitado pelo responsável.
- **Entendimento do Negócio:** Compreender a necessidade real do dono do problema e validar protótipos de solução.
- **Coleta de Dados:** Extrair dados das fontes disponíveis, como bancos de dados da empresa.
- **Limpeza dos Dados:** Remover inconsistências nos dados para garantir qualidade e evitar impactos negativos nos modelos de Machine Learning.
- **Exploração dos Dados:** Analisar e explorar os dados para criar hipóteses de negócio acionáveis e novas features para a modelagem.
- **Modelagem dos Dados:** Preparar os dados para aplicação de algoritmos de Machine Learning, incluindo transformações e encoding.
- **Aplicação de Algoritmos de Machine Learning:** Selecionar, aplicar e comparar algoritmos para escolher o mais adequado baseado na performance.
- **Avaliação de Performance:** Avaliar o desempenho do algoritmo escolhido em relação aos resultados esperados de negócio. Se aceitável, o algoritmo é publicado; caso contrário, o processo retorna para ajustes.
- **Publicação da Solução:** Disponibilizar a solução final para uso, proporcionando valor tangível à empresa.

## Coleta de Dados
Os dados de origem pública foram coletados através da plataforma Kaggle.
Arquivos coletados:

- **train.csv:** dados históricos incluindo vendas.
- **test.csv:** dados históricos excluindo vendas.
- **store.csv:** informações complementares sobre as lojas.

O conjunto de dados é composto 1.017.209 linhas, cada linha representa um dia de vendas numa determinada loja em um período de 2 anos e 7 meses.
É composto também por 18 colunas, cada uma representa uma característica da venda e/ou da loja.

Para mais detalhes sobre os dados, acesse https://www.kaggle.com/c/rossmann-store-sales/data.


## Limpeza dos Dados
Após a coleta e carregamento dos dados, foi realizada uma limpeza que incluiu a renomeação das colunas para snake case, 
tratamento de valores nulos e ausentes, conversão de formatos de data e números, além da aplicação de estatísticas descritivas. 

Algumas features, como dados de competidores e promoções, apresentaram altos percentuais de valores nulos (cerca de 30% -50% ), 
mas esses valores foram considerados significativos no contexto do negócio. Por exemplo, valores nulos em "competition_distance" indicavam a ausência de 
competidores próximos e foram preenchidos com o valor de 200.000 metros distância. 
Para resolver o problema de valores zerados de vendas, seja por dias em que as lojas estavam fechadas ou algum outro motivo, 
as linhas correspondentes foram removidas, representando cerca de 17% da base de dados.

## Analise Exproratoria dos Dados (EDA)
A Analise Exproratoria dos Dados visa principalmente a criação ou derivação de novas variáveis, a formulação e validação de hipóteses de negócio, e a identificação das variáveis que influenciam a variável resposta, no caso desse projeto, as vendas.

Durante a Analise Exproratoria também é feita a Feature Engineering com a criação de novas variáveis que ajudem a melhorar a perfomance do modelo de Machine Learning. Durante o projeto, nessa etapa foi separado a data em novas variáveis temporais, como semanas do ano, dia, mes, ano, etc.

Para orientar a Anallise Exploratória, foi criado hipoetes com a ajuda de um Mindmap, com a finalidade de ser ter um entendimento maior sobre o negócio.

![mind_map_hip](https://github.com/TiagoDSL/previsao_vendas_rossmann/assets/99509388/bcdcb01c-d62e-4086-a69b-cd1faeb222c7)


As principais hipoteses que foram testadas:
**1.** Lojas com maior sortimentos deveriam vender mais.

**2.** Lojas com competidores mais próximos deveriam vender menos.

**3.** Lojas com competidores à mais tempo deveriam vendem mais.

**4.** Lojas com promoções ativas por mais tempo deveriam vender mais.

**5.** Lojas com mais dias de promoção deveriam vender mais.

**6.** Lojas com mais promoções consecutivas deveriam vender mais. 

**7.** Lojas abertas durante o feriado de Natal deveriam vender mais.

**8.** Lojas deveriam vender mais ao longo dos anos.

**9.** Lojas deveriam vender mais no segundo semestre do ano.

**10.** Lojas deveriam vender mais depois do dia 10 de cada mês.

**11.** Lojas deveriam vender menos aos finais de semana.

**12.** Lojas deveriam vender menos durante os feriados escolares.


 
###  Análise Univariada 
Na analise univariada, foi realizado a pltagem de um gráfico para que pudesse ter um melhor entendimento da distribuição das váriaveis.

  [imagem histograma]

###  Análise Bivariada

A análise bivariada (comparando uma variável explicativa com a variável resposta) foi utilizada para verificar as hipóteses de negócio previamente definidas no mapa mental de hipóteses. Além disso, extraímos insights importantes sobre o negócio com base nos resultados encontrados.

Principais insights sobre o negócio:

- **Lojas com competidores mais próximos vendem mais** (Essa observação indica que a concorrência é mais intensa para estabelecimentos próximos a shoppings e galerias):

![H2](https://github.com/TiagoDSL/previsao_vendas_rossmann/assets/99509388/5f334646-9752-4716-bed0-14ab007ec47e)

- **Lojas com mais promoções consecutivas vendem menos**:
  
![H3](https://github.com/TiagoDSL/previsao_vendas_rossmann/assets/99509388/df9827d9-d0bd-4216-ad6a-83c0749dfb55)

- **Lojas vendem menos nos finais de semana**:

![H5](https://github.com/TiagoDSL/previsao_vendas_rossmann/assets/99509388/11751920-7e6e-45c4-80be-e95b049570e4)

Leg: **1**: Segunda; **2**: Terça; **3**: Quarta; **4**: Quinta; **5**: Sexta; **6**: Sábado; **7**: Domingo.


### Analise multivariada
Com a análise multivariada conseguimos identificar quais variáveis têm um impacto significativo na predição das vendas. Além disso, ela ajuda a entender quais variáveis estão mais correlacionadas entre si, o que é importante para detectar multicolinearidade, um fenômeno que pode afetar a precisão dos modelos. Neste caso, utilizamos a correlaçao de Pearson.

![correlacao](https://github.com/TiagoDSL/previsao_vendas_rossmann/assets/99509388/cec2a065-e70e-4398-a1b0-086cbdfdaaeb)


## Modelagem dos Dados
Na etapa de modelagem dos dados, os dados foram preparados para o modelo de Machine Learning. Isso envolveu transformações como encoding (convertendo variáveis categóricas em numéricas) e rescaling (ajustando variáveis para a mesma escala, eliminando desproporções que podem afetar o modelo). Não foi necessário aplicar normalização, pois não foi identificada a necessidade de ajustar a distribuição dos dados.

## Seleção de Features 
Nessa etapa de seleção de features, foi utilizada um modelo de Random Forest para a seleção de features mais relevantes. Na seleção de features com Random Forest, várias árvores de decisão são construídas usando diferentes conjuntos de variáveis. Cada árvore calcula a importância das variáveis ao prever os resultados. As variáveis mais importantes são identificadas com base na contribuição para a precisão do modelo, ajudando a eliminar aquelas menos relevantes ou redundantes. Isso melhora a eficiência e a precisão das previsões sem depender de abordagens como o Boruta, que usa permutações aleatórias para comparação.

## Algoritmos de Machine Learning 
Dado que o problema do projeto envolve regressão, optamos por selecionar os seguintes modelos de machine learning para avaliar seu desempenho nos dados e prever resultados com maior precisão:
- Avarege Model (usado para ser ter um bass line de perfomance);
- Linear Regression;
- Linear Regression - Lasso;
- Random Forest Regressor.

### Cross-validation 
Para realizar a técnica de cross-validation, as últimas 30 semanas do conjunto de dados de treino foram reservadas. 
Nessa abordagem, os dados de validação são divididos em blocos, sendo que cada bloco atua como conjunto de teste em um ciclo. 
Após a avaliação, o bloco volta a ser incorporado aos dados de treino. Dessa forma, cada conjunto de 6 semanas é utilizado como conjunto de teste em algum momento durante a avaliação do modelo. 
A principal vantagem dessa técnica é aumentar a confiabilidade na medição dos modelos, garantindo que a performance não dependa exclusivamente de um único conjunto específico de dados.

![cross_val](https://github.com/TiagoDSL/previsao_vendas_rossmann/assets/99509388/ce76f7d1-3dd3-450f-b952-d5b1a0aaacd8)


## Avaliação de Performance dos Modelos de Machine Learning 
Para avaliar a perfomance dos modelos, foram utilizadas as seguintes métricas:
- **MAE** (Mean Absolute Error): Calcula a média absoluta dos erros de previsão em relação aos valores originais.
- **MAPE** (Mean Absolute Percentage Error): Mede o erro médio em termos de porcentagem em relação aos valores reais.
- **RMSE** (Root Mean Square Error): Calcula a raiz quadrada da média dos quadrados dos erros. Esta métrica penaliza erros maiores de forma mais severa, proporcionando uma comparação mais rigorosa entre modelos.

Apos rodas os modelos e realizar a aplicaçlão do Cross-Validations, a perfomance apresentada pelos modelos foi a seguinte:

   ![performance-pos-cross](https://github.com/TiagoDSL/previsao_vendas_rossmann/assets/99509388/ee454a0d-e26a-4cb1-9050-39da44b4bef0)


### Escolha do modelo
Por ter apresentado a melhor perfomance, o modelo escolhido foi a Random Forest Regressor. 
Apesar de ser um modelo demorado e que ocupa um espaço maior em comparação a putros algoritmos que não foram testados.

## Ajuste de Hiperparâmetros
Foi realizado um ajuste de parâmetros do modelo Random Forest Regressor utilizando a técinca de Random Search.
Em vez de testar todas as combinações possíveis de hiperparâmetros, o que pode ser computacionalmente caro, 
o random search seleciona aleatoriamente combinações para avaliação. Isso pode levar a resultados eficientes em termos de tempo e recursos, 
frequentemente encontrando boas soluções sem a necessidade de explorar todas as opções disponíveis.

## Desempenho do Algoritmo
Ao analisarmos o gráfico de desempenho do algoritmo, podemos observar que os dois primeiros gráficos abaixo mostram que o modelo consegue capturar o comportamento cíclico das vendas. 
No entanto, também é evidente que em alguns períodos a taxa de erro é mais elevada.

Nos dois últimos gráficos, a distribuição das previsões parece seguir uma distribuição normal. 
No quarto gráfico, notamos que muitas previsões se destacam das outras, indicando a presença de valores discrepantes.

![desempenho](https://github.com/TiagoDSL/previsao_vendas_rossmann/assets/99509388/557922d2-83fb-4955-a7df-0441b5b6e2e2)


## Perfomance Final do Modelo apos o Ajuste
Rersultado final do algoritmo após todos os ajustes e validações:

![imagem-result-final-rf](https://github.com/TiagoDSL/previsao_vendas_rossmann/assets/99509388/3982096e-692b-4a7a-b086-fd2d32f19639)


## Tradução do modelo para o resultado do negocio
Além de desenvolver um algoritmo preciso para previsões, é crucial para nós, cientistas de dados, traduzir os resultados do algoritmo em termos financeiros. Dessa forma, apresentamos os resultados do modelo para a equipe de negócios. Definimos diferentes cenários baseados nas previsões, proporcionando uma visão clara para a tomada de decisões estratégicas.

![cenarios](https://github.com/TiagoDSL/previsao_vendas_rossmann/assets/99509388/4e96f382-2970-40aa-8061-b9a90cb35d20)



## Conclusão
Ao concluir esta primeira aplicação do método CRISP-DM para este projeto, podemos prever que as 1.115 lojas da rede Rossmann faturarão aproximadamente R$ 290 milhões nas próximas seis semanas, com um erro aproximado de 12,4%.

O modelo conseguiu capturar bem o comportamento das vendas na maioria das lojas, embora o desempenho não tenha sido uniforme em todas elas. Seria interessante para o CEO priorizar as lojas que apresentaram melhor desempenho.

## Proximos Passos
- Realizar a criação de um bot no telegram para que o CEO possa consultar as previsoes da lojas;
- Realizar o teste de outros algoritmons de macinhe learning e observar se a perfomance irá melhorar;
- Realizar uma investigação para identificar as possíveis causas de algumas lojas nao terem um bom desempenho nas previsoes;
- Criar novas variáveis que possam contribuir para o desempenho do modelo, sem comprometer a dimensionalidade;
- Realizar o levantamentos de novas hipoteses, a fim de identificar novos insights;
- Resolver o problema de data leakage.

## Tecnologias Utilizadas 

<img src="https://img.shields.io/badge/mac%20os-000000?style=for-the-badge&logo=apple&logoColor=white" alt="Mac OS badge"> 
<img src="https://img.shields.io/badge/conda-342B029.svg?&style=for-the-badge&logo=anaconda&logoColor=white">
<img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white"> 
<img src="https://img.shields.io/badge/Vscode-007ACC?style=for-the-badge&logo=visual-studio-code&logoColor=white">
<img src="https://img.shields.io/badge/Jupyter-F37626.svg?&style=for-the-badge&logo=Jupyter&logoColor=white">
<img src="https://img.shields.io/badge/NumPy-013243.svg?style=for-the-badge&logo=NumPy&logoColor=white">
<img src="https://img.shields.io/badge/pandas-150458.svg?style=for-the-badge&logo=pandas&logoColor=white">
<img src="https://img.shields.io/badge/scikitlearn-F7931E.svg?style=for-the-badge&logo=scikit-learn&logoColor=white">
<img src="https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white">
<img src="https://img.shields.io/badge/Kaggle-20BEFF?style=for-the-badge&logo=Kaggle&logoColor=white">

- Seaborn: :bar_chart: 
- Matplotlib: :chart_with_upwards_trend: 
