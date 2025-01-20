# Análise de Sentimento de Texto com Azure AI Language e Salvando Resultados

Este guia detalha como usar o **Azure AI Language** para realizar a análise de sentimento em um texto, como criar um arquivo de texto com suas sentenças, e como salvar e descrever o processo, insights e possibilidades aprendidas.

## 1. Configuração Inicial

Antes de começar, você precisa ter uma conta no Azure e um recurso do **Azure AI Language** configurado. Caso ainda não tenha, siga os passos abaixo:

1.  **Acesse o portal do Azure** em [https://portal.azure.com](https://portal.azure.com) e faça login com suas credenciais da Microsoft.
2.  Crie um recurso do **Language service**:
    *   Clique no botão **＋Criar um recurso** e procure por *Language service*.
    *   Selecione **criar** um plano de **Language service**.
    *   Na página, selecione **Continuar para criar seu recurso**.
    *   Configure o recurso com as seguintes opções:
        *   **Assinatura**: *Sua assinatura do Azure*.
        *   **Grupo de recursos**: *Crie ou selecione um grupo de recursos com um nome único*.
        *   **Região**: *Selecione a região geográfica mais próxima. Se estiver no leste dos EUA, use “Leste dos EUA 2”*.
        *   **Nome**: *Insira um nome único*.
        *   **Nível de preço**: *Free F0 ou S se Free F0 não estiver disponível*.
        *   Marque a caixa indicando que você leu e entendeu os termos abaixo.
    *   Selecione **Revisar + criar**, depois **Criar** e aguarde a conclusão da implantação .
3.  **Configure o recurso no Azure AI Language Studio**:
    *   Abra o **Language Studio** em [https://language.cognitive.azure.com](https://language.cognitive.azure.com) e faça login.
    *   Quando solicitado a selecionar um recurso do Azure, configure:
        *   **Diretório Azure**: *Diretório padrão*.
        *   **Assinatura Azure**: *Sua assinatura*.
        *   **Tipo de recurso**: *Language*.
        *   **Nome do recurso**: *Selecione o recurso Language service que você acabou de criar* .
    *   Selecione **Concluído**.
    *   **Importante:** Caso não seja solicitado a escolher um recurso, verifique as configurações na aba de **Recursos** no menu de **Configurações** (⚙) e selecione seu recurso, certificando-se que a Identidade Gerenciada esteja **Habilitada** .

## 2. Criar Pasta "inputs" e Arquivo de Texto

1.  No seu computador, crie uma pasta chamada **inputs**.
2.  Dentro da pasta **inputs**, crie um arquivo de texto (por exemplo, `sentences.txt`).
3.  Neste arquivo, escreva algumas sentenças que você deseja analisar. Por exemplo:
    *   "O serviço do hotel foi excelente e eu amei a localização."
    *   "A comida estava horrível e o quarto era muito pequeno."
    *   "Apesar de alguns problemas, eu gostei da minha estadia."
    *   "O atendimento foi péssimo e não recomendo."
    *   "O quarto era espaçoso e confortável, tudo perfeito."

## 3. Realizar a Análise de Sentimento

1.  Abra o **Language Studio** em [https://language.cognitive.azure.com](https://language.cognitive.azure.com) .
2.  Na página inicial, selecione a aba **Classificar texto** e então o bloco **Analisar sentimento e extrair opiniões** .
3.  Em *Selecionar idioma do texto*, escolha **Português**.
4.  Em *Selecionar seu recurso do Azure*, escolha seu recurso.
5.  Em *Insira seu próprio texto, carregue um arquivo ou use um dos nossos textos de exemplo*, copie e cole o conteúdo do seu arquivo `sentences.txt`.
6.  Marque a caixa confirmando que a demonstração pode gerar custos e clique em **Executar** .
7.  Analise os resultados:
    *   O serviço analisará o sentimento de cada frase e do documento como um todo .
    *   Para cada frase e documento, um sentimento geral será apresentado, junto com os scores de *positivo*, *neutro* e *negativo*.
    *   Os scores indicam o nível de confiança do serviço em relação a cada tipo de sentimento .

## 4. Salvar os Resultados da Análise

1.  **Copie os resultados** da análise de sentimento do painel do Language Studio.
2.  Crie um **arquivo de texto** (por exemplo, `sentences_output.txt`) dentro da pasta **output**.
3.  **Cole os resultados** copiados no arquivo de texto e salve-o.

## 5. Insights e Possibilidades Aprendidas

Durante este processo, você pode ter aprendido:

*   **A capacidade de análise de sentimento**: O Azure AI Language pode identificar o sentimento geral de textos.
*   **Scores de confiança**: Os scores de confiança indicam a probabilidade de um texto ser positivo, neutro ou negativo, oferecendo mais precisão na análise.
*   **Análise detalhada**: O serviço pode analisar o sentimento de cada frase individualmente, além do sentimento geral do texto.
*   **Versatilidade**: A análise de sentimento pode ser aplicada em diversos tipos de textos, como reviews de clientes, feedbacks, posts em redes sociais, entre outros.

**Possibilidades:**

*   **Análise de feedback de clientes**: Identificar se os clientes estão satisfeitos com produtos ou serviços através do sentimento expresso em seus comentários.
*   **Monitoramento de redes sociais**: Acompanhar a percepção pública sobre marcas ou eventos através da análise de posts e comentários.
*   **Classificação de documentos**: Categorizar documentos de acordo com o sentimento predominante em seu conteúdo.
*    **Automação de processos**: Analisar e classificar textos para direcionar ações baseadas na polaridade do sentimento.

## 6. Limpeza dos Recursos

Se você não pretende realizar mais exercícios, exclua os recursos para evitar custos desnecessários:

1.  Abra o **portal do Azure** em [https://portal.azure.com](https://portal.azure.com) .
2.  Selecione o grupo de recursos que contém o recurso criado.
3.  Selecione o recurso e clique em **Excluir**, depois em **Sim** para confirmar.
4. Links:
https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/09-speech.html
https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/06-text-analysis.html
