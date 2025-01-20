# Reconhecimento de Texto em Imagem com Azure AI Vision e Salvando Resultados

Este guia detalha como usar o **Azure AI Vision** para realizar o reconhecimento de texto (OCR) em uma imagem, e como salvar os resultados em uma pasta, descrevendo o processo, insights e possibilidades aprendidas.

## 1. Configuração Inicial

Antes de começar, você precisa ter uma conta no Azure e um recurso do **Azure AI services** configurado. Caso ainda não tenha, siga os passos abaixo:

1.  **Acesse o portal do Azure** em [https://portal.azure.com](https://portal.azure.com) e faça login com suas credenciais da Microsoft [1-3].
2.  Crie um recurso do **Azure AI services**:
    *   Clique em **＋Criar um recurso** e procure por *Azure AI services* [1-3].
    *   Selecione a opção *Azure services only* para refinar a busca [2].
    *   Escolha a instância de  *Azure AI services* com a descrição *Connect powerful AI to your apps* [4].
    *   Configure o recurso com as seguintes opções:
        *   **Assinatura**: *Sua assinatura do Azure* [4-6].
        *   **Grupo de recursos**: *Crie ou selecione um grupo de recursos com um nome único* [4-6].
        *   **Região**: *Selecione a região geográfica mais próxima. Se estiver no leste dos EUA, use "Leste dos EUA 2"* [4-6].
        *   **Nome**: *Insira um nome único* [4-6].
        *   **Nível de preço**: *Standard S0* [4-6].
        *   Marque a caixa indicando que você leu e entendeu os termos abaixo [4-6].
    *   Clique em **Revisar + criar** e depois em **Criar** [4-6]. Aguarde a conclusão da implantação.
3.  **Conecte o recurso ao Vision Studio**:
    *   Abra o **Vision Studio** em [https://portal.vision.cognitive.azure.com](https://portal.vision.cognitive.azure.com) [7-9].
    *   Faça login com a mesma conta usada para criar o recurso do Azure AI services [7-9].
    *   Certifique-se de usar o mesmo diretório [7-9].
    *   Na página inicial do Vision Studio, selecione **View all resources** em **Getting started with Vision** [7-9].
    *   Passe o mouse sobre o recurso criado e marque a caixa à esquerda do nome. Depois, clique em **Select as default resource** [7-9].
    *   Se o recurso não estiver listado, clique em **Refresh** [10-12].
    *   Feche a página de configurações clicando no "x" no canto superior direito [10-12].

## 2. Criar Pastas "inputs" e "output"

1.  No seu computador, crie uma pasta chamada **inputs**.
2.  Dentro da pasta **inputs**, salve a imagem que você deseja usar para o reconhecimento de texto. Por exemplo, você pode usar as imagens fornecidas nos exercícios como `advert.jpg`, `letter.jpg`, `note.jpg` ou `receipt.jpg` [13, 14].
3.  Crie também uma pasta chamada **output** no mesmo diretório onde você criou a pasta **inputs**.

## 3. Realizar o Reconhecimento de Texto (OCR)

1.  Abra o **Vision Studio** em [https://portal.vision.cognitive.azure.com](https://portal.vision.cognitive.azure.com) [10].
2.  Na página inicial, selecione **Optical character recognition** e, em seguida, **Extract text from images** [10].
3.  Leia e marque a caixa de confirmação da política de uso do recurso [10].
4.  Clique em **Browse for a file** e navegue até a pasta **inputs** [13].
5.  Selecione a imagem que você salvou anteriormente (por exemplo, `advert.jpg`) e clique em **Open** [13].
6.  Analise os resultados:
    *   Em **Detected attributes**, o texto encontrado na imagem será organizado em uma estrutura hierárquica de regiões, linhas e palavras [13].
    *   Na imagem, a localização do texto será indicada por uma caixa delimitadora [13].
7.  Se você tiver tempo, tente outras imagens como `letter.jpg`, `note.jpg` ou `receipt.jpg` [14].

## 4. Salvar os Resultados do OCR

1.  **Copie o texto** detectado do painel **Detected attributes** no Vision Studio.
2.  Crie um **arquivo de texto** (por exemplo, `advert_output.txt`) dentro da pasta **output**.
3.  **Cole o texto** copiado no arquivo de texto e salve-o.
4.  Se desejar, salve também **informações sobre as caixas delimitadoras** do texto, se disponíveis no Vision Studio.

## 5. Insights e Possibilidades Aprendidas

Durante este processo, você pode ter aprendido:

*   **O poder do OCR**: O Azure AI Vision é capaz de extrair texto de imagens com boa precisão [15].
*   **Estrutura hierárquica**: O texto é organizado em regiões, linhas e palavras, o que pode ser útil para diversas aplicações [13].
*   **Caixas delimitadoras**: A localização do texto é visualizada com caixas delimitadoras, facilitando a identificação e manipulação [13].
*   **Versatilidade**: O OCR pode ser aplicado a diversos tipos de imagens, como anúncios, cartas, notas e recibos [13, 14].

**Possibilidades:**

*   **Automação de entrada de dados**: Extrair texto de documentos digitalizados para automatizar processos de entrada de dados.
*   **Acessibilidade**: Tornar o conteúdo de imagens acessível para pessoas com deficiência visual.
*   **Análise de documentos**: Extrair informações de contratos, faturas e outros documentos.
*   **Digitalização de arquivos**: Converter documentos físicos em texto digital para facilitar a busca e organização.

## 6. Limpeza dos Recursos

Se você não pretende realizar mais exercícios, exclua os recursos para evitar custos desnecessários:

1.  Abra o **portal do Azure** em [https://portal.azure.com](https://portal.azure.com) [14, 16, 17].
2.  Selecione o grupo de recursos que contém o recurso criado [14, 16, 17].
3.  Selecione o recurso e clique em **Excluir**, depois em **Sim** para confirmar [14, 16, 17].
4. Links:
https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/04-face.html
https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/05-ocr.html
https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/03-image-analysis.html
