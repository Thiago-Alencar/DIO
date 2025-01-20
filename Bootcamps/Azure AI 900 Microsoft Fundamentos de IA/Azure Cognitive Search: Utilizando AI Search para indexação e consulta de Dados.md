# Configuração de Pesquisa com Azure AI Search e Análise de Dados

Este guia detalha como configurar uma solução de pesquisa usando o **Azure AI Search**, enriquecendo dados com **Azure AI services** e armazenando os resultados, além de explorar os insights e possibilidades aprendidos durante o processo.

## 1. Criação dos Recursos no Azure

Antes de iniciar, é necessário criar alguns recursos no Azure.

1.  **Acesse o portal do Azure** em [https://portal.azure.com](https://portal.azure.com).
2.  **Crie um recurso do Azure AI Search:** [1]
    *   Clique em **+ Criar um recurso** e procure por *Azure AI Search*.
    *   Selecione **Azure AI Search** e clique em **Criar**.
    *   Configure o recurso com os seguintes parâmetros:
        *   **Assinatura**: *Sua assinatura do Azure*.
        *   **Grupo de recursos**: *Crie ou selecione um grupo de recursos com um nome único*.
        *   **Nome do serviço**: *Um nome único para o serviço*.
        *   **Localização**: *Escolha uma região disponível*.
        *   **Nível de preço**: *Básico*.
    *   Clique em **Revisar + criar** e depois em **Criar**.
3.  **Crie um recurso do Azure AI services:** [2]
    *   Volte para a página inicial do portal e clique em **+ Criar um recurso**.
    *   Procure por *Azure AI services* e clique em **Criar**.
    *   Configure o recurso com os seguintes parâmetros:
        *   **Assinatura**: *Sua assinatura do Azure*.
        *   **Grupo de recursos**: *O mesmo grupo de recursos do Azure AI Search*.
        *   **Região**: *A mesma localização do Azure AI Search*.
        *   **Nome**: *Um nome único para o serviço*.
        *  **Nível de preço**: *Standard S0*.
        *   Marque a caixa confirmando que você leu os termos.
    *   Clique em **Revisar + criar** e depois em **Criar**.
4.  **Crie uma conta de armazenamento:** [3]
    *   Volte para a página inicial do portal e clique em **+ Criar um recurso**.
    *   Procure por *Storage account* e clique em **Criar**.
    *   Configure o recurso com os seguintes parâmetros:
        *   **Assinatura**: *Sua assinatura do Azure*.
        *   **Grupo de recursos**: *O mesmo grupo de recursos dos outros recursos*.
        *   **Nome da conta de armazenamento**: *Um nome único*.
        *   **Localização**: *Qualquer localização disponível*.
        *   **Performance**: *Standard*.
        *   **Redundância**: *Armazenamento localmente redundante (LRS)*.
    *   Clique em **Revisar** e depois em **Criar**.
    *   Após a criação, acesse a conta de armazenamento, selecione **Configuração** e habilite o *Acesso anônimo de blob*. [4]

## 2. Upload de Documentos para o Azure Storage

1.  Na sua conta de armazenamento, selecione **Containers** no menu lateral esquerdo. [5]
2.  Clique em **+ Container** e crie um container chamado `coffee-reviews` com o nível de acesso público definido como *Container (acesso anônimo de leitura para containers e blobs)*.
3.  Baixe os arquivos de reviews de café compactados de [https://aka.ms/mslearn-coffee-reviews](https://aka.ms/mslearn-coffee-reviews), e extraia para a pasta `reviews`.
4.  No portal do Azure, selecione o container `coffee-reviews`, clique em **Upload** e carregue todos os arquivos da pasta `reviews`. [6]

## 3. Indexação dos Documentos

1.  No portal do Azure, acesse o recurso do **Azure AI Search**. [7]
2.  Na página de *Visão geral*, clique em **Importar dados**.
3.  Na página *Conectar aos seus dados*, selecione **Azure Blob Storage** como fonte de dados e configure:
    *   **Fonte de dados**: *Azure Blob Storage*.
    *   **Nome da fonte de dados**: `coffee-customer-data`.
    *   **Dados a serem extraídos**: *Conteúdo e metadados*.
    *   **Modo de análise**: *Padrão*.
    *   **String de conexão**: *Selecione sua conta de armazenamento e o container* `coffee-reviews`.
    *   **Autenticação de identidade gerenciada**: *Nenhum*.
    *   **Nome do container**: *Preenchido automaticamente após a conexão*.
    *   **Pasta Blob**: *Deixe em branco*.
    *   **Descrição**: *Reviews para as lojas Fourth Coffee*.
4.  Clique em **Próximo: Adicionar habilidades cognitivas (Opcional)**. [8]
5.  Na seção *Anexar serviços de IA*, selecione seu recurso do Azure AI services.
6.  Na seção *Adicionar enriquecimentos*:
    *   Altere o **Nome do conjunto de habilidades** para `coffee-skillset`.
    *   Marque a caixa **Habilitar OCR e mesclar todo o texto no campo merged\_content**.
    *   Garanta que o **Campo de dados de origem** esteja definido para `merged_content`.
    *   Altere o **Nível de granularidade de enriquecimento** para *Páginas (chunks de 5000 caracteres)*.
    *   Não marque *Habilitar enriquecimento incremental*.
7. Selecione os seguintes campos enriquecidos: [9]
    *   `locations`
    *    `keyphrases`
    *   `sentiment`
    *    `imageTags`
    *    `imageCaption`
8.  Em **Salvar enriquecimentos em um armazenamento de conhecimento**, selecione:
    *   *Projeções de imagem*.
    *   *Documentos*.
    *   *Páginas*.
    *   *Frases-chave*.
    *   *Entidades*.
    *   *Detalhes da imagem*.
    *   *Referências de imagem*.
    *   Selecione sua conta de armazenamento como string de conexão.
9.  Crie um novo container chamado `knowledge-store` com nível de privacidade `Privado`, e selecione-o. [10]
10. Selecione `Azure blob projections: Document` e mantenha o nome do container `knowledge-store` auto preenchido.
11. Clique em **Próximo: Personalizar índice de destino**. Altere o **Nome do índice** para `coffee-index`.
12. Garanta que a **Chave** seja `metadata_storage_path`. Deixe `Nome do sugestor` em branco.
13. Selecione **filterable** para os seguintes campos: `content`, `locations`, `keyphrases`, `sentiment`, `merged_content`, `text`, `layoutText`, `imageTags`, `imageCaption`. [11]
14. Clique em **Próximo: Criar um indexador**.
15. Altere o **Nome do indexador** para `coffee-indexer`.
16. Deixe o **Agendamento** definido como *Uma vez*.
17. Expanda **Opções avançadas** e certifique-se de que a opção **Chaves de codificação Base-64** esteja selecionada.
18. Clique em **Enviar** para criar a fonte de dados, conjunto de habilidades, índice e indexador. [12]
19. Após a execução do indexador, volte à página do recurso do Azure AI Search, selecione **Indexadores**, e confirme se o status do `coffee-indexer` é *Sucesso*.

## 4. Consulta do Índice

1.  Na página de visão geral do seu serviço de pesquisa, clique em **Search explorer**. [13]
2.  Certifique-se de que o índice selecionado seja o `coffee-index`.
3.  Altere a *visualização* para **Visualização JSON**.
4.  Na seção *Editor de consulta JSON*, execute as seguintes consultas: [14, 15]
    *   Para retornar todos os documentos:
        ```json
        { "search": "*", "count": true }
        ```
    *   Para filtrar por localização:
        ```json
        { "search": "locations:'Chicago'", "count": true }
        ```
    *   Para filtrar por sentimento negativo:
        ```json
        { "search": "sentiment:'negative'", "count": true }
        ```

## 5. Análise do Knowledge Store

1.  Acesse sua conta de armazenamento e selecione **Containers**. [16]
2.  Selecione o container `knowledge-store` e explore as pastas que contém os metadados de cada documento. Selecione um arquivo `objectprojection.json` para ver o JSON produzido por um dos documentos. [17]
3.  Retorne aos containers, selecione `coffee-skillset-image-projection` e examine as imagens salvas de cada documento.
4.  No menu lateral esquerdo, selecione **Storage browser**, e depois **Tabelas**.
5.  Selecione a tabela `coffeeSkillsetKeyPhrases` para ver as frases-chave extraídas do conteúdo. [18]

## 6. Insights e Possibilidades Aprendidas

Durante este processo, você pode ter aprendido:

*   **Indexação e Enriquecimento de Dados:** O Azure AI Search pode indexar documentos e enriquecê-los com informações extraídas por meio de habilidades de IA.
*   **Uso de Habilidades Cognitivas:** As habilidades cognitivas, como OCR, extração de frases-chave, detecção de sentimentos e extração de entidades, podem gerar insights significativos.
*   **Armazenamento de Conhecimento:** O knowledge store permite armazenar e analisar dados enriquecidos de maneira organizada, como tabelas e projeções de dados.
*   **Consultas Flexíveis:** O Search explorer permite fazer consultas complexas utilizando filtros, e visualizar os resultados em formato JSON.
*    **Integração de Serviços Azure:** A facilidade de integrar diferentes serviços Azure para criar uma solução de busca e análise robusta.

**Possibilidades:**

*   **Pesquisa Aprimorada:** Criar soluções de pesquisa personalizadas para documentos, imagens e outros tipos de dados.
*   **Análise de Feedback:** Analisar feedback de clientes, identificar tendências e sentimentos para melhoria de produtos ou serviços.
*   **Extração de Informações:** Extrair informações relevantes de grandes volumes de dados, como entidades, frases-chave e locais.
*   **Geração de Relatórios:** Gerar relatórios com insights baseados em dados enriquecidos e armazenados no knowledge store.
*    **Automação de Processos:** Automatizar processos de análise e classificação de informações.

## 7. Limpeza dos Recursos

Se você não pretende realizar mais exercícios, exclua os recursos para evitar custos desnecessários:

1.  Abra o **portal do Azure** em [https://portal.azure.com](https://portal.azure.com).
2.  Selecione o grupo de recursos que contém o recurso criado.
3.  Selecione o recurso e clique em **Excluir**, depois em **Sim** para confirmar.
4. Links: https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/11-ai-search.html
