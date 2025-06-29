# Tutorial: Como Criar um Dashboard de Vendas Interativo no Excel

![Excel](https://img.shields.io/badge/Microsoft_Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)
![Nível](https://img.shields.io/badge/n%C3%ADvel-intermedi%C3%A1rio-yellow?style=for-the-badge)
![Licença](https://img.shields.io/badge/licen%C3%A7a-MIT-blue?style=for-the-badge)

## Sobre Este Tutorial

Este documento é um guia passo a passo para transformar uma base de dados de vendas bruta em um **Dashboard dinâmico e informativo** no Microsoft Excel. O objetivo é capacitar você a organizar, analisar e visualizar dados de forma eficaz, permitindo a extração de insights valiosos para a tomada de decisão.

Vamos focar em ferramentas essenciais como Tabelas Estruturadas, Tabelas Dinâmicas, Gráficos Dinâmicos e Segmentação de Dados.

## Índice do Tutorial

1.  [O Ponto de Partida: A Base de Dados](#-passo-1-o-ponto-de-partida-a-base-de-dados)
2.  [Organizando os Dados com Tabelas Estruturadas](#-passo-2-organizando-os-dados-com-tabelas-estruturadas)
3.  [A Central de Análise: Criando as Tabelas Dinâmicas](#-passo-3-a-central-de-análise-criando-as-tabelas-dinâmicas)
4.  [Dando Vida aos Dados: Inserindo Gráficos Dinâmicos](#-passo-4-dando-vida-aos-dados-inserindo-gráficos-dinâmicos)
5.  [Montando o Painel: O Layout do Dashboard](#-passo-5-montando-o-painel-o-layout-do-dashboard)
6.  [Interatividade Total com Segmentação de Dados (Slicers)](#-passo-6-interatividade-total-com-segmentação-de-dados-slicers)
7.  [Toques Finais e Apresentação](#-passo-7-toques-finais-e-apresentação)
8.  [Conclusão e Próximos Desafios](#-conclusão-e-próximos-desafios)

---

### 🏁 Passo 1: O Ponto de Partida: A Base de Dados

Todo bom dashboard começa com dados bem organizados. Para este tutorial, sua base de dados deve ser uma **lista plana**, onde cada linha representa um registro único (uma venda) e cada coluna uma característica dessa venda.

Crie uma aba no seu Excel chamada `Base_de_Dados` e organize suas informações com os seguintes cabeçalhos (ou similares):

| ID_Pedido | Data_Venda | Vendedor      | Região    | Produto             | Categoria | Preco_Unitario | Quantidade | Total_Venda |
| :-------- | :--------- | :------------ | :-------- | :------------------ | :-------- | :------------- | :--------- | :---------- |
| 1001      | 01/01/2025 | Ana Silva     | Sudeste   | Notebook Pro X      | Eletrônicos | 4500           | 2          | 9000        |
| 1002      | 02/01/2025 | Carlos Souza  | Nordeste  | Cadeira Gamer       | Mobiliário  | 1200           | 5          | 6000        |
| 1003      | 02/01/2025 | Ana Silva     | Sudeste   | Mouse sem Fio       | Acessórios  | 150            | 10         | 1500        |

**Dica:** A coluna `Total_Venda` pode ser uma fórmula: `=[@[Preco_Unitario]]*[@[Quantidade]]` depois que transformarmos os dados em uma Tabela.

### 🗂️ Passo 2: Organizando os Dados com Tabelas Estruturadas

Transformar sua base de dados em uma Tabela Estruturada é o passo mais importante para garantir que seu dashboard seja dinâmico.

1.  Clique em qualquer célula dentro da sua base de dados.
2.  Pressione `Ctrl + T` (ou vá em `Inserir > Tabela`).
3.  Confirme que a opção "Minha tabela tem cabeçalhos" está marcada e clique em OK.
4.  Com a tabela selecionada, vá na guia `Design da Tabela` (que aparecerá no menu superior).
5.  No campo **Nome da Tabela**, dê um nome significativo, como `tblVendas`.

### ⚙️ Passo 3: A Central de Análise: Criando as Tabelas Dinâmicas

As Tabelas Dinâmicas (PivotTables) serão o motor do nosso dashboard. Elas farão os cálculos e as sumarizações. Vamos criá-las em uma nova aba para manter a organização.

1.  Crie uma nova aba chamada `Apoio_Dinamicas`. É aqui que todas as nossas tabelas de apoio ficarão.
2.  Volte para a `Base_de_Dados`, clique na sua `tblVendas`.
3.  Vá em `Inserir > Tabela Dinâmica`.
4.  Na janela que se abre, escolha "Planilha Existente" e, no campo `Localização`, selecione a célula `A1` da sua aba `Apoio_Dinamicas`.

Agora, vamos criar as análises que precisamos:

-   **Análise 1: Receita Total por Categoria**
    -   Arraste `Categoria` para o campo **Linhas**.
    -   Arraste `Total_Venda` para o campo **Valores**.

-   **Análise 2: Vendas por Vendedor**
    -   Copie e cole a Tabela Dinâmica que você acabou de criar em outra célula da mesma aba (ex: `E1`).
    -   Nesta nova tabela, troque o campo `Categoria` (em Linhas) por `Vendedor`.

-   **Análise 3: Vendas ao Longo do Tempo**
    -   Crie uma terceira Tabela Dinâmica.
    -   Arraste `Data_Venda` para **Linhas**. O Excel agrupará automaticamente por meses e anos.
    -   Arraste `Total_Venda` para **Valores**.

Repita o processo para todas as análises que desejar (ex: Vendas por Região, Quantidade de Produtos Vendidos, etc.).

### 📊 Passo 4: Dando Vida aos Dados: Inserindo Gráficos Dinâmicos

Para cada Tabela Dinâmica que criamos, vamos gerar um Gráfico Dinâmico correspondente.

1.  Clique na sua primeira Tabela Dinâmica (Receita por Categoria).
2.  Vá na guia `Análise de Tabela Dinâmica > Gráfico Dinâmico`.
3.  Escolha o tipo de gráfico que melhor representa os dados. Um gráfico de **Barras** ou de **Pizza/Rosca** funciona bem para categorias.
4.  Repita o processo para as outras tabelas:
    -   **Vendas por Vendedor:** Gráfico de **Barras**.
    -   **Vendas ao Longo do Tempo:** Gráfico de **Linhas**.

**Dica:** "Limpe" seus gráficos clicando nos botões cinzas de campo (ex: "Soma de Total_Venda") com o botão direito e escolhendo `Ocultar Todos os Botões de Campo no Gráfico`.

### 🎨 Passo 5: Montando o Painel: O Layout do Dashboard

É hora de juntar tudo em uma única tela.

1.  Crie uma nova aba final chamada `Dashboard`.
2.  Vá em `Exibir` e desmarque as `Linhas de Grade` e os `Títulos` para ter uma tela em branco.
3.  Volte para a aba `Apoio_Dinamicas`.
4.  Selecione cada um dos seus gráficos, use `Ctrl + X` (Recortar) e `Ctrl + V` (Colar) para movê-los para a sua aba `Dashboard`.
5.  Organize os gráficos de forma lógica e visualmente agradável. Deixe um espaço no topo ou na lateral para os nossos filtros.

### 🖱️ Passo 6: Interatividade Total com Segmentação de Dados (Slicers)

A Segmentação de Dados (Slicers) e a Linha do Tempo são os filtros interativos que darão poder ao seu dashboard.

1.  Clique em qualquer um dos seus gráficos no `Dashboard`.
2.  Vá em `Análise de Gráfico Dinâmico > Inserir Segmentação de Dados`.
3.  Na janela que abrir, marque as caixas dos filtros que você quer usar. Sugestões: `Região`, `Vendedor`, `Categoria`. Clique em OK.
4.  Para o filtro de data, vá em `Análise de Gráfico Dinâmico > Inserir Linha do Tempo` e selecione `Data_Venda`.

**Passo mais importante da interatividade:**

Por padrão, um slicer controla apenas o gráfico do qual ele foi criado. Precisamos conectá-lo a **TODOS** os gráficos.

5.  Clique com o botão direito em um dos slicers e escolha `Conexões de Relatório`.
6.  Na janela, marque a caixa de seleção para **TODAS as Tabelas Dinâmicas** que você criou na sua aba `Apoio_Dinamicas`.
7.  Clique em OK e repita este processo para **cada slicer** e para a **Linha do Tempo**.

Agora, ao clicar em um botão de um slicer, todos os gráficos do dashboard serão filtrados simultaneamente!

### ✨ Passo 7: Toques Finais e Apresentação

1.  **Personalize o Design:** Altere as cores dos seus gráficos e slicers para que combinem. Na guia `Design` do gráfico e na guia `Segmentação` do slicer, você encontrará várias opções de estilo.
2.  **KPIs Principais:** Crie cartões para os indicadores mais importantes (ex: Receita Total). Você pode fazer isso inserindo uma forma de `Caixa de Texto`, clicando na barra de fórmulas, digitando `=` e, em seguida, clicando na célula da Tabela Dinâmica que contém o valor total.
3.  **Oculte as Abas de Apoio:** Clique com o botão direito nas abas `Base_de_Dados` e `Apoio_Dinamicas` e escolha `Ocultar`.
4.  **Proteja seu Trabalho:** Vá na aba `Dashboard`, em `Revisão > Proteger Planilha`. Isso evita que usuários alterem o layout acidentalmente. Permita apenas a seleção de células desbloqueadas para que os slicers continuem funcionando.

### ✅ Conclusão e Próximos Desafios

Parabéns! Você construiu um dashboard de vendas completo, visualmente atraente e, o mais importante, interativo. Essa ferramenta permite analisar o desempenho de vendas de múltiplos ângulos com apenas alguns cliques.

**Como ir além:**
-   **Power Pivot e DAX:** Para análises mais complexas e para relacionar múltiplas tabelas, explore o Power Pivot e as fórmulas DAX.
-   **Power Query:** Automatize a limpeza e a importação de dados de fontes externas (outros arquivos, bancos de dados) com o Power Query.
-   **Gráficos Personalizados:** Explore tipos de gráficos menos comuns, como Funil, Mapa de Árvore ou Cascata, para diferentes tipos de visualização.

