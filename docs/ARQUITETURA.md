# Arquitetura do projeto

## Visão geral

O RifasJess utiliza uma arquitetura de três camadas baseada nos recursos da Microsoft Power Platform.

## Camada de apresentação

A camada de apresentação foi construída com Microsoft Power Apps Canvas.

Responsabilidades:

- exibição das telas;
- navegação;
- formulários;
- galeria de materiais;
- entrada de dados;
- mensagens apresentadas ao usuário.

## Camada de lógica

A lógica de negócio foi implementada com fórmulas Power Fx.

Responsabilidades:

- definição do modo de inclusão ou edição;
- seleção do registro;
- pesquisa dos materiais;
- validação do formulário;
- envio dos dados;
- atualização da fonte de dados;
- navegação após o salvamento.

## Camada de dados

A persistência dos registros é realizada por uma lista do Microsoft SharePoint.

Na AC1, a lista Materiais armazena os dados utilizados pelo formulário e pela galeria.

## Fluxo principal da AC1

1. O usuário acessa o aplicativo.
2. O usuário abre a tela de materiais.
3. O aplicativo consulta os registros no SharePoint.
4. O usuário pode cadastrar um material.
5. O formulário valida e envia os dados.
6. O SharePoint armazena o registro.
7. A galeria apresenta os dados atualizados.

## Fluxo de edição

1. O usuário seleciona o ícone de edição.
2. O aplicativo armazena o identificador do material selecionado.
3. O formulário é aberto em modo de edição.
4. O registro correspondente é consultado.
5. O usuário altera os dados.
6. O formulário atualiza o registro no SharePoint.