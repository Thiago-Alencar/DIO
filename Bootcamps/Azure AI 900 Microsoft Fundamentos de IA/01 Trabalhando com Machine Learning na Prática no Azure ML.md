# Criação de um Modelo de Previsão com Azure Machine Learning e Configuração de Pontos de Extremidade

Este guia detalha como criar um modelo de machine learning para prever aluguéis de bicicletas usando o Azure Machine Learning, e como implantar e testar o modelo.

## 1. Criar um Workspace do Azure Machine Learning

Antes de tudo, você precisará de um workspace do Azure Machine Learning. Siga estas etapas:

1.  **Acesse o portal do Azure** em [https://portal.azure.com](https://portal.azure.com) usando suas credenciais da Microsoft [1].
2.  Selecione **+ Criar um recurso**, procure por *Machine Learning* e crie um novo recurso **Azure Machine Learning** [1].
3.  Configure as seguintes opções [1]:
    *   **Assinatura**: *Sua assinatura do Azure*.
    *   **Grupo de recursos**: *Crie ou selecione um grupo de recursos*.
    *   **Nome**: *Insira um nome único para seu workspace*.
    *   **Região**: Leste dos EUA.
    *   **Conta de armazenamento**: *Anote a nova conta de armazenamento padrão que será criada para seu workspace*.
    *   **Cofre de chaves**: *Anote o novo cofre de chaves padrão que será criado para seu workspace*.
    *   **Application Insights**: *Anote o novo recurso do Application Insights padrão que será criado para seu workspace*.
    *   **Registro de contêiner**: Nenhum (um será criado automaticamente na primeira vez que você implantar um modelo em um contêiner).
4.  Selecione **Revisar + criar** e depois **Criar**. Aguarde a criação do workspace e vá para o recurso implantado [1].
5.  No seu recurso de workspace do Azure Machine Learning, selecione **Iniciar estúdio** ou acesse [https://ml.azure.com](https://ml.azure.com) e faça login usando sua conta Microsoft [2].

## 2. Treinar um Modelo com Automated Machine Learning

Agora, você usará o recurso de aprendizado de máquina automatizado para treinar um modelo:

1.  No Azure Machine Learning Studio, vá para a página **Automated ML** (em **Criação**) [3].
2.  Crie um novo trabalho Automated ML com as seguintes configurações [3-6]:
    *   **Configurações básicas**:
        *   **Nome do trabalho**: Mantenha o nome pré-preenchido.
        *   **Novo nome do experimento**: mslearn-bike-rental.
        *   **Descrição**: Aprendizado de máquina automatizado para previsão de aluguel de bicicletas.
        *   **Tags**: *nenhuma*.
    *   **Tipo de tarefa e dados**:
        *   **Selecionar tipo de tarefa**: Regressão.
        *   **Selecionar conjunto de dados**: Crie um novo conjunto de dados com as seguintes configurações:
            *   **Nome**: bike-rentals
            *   **Descrição**: Dados históricos de aluguel de bicicletas
            *  **Tipo**: Tabela (mltable)
            *   **Fonte de dados**: Selecione **De arquivos locais**
             *  **Tipo de armazenamento de destino**: Azure Blob Storage
             *  **Nome**: workspaceblobstore
            *   **Seleção MLtable**:
               *   **Carregar pasta**: *Baixe e descompacte a pasta que contém os dois arquivos que você precisa carregar* [https://aka.ms/bike-rentals](https://aka.ms/bike-rentals)
    *   **Configurações da tarefa**:
        *   **Tipo de tarefa**: Regressão
        *   **Conjunto de dados**: bike-rentals
        *   **Coluna de destino**: rentals (inteiro)
    *   **Configurações adicionais**:
        *   **Métrica primária**: NormalizedRootMeanSquaredError
        *   **Explicar melhor modelo**: *Desmarcado*
        *   **Habilitar empilhamento de conjuntos**: *Desmarcado*
        *   **Usar todos os modelos suportados**: Desmarcado. Restrinja o trabalho para tentar apenas alguns algoritmos específicos.
        *   **Modelos permitidos**: Selecione apenas **RandomForest** e **LightGBM**.
        *  **Limites**:
           *  **Máximo de tentativas**: 3
           *  **Máximo de tentativas simultâneas**: 3
           *  **Máximo de nós**: 3
            *   **Limite de pontuação da métrica**: 0.085.
            *   **Tempo limite do experimento**: 15.
            *  **Tempo limite da iteração**: 15.
           *  **Habilitar encerramento antecipado**: *Selecionado*
    *   **Validação e teste**:
        *   **Tipo de validação**: Divisão treino-validação
        *   **Porcentagem de dados de validação**: 10
        *   **Conjunto de dados de teste**: Nenhum
    *   **Compute**:
        *  **Selecionar tipo de compute**: Serverless
        *  **Tipo de máquina virtual**: CPU
        *   **Nível da máquina virtual**: Dedicado
        *   **Tamanho da máquina virtual**: Standard\_DS3\_V2
        *   **Número de instâncias**: 1
3.  Envie o trabalho de treinamento. Ele iniciará automaticamente. Aguarde a conclusão do trabalho [6].

## 3. Revisar o Melhor Modelo

Após a conclusão do trabalho de aprendizado de máquina automatizado, revise o melhor modelo:

1.  Na guia **Visão geral** do trabalho de aprendizado de máquina automatizado, observe o resumo do melhor modelo [7].
2.  Selecione o texto em **Nome do algoritmo** para o melhor modelo para ver seus detalhes [7].
3.  Selecione a guia **Métricas** e selecione os gráficos **resíduos** e **predicted\_true**, se ainda não estiverem selecionados [7].
4.  Revise os gráficos que mostram o desempenho do modelo [7].

## 4. Implantar e Testar o Modelo

Implante o modelo treinado como um serviço web:

1.  Na guia **Modelo** do melhor modelo, selecione **Implantar** e use a opção **Ponto de extremidade em tempo real** [8].
2.  Configure as seguintes opções de implantação [8]:
    *   **Máquina virtual**: Standard_DS3_v2
    *  **Contagem de instâncias**: 3
    *   **Ponto de extremidade**: Novo
    *   **Nome do ponto de extremidade**: Deixe o padrão ou certifique-se de que seja globalmente exclusivo.
    *   **Nome da implantação**: Deixe o padrão.
    *  **Coleta de dados de inferência**: *Desabilitado*
    *  **Pacote de modelo**: *Desabilitado*
3.  Aguarde o início da implantação e a alteração do **Status da implantação** para *Bem-sucedido*. Isso pode levar de 5 a 10 minutos [9].
4.  Após a implantação, selecione **Endpoints** no menu esquerdo e abra o ponto de extremidade em tempo real **predict-rentals** [9].
5.  Na página do ponto de extremidade, vá para a guia **Testar** [9].
6.  No painel **Dados de entrada para testar o ponto de extremidade**, substitua o JSON de modelo pelos seguintes dados de entrada [10]:
    ```json
    {
    "input_data": {
        "columns": [
            "day",
            "mnth",
            "year",
            "season",
            "holiday",
            "weekday",
            "workingday",
            "weathersit",
            "temp",
            "atemp",
            "hum",
            "windspeed"
        ],
        "index": [
            0
        ],
        "data": [
            [
                1,
                1,
                2022,
                2,
                0,
                1,
                1,
                2,
                0.3,
                0.3,
                0.3,
                0.3
            ]
        ]
    }
    }
    ```
7.  Clique no botão **Testar**. Analise os resultados do teste [10].

## 5. Limpar os Recursos

Para evitar custos desnecessários, exclua o ponto de extremidade e o workspace se não os precisar mais:

1.  Na guia **Endpoints**, selecione o ponto de extremidade **predict-rentals**. Em seguida, selecione **Excluir** [11].
2.  Para excluir seu workspace, acesse a página **Grupos de recursos** no portal do Azure, abra o grupo de recursos que você especificou ao criar seu workspace e clique em **Excluir grupo de recursos** [12].
3. Links
https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/01-machine-learning.html
https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/02-content-safety.html
