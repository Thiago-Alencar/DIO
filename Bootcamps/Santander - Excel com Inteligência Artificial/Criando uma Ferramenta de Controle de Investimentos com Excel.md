# Simulador de Investimentos em Fundos Imobiliários (FIIs)


## 🎯 Objetivo do Projeto

Este projeto consiste na criação de uma ferramenta em Microsoft Excel para simular o crescimento de patrimônio e a geração de renda passiva através de investimentos em Fundos de Investimento Imobiliário (FIIs). A planilha permite ao usuário visualizar o potencial de seus investimentos ao longo do tempo, considerando aportes mensais e o reinvestimento dos dividendos (efeito "bola de neve").

O objetivo principal é fornecer uma ferramenta prática e visual para que investidores, iniciantes ou experientes, possam projetar seus resultados e tomar decisões mais informadas.

## ✨ Funcionalidades Principais

A ferramenta de simulação possui as seguintes características:

* **Simulação Personalizada:** O usuário pode inserir dados como o FII desejado, o valor do aporte mensal e o preço de aquisição da cota.
* **Cálculo de Rendimento Mensal:** Calcula automaticamente os dividendos recebidos com base na quantidade de cotas e no dividendo por cota (Dividend Yield).
* **Projeção de Reinvestimento:** Simula o "efeito bola de neve", onde os dividendos recebidos são somados ao aporte mensal para comprar novas cotas.
* **Visualização de Longo Prazo:** Apresenta uma tabela detalhada que mostra a evolução do patrimônio, o total de cotas e a renda passiva mensal ao longo de vários anos.
* **Base de Dados de FIIs:** Inclui uma aba com dados de diferentes Fundos Imobiliários que podem ser usados como referência para a simulação.

## 🛠️ Como a Planilha Funciona (Documentação Técnica)

A estrutura da planilha foi dividida em duas abas principais para garantir organização e clareza: `APP` e `Planilha2` (Base de Dados).

### 1. Aba de Dados (`Planilha2`)

Esta aba funciona como um pequeno banco de dados que alimenta a ferramenta principal.

* **Estrutura:** Contém uma lista de Fundos Imobiliários com informações relevantes como:
    * `FUNDO`: O ticker (código de negociação) do FII.
    * `SETOR`: O segmento de atuação do fundo (Ex: Lajes Corporativas, Shoppings, Logística).
    * `PREÇO`: O valor atual da cota.
    * `DIVIDEND YIELD (mês)`: O rendimento percentual mensal do fundo.
    * `DIVIDENDO`: O valor em reais do último dividendo distribuído por cota.

* **Utilização:** Os dados desta aba são utilizados na aba `APP` para preencher automaticamente as informações do FII selecionado, utilizando a função `PROCV` (ou `VLOOKUP`) do Excel.

### 2. Aba de Simulação (`APP`)

Esta é a interface principal onde o usuário interage e visualiza os resultados da simulação.

#### **Entradas do Usuário (Inputs)**

O usuário precisa preencher os seguintes campos para iniciar a simulação:

* **`Escolha o FII:`**: Um menu suspenso (Data Validation) que permite selecionar um dos FIIs listados na `Planilha2`.
* **`Preço da Cota (R$):`**: O valor de compra da cota do FII. Este valor pode ser preenchido automaticamente ao escolher o FII ou inserido manualmente.
* **`Aporte Mensal (R$):`**: O valor que o investidor planeja investir todos os meses.

#### **Cálculos Financeiros Aplicados**

A planilha realiza uma série de cálculos sequenciais para projetar o crescimento do investimento mês a mês.

1.  **Rendimento Mensal (Dividendos):** O principal cálculo financeiro da planilha. A fórmula base é:
    $$ \text{Rendimento Mensal} = \text{Total de Cotas} \times \text{Dividendo por Cota} $$
    Este valor representa a renda passiva gerada pelos seus investimentos a cada mês.

2.  **Total Disponível para Investir:** Soma o aporte definido pelo usuário com os dividendos recebidos no mês.
    $$ \text{Total para Investir} = \text{Aporte Mensal} + \text{Rendimento Mensal} $$

3.  **Novas Cotas Adquiridas:** Calcula quantas novas cotas podem ser compradas com o valor total disponível.
    $$ \text{Novas Cotas} = \frac{\text{Total para Investir}}{\text{Preço da Cota}} $$
    *Observação: A planilha utiliza a função `INT` para considerar apenas a compra de cotas inteiras.*

4.  **Atualização do Saldo:** O valor que sobra após a compra das cotas é guardado como saldo para o próximo mês.
    $$ \text{Saldo do Mês} = \text{MOD}(\text{Total para Investir}, \text{Preço da Cota}) $$

5.  **Efeito Bola de Neve:** Ao longo do tempo, o `Rendimento Mensal` cresce, o que aumenta o `Total para Investir` e, consequentemente, a quantidade de `Novas Cotas` adquiridas. Esse ciclo de reinvestimento acelera o crescimento do patrimônio e da renda passiva.

## 🚀 Como Utilizar a Ferramenta

Siga os passos abaixo para realizar sua simulação:

1.  **Abra o arquivo Excel:** Inicie o arquivo `Simulador_Investimentos_Fundos_Imobiliarios.xlsx`.
2.  **Acesse a aba `APP`:** Navegue para a planilha principal da simulação.
3.  **Escolha o Fundo:** No campo **`Escolha o FII`**, selecione um fundo da lista suspensa. As informações de preço e dividendo serão carregadas automaticamente.
4.  **Defina seu Aporte:** Insira o valor que você deseja investir mensalmente no campo **`Aporte Mensal (R$)`**.
5.  **Analise os Resultados:** Observe a tabela de projeção. Ela mostrará a evolução do seu investimento, incluindo:
    * O número de cotas que você acumulará.
    * O valor total investido (soma dos aportes).
    * O total de dividendos recebidos.
    * O patrimônio total acumulado.
    * Sua renda passiva mensal projetada.
