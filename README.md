
# Aprendizado Automatizado de Máquina no Azure Machine Learning

experimento de Aprendizagem Automatizada, de Regressão, utilizando  Azure Machine Learning, realizado como desafio de projeto no Bootcamp Microsoft Azure AI Fundamentals da [https://www.dio.me/]()


## Use o aprendizado automático de máquina para treinar um modelo

O machine learning automatizado permite que você experimente vários algoritmos e parâmetros para treinar vários modelos e identificar o melhor para seus dados. Neste exercício, você usará um conjunto de dados de detalhes históricos de aluguel de bicicletas para treinar um modelo que prevê o número de aluguel de bicicletas que deve ser esperado em um determinado dia, com base em características sazonais e meteorológicas.

- Citação: Os dados utilizados neste exercício são derivados de[ Capital Bikeshare](https://capitalbikeshare.com/system-data) e é usado de acordo com os dados publicados [contrato de licença.](https://ride.capitalbikeshare.com/data-license-agreement)

Em [Estúdio Azure Machine Learning](https://ml.azure.com/), veja o `ML Automatizado página (abaixo Autoria).`

Crie um novo trabalho de ML automatizado com as seguintes configurações, usando Próximo conforme necessário para progredir na interface do usuário:

## Configurações básicas:

`Nome do trabalho:` mslearn-bike-automl

`Novo nome do experimento:` mslearn-bike-rental

`Descrição:` Aprendizado automatizado de máquina para previsão de aluguel de bicicletas

`Tags:` nenhum

`Tipo de tarefa e dados:`

**Configurações de tarefas:**

**Tipo de tarefa:** Regressão

**Conjunto de dados:** aluguel de bicicletas

**Coluna de destino:** Aluguel ( inteiro )

**Configurações de configuração adicionais:**

**Métrica primária:** Erro quadrado médio da raiz normalizado

**Explique o melhor modelo:** Não selecionado

**Use todos os modelos suportados:** Unselecionado. Você restrinja o trabalho para tentar apenas alguns algoritmos específicos.

**Modelos permitidos:** Selecionar apenas **RandomForest** e **LightGBM** — normalmente você quer tentar o maior número possível, mas cada modelo adicionado aumenta o tempo que leva para executar o trabalho.

**Limites:** Expanda esta seção

**Testes máximos:** 3

**Testes simultâneos máximos:** 3

**Nós máximos:** 3

**Limiar de pontuação métrica:** 0,085 (de modo que, se um modelo atingir uma pontuação média quadrática de erro métrico de raiz normalizada de 0,085 ou menos, o trabalho terminará.)

**Tempo limite:** 15

**Tempo limite de iteração:** 15

**Ativar a rescisão antecipada:** Selecionado

**Validação e teste:**

**Tipo de validação:** Divisão de validação de trem

**Percentagem de dados de validação:** 10

**Conjunto de dados de teste:** Nenhum

**Computação:**

**Selecione o tipo de computação:** Sem servidor

**Tipo de máquina virtual:** CPU

**Nível de máquina virtual:** Dedicado

**Tamanho da máquina virtual:** Standard_DS3_V2*

**Número de instâncias:** 1
* *Se sua assinatura restringir os tamanhos de VM disponíveis para você, escolha qualquer tamanho disponível.*

`Envie o trabalho de treinamento. Começa automaticamente.`

Espere o trabalho terminar. Pode demorar um pouco — agora pode ser um bom momento para uma pausa para o café!

## Reveja o melhor modelo

Quando o trabalho de aprendizado de máquina automatizado for concluído, você poderá revisar o melhor modelo treinado por ele.


1- No Visão geral guia do trabalho de aprendizado de máquina automatizado, observe o melhor resumo do modelo.

2- Selecione o texto em Nome do algoritmo para o melhor modelo para ver seus detalhes.

3 - Selecione o **Métricas** tab e selecione o **resíduos** e **predicted_true** gráficos se eles ainda não estiverem selecionados.

Revise os gráficos que mostram o desempenho do modelo. O **resíduos** o gráfico mostra o resíduos (as diferenças entre os valores previstos e reais) como um histograma. O **predicted_true** o gráfico compara os valores previstos com os valores verdadeiros.



## Implante e teste o modelo

1- No **Modelo** guia para o melhor modelo treinado pelo seu trabalho automatizado de aprendizado de máquina, selecione **Implantar** e usar o **Serviço web** opção para implantar o modelo com as seguintes configurações:

**Nome:** previsao-rentais

**Descrição:** Previsão de aluguel de ciclo

**Tipo de computação:** Instância do Container do Azure

**Ativar autenticação:** Selecionado

2- Aguarde o início da implantação - isso pode levar alguns segundos. O **Implantar status** para o **previsões-rentais** o endpoint será indicado na parte principal da página como Correndo.

3- Espere pelo **Implantar status** mudar para Sucedido. Isso pode levar 5-10 minutos.

## Teste o serviço implantado

 Agora você pode testar seu serviço implantado.

1- No estúdio Azure Machine Learning, no menu à esquerda, selecione **Endpoints** e abrir o **previsões-rentais** ponto final em tempo real.

2- No **previsão-rentais** página de ponto de extremidade em tempo real ver o **Teste** guia.

3- No **Dados de entrada para testar o endpoint painel**, substitua o modelo JSON pelos seguintes dados de entrada:

```
 {
   "Inputs": { 
     "data": [
       {
         "day": 1,
         "mnth": 1,   
         "year": 2022,
         "season": 2,
         "holiday": 0,
         "weekday": 1,
         "workingday": 1,
         "weathersit": 2, 
         "temp": 0.3, 
         "atemp": 0.3,
         "hum": 0.3,
         "windspeed": 0.3 
       }
     ]    
   },   
   "GlobalParameters": 1.0
 }
 
```

4- Clique no Teste botão.

5- Revise os resultados do teste, que incluem um número previsto de aluguéis com base nos recursos de entrada - semelhante a isso:

```
 {
   "Results": [
     444.27799000000000
   ]
 }
 ```
