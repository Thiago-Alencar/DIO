# Tutorial: Crie sua Própria Ferramenta de Controle para o Imposto de Renda no Excel

![Excel](https://img.shields.io/badge/Microsoft_Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)
![Nível](https://img.shields.io/badge/n%C3%ADvel-intermedi%C3%A1rio-yellow?style=for-the-badge)
![Licença](https://img.shields.io/badge/licen%C3%A7a-MIT-blue?style=for-the-badge)

## Sobre Este Repositório

Este repositório não contém uma planilha pronta. Em vez disso, ele é um **guia completo e detalhado** que ensina você a construir, passo a passo, uma poderosa ferramenta no Excel para organizar e agregar informações para a sua declaração de Imposto de Renda.

O objetivo é aplicar conceitos práticos de Excel, desde a estruturação de dados até a automação com VBA, criando uma solução robusta e com interface amigável.

## Índice do Tutorial

1.  [Planejamento e Estrutura](#-passo-0-planejamento-e-estrutura)
2.  [Configuração Inicial do Arquivo](#-passo-1-configuração-inicial-do-arquivo)
3.  [Criando as Abas de Trabalho](#-passo-2-criando-as-abas-de-trabalho)
4.  [Estruturando as Tabelas de Dados](#-passo-3-estruturando-as-tabelas-de-dados)
5.  [Implementando a Validação de Dados](#-passo-4-implementando-a-validação-de-dados)
6.  [Criando o Dashboard de Resumo com Fórmulas](#-passo-5-criando-o-dashboard-de-resumo-com-fórmulas)
7.  [Construindo o Menu de Navegação (Simples e Avançado)](#-passo-6-construindo-o-menu-de-navegação)
8.  [Toques Finais e Proteção](#-passo-7-toques-finais-e-proteção)
9.  [Conclusão e Próximos Passos](#-conclusão-e-próximos-passos)

---

### 🏁 Passo 0: Planejamento e Estrutura

Antes de abrir o Excel, vamos planejar. Nossa ferramenta terá:
-   **Abas de Entrada de Dados:** Locais para inserir rendimentos, pagamentos, bens, etc.
-   **Aba de Controle:** Uma aba oculta para listas suspensas (dropdowns), garantindo a consistência dos dados.
-   **Aba de Visualização:** Um dashboard para resumir as informações.
-   **Aba de Navegação:** Um menu principal para facilitar o uso.

### 💾 Passo 1: Configuração Inicial do Arquivo

1.  Abra o Microsoft Excel e crie uma nova pasta de trabalho em branco.
2.  Imediatamente, salve o arquivo. É **essencial** salvá-lo com o tipo correto para suportar macros (VBA), que usaremos para a navegação.
    -   **Nome do Arquivo:** `Controle_IRPF.xlsm`
    -   **Tipo:** `Pasta de Trabalho Habilitada para Macro do Excel (*.xlsm)`

### 📑 Passo 2: Criando as Abas de Trabalho

Vamos criar todas as abas (planilhas) que precisaremos. Renomeie as abas padrão e crie novas até ter a seguinte estrutura:

1.  `Menu`
2.  `Rendimentos`
3.  `Pagamentos`
4.  `Bens_Direitos`
5.  `Dashboard`
6.  `Listas_Aux` (esta será nossa aba de controle)

### 📊 Passo 3: Estruturando as Tabelas de Dados

Agora, vamos definir os cabeçalhos em cada aba de entrada de dados e formatá-los como **Tabelas Estruturadas**. Isso torna as fórmulas dinâmicas e muito mais fáceis de ler.

1.  **Na aba `Rendimentos`:**
    -   Insira os cabeçalhos: `Data`, `Tipo`, `Fonte Pagadora`, `CPF/CNPJ da Fonte`, `Descrição`, `Valor`.
    -   Selecione os cabeçalhos e uma linha abaixo.
    -   Pressione `Ctrl + T` (ou vá em `Inserir > Tabela`).
    -   Marque a caixa "Minha tabela tem cabeçalhos" e clique em OK.
    -   Com a tabela selecionada, vá na guia `Design da Tabela` e mude o **Nome da Tabela** para `tblRendimentos`.

2.  **Na aba `Pagamentos`:**
    -   Cabeçalhos: `Data`, `Categoria`, `Beneficiário`, `CPF/CNPJ do Beneficiário`, `Descrição`, `Valor Pago`, `Valor Reembolsado`.
    -   Repita o processo para criar uma tabela e nomeie-a `tblPagamentos`.

3.  **Na aba `Bens_Direitos`:**
    -   Cabeçalhos: `Código do Bem`, `Localização`, `Descrição Detalhada`, `Valor (Ano Anterior)`, `Valor (Ano Atual)`.
    -   Crie a tabela e nomeie-a `tblBensDireitos`.

### ✔️ Passo 4: Implementando a Validação de Dados

Para evitar erros de digitação, vamos usar o recurso de Validação de Dados.

1.  **Crie as listas na aba `Listas_Aux`:**
    -   Na coluna A, crie uma lista de **Tipos de Rendimento** (ex: Salário, Aluguel, Pensão).
    -   Na coluna B, crie uma lista de **Categorias de Pagamento** (ex: Despesa Médica, Instrução, Pensão Alimentícia, Aluguel).

2.  **Aplique a validação na tabela `tblPagamentos`:**
    -   Selecione toda a coluna `Categoria` da sua tabela (clique no cabeçalho `Categoria` quando o cursor virar uma seta preta para baixo).
    -   Vá em `Dados > Validação de Dados`.
    -   Em `Permitir`, escolha `Lista`.
    -   No campo `Fonte`, clique na setinha e selecione o intervalo com as categorias que você criou na aba `Listas_Aux`.
    -   Clique em OK. Agora, a coluna `Categoria` terá um menu suspenso.

3.  **(Opcional) Validação de CPF/CNPJ:**
    -   Selecione a coluna `CPF/CNPJ`.
    -   Em `Validação de Dados`, escolha `Personalizado`.
    -   Use a fórmula `=ÉNÚM(A2*1)` para garantir que apenas números sejam digitados (ajuste `A2` para a primeira célula de dados da coluna). Isso é uma validação simples; validações completas de CPF exigem fórmulas mais complexas ou VBA.

### 📈 Passo 5: Criando o Dashboard de Resumo com Fórmulas

Na aba `Dashboard`, vamos consolidar os totais. Graças às tabelas estruturadas, isso é muito fácil.

1.  **Total de Rendimentos:**
    -   Em uma célula, digite o texto "Total de Rendimentos".
    -   Na célula ao lado, insira a fórmula:
    ```excel
    =SOMA(tblRendimentos[Valor])
    ```

2.  **Total de Pagamentos Dedutíveis:**
    -   Em outra célula, digite "Total de Despesas Médicas".
    -   Na célula ao lado, use a função `SOMASES`:
    ```excel
    =SOMASES(tblPagamentos[Valor Pago]; tblPagamentos[Categoria]; "Despesa Médica")
    ```
    (Note que o separador pode ser `;` ou `,` dependendo da sua configuração do Excel).

3.  Crie outros resumos que você achar úteis, como o valor total do seu patrimônio usando a tabela `tblBensDireitos`.

### 🧭 Passo 6: Construindo o Menu de Navegação

Vamos criar botões na aba `Menu` para facilitar o acesso às outras abas.

#### Método 1: Simples (com Hiperlinks)

1.  Na aba `Menu`, vá em `Inserir > Formas` e escolha um retângulo. Desenhe um botão.
2.  Digite um texto dentro do botão, como "Lançar Rendimentos".
3.  Clique com o botão direito na forma e escolha `Link...`.
4.  Na janela que abrir, selecione `Colocar neste Documento` no menu à esquerda.
5.  Escolha a aba `Rendimentos` na lista e clique em OK.
6.  Repita o processo para todos os outros botões (`Pagamentos`, `Dashboard`, etc.).

#### Método 2: Avançado (com VBA)

Este método dá um ar mais profissional, pois esconde as outras abas, mostrando apenas a ativa.

1.  Pressione `Alt + F11` para abrir o Editor do VBA.
2.  No menu, vá em `Inserir > Módulo`. Um módulo em branco aparecerá.
3.  Cole o seguinte código no módulo:
    ```vba
    Sub NavegarPara(NomeDaAba As String)
        ' Oculta todas as abas, exceto o Menu
        Dim ws As Worksheet
        For Each ws In ThisWorkbook.Worksheets
            If ws.Name <> "Menu" Then
                ws.Visible = xlSheetHidden
            End If
        Next ws
        
        ' Mostra a aba de destino
        ThisWorkbook.Sheets(NomeDaAba).Visible = xlSheetVisible
        
        ' Ativa a aba de destino
        ThisWorkbook.Sheets(NomeDaAba).Activate
    End Sub

    ' Funções específicas para cada botão
    Sub IrParaRendimentos()
        Call NavegarPara("Rendimentos")
    End Sub

    Sub IrParaPagamentos()
        Call NavegarPara("Pagamentos")
    End Sub

    Sub IrParaDashboard()
        Call NavegarPara("Dashboard")
    End Sub

    Sub VoltarAoMenu()
        Call NavegarPara("Menu")
        ThisWorkbook.Sheets("Menu").Activate
    End Sub
    ```
4.  Feche o editor de VBA.
5.  Crie seus botões na aba `Menu` como no método 1.
6.  Em vez de adicionar um link, clique com o botão direito no botão e escolha `Atribuir Macro...`.
7.  Selecione a macro correspondente (ex: `IrParaRendimentos` para o botão de rendimentos) e clique em OK.
8.  **Importante:** Em cada aba (`Rendimentos`, `Pagamentos`, etc.), crie um botão "Voltar ao Menu" e atribua a ele a macro `VoltarAoMenu`.

### ✨ Passo 7: Toques Finais e Proteção

1.  **Oculte a aba `Listas_Aux`:** Clique com o botão direito na aba e escolha `Ocultar`.
2.  **Melhore a aparência:** Na aba `Menu` e `Dashboard`, vá em `Exibir` e desmarque a opção `Linhas de Grade` para um visual mais limpo.
3.  **Proteja a estrutura:** Vá em `Revisão > Proteger Pasta de Trabalho`. Isso impede que os usuários excluam ou movam suas abas.
4.  **Proteja as fórmulas:** Na aba `Dashboard`, selecione as células que contêm suas fórmulas, clique com o botão direito, vá em `Formatar Células > Proteção` e verifique se a caixa `Bloqueada` está marcada. Depois, vá em `Revisão > Proteger Planilha`.

### ✅ Conclusão e Próximos Passos

Parabéns! Você construiu uma ferramenta funcional e organizada para controlar suas informações do IRPF. Você aplicou conceitos de estruturação de dados, fórmulas, validação e até automação.

**Desafios para evoluir o projeto:**
-   Crie gráficos no seu `Dashboard`.
-   Use a `Formatação Condicional` para destacar pagamentos acima de um certo valor.
-   Pesquise sobre como criar um UserForm em VBA para uma entrada de dados ainda mais sofisticada.

