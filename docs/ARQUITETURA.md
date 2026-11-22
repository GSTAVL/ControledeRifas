# Arquitetura do RifasJess

## Visão geral

O RifasJess foi desenvolvido com Microsoft Power Apps Canvas e utiliza listas do SharePoint como camada de persistência.

A solução está dividida em três camadas:

1. apresentação;
2. lógica;
3. dados.

## Camada de apresentação

A camada de apresentação utiliza Microsoft Power Apps Canvas.

Responsabilidades:

- exibição das telas;
- navegação;
- entrada de dados;
- formulários;
- galerias;
- pesquisa;
- mensagens;
- indicadores;
- dashboard.

## Camada de lógica

A lógica de negócio utiliza Power Fx.

Responsabilidades:

- navegação entre as telas;
- validação dos campos;
- definição do modo de inclusão ou edição;
- busca dos registros;
- cálculo dos valores das rifas;
- atualização do status dos materiais;
- cálculo dos indicadores;
- atualização das fontes;
- tratamento de erros.

## Camada de dados

A persistência utiliza duas listas do SharePoint:

- MateriaisLista;
- RifasLista.

## Módulo de materiais

O módulo de materiais é responsável por:

- cadastrar materiais;
- consultar registros;
- pesquisar pelo nome;
- editar;
- alterar o status;
- identificar materiais comprados;
- contabilizar itens comprados e pendentes.

### Fluxo

`Usuário → Power Apps → Power Fx → MateriaisLista`

## Módulo de rifas

O módulo de rifas é responsável por:

- cadastrar vendas;
- consultar registros;
- pesquisar compradores;
- editar;
- registrar método de pagamento;
- calcular ou armazenar o valor da venda;
- armazenar anexos opcionais.

### Fluxo

`Usuário → Power Apps → Power Fx → RifasLista`

## Controle de compra

O controle de compra altera o status de um material existente.

Fluxo:

1. O usuário seleciona o ícone de carrinho.
2. O aplicativo identifica o material selecionado.
3. O usuário confirma a operação.
4. Power Fx atualiza o registro.
5. O SharePoint armazena o novo status.
6. O aplicativo apresenta a identificação de comprado.
7. O contador é atualizado.

## Dashboard integrado

O dashboard utiliza as duas fontes.

### Entradas

Da lista Materiais:

- valor necessário;
- quantidade total;
- quantidade comprada;
- quantidade pendente.

Da lista Rifas:

- valor arrecadado.

### Saídas

- valor necessário;
- valor arrecadado;
- valor restante ou excedente;
- percentual arrecadado;
- materiais comprados;
- materiais pendentes.

## Fluxo do dashboard

`MateriaisLista + RifasLista → Power Fx → Dashboard`

## Atualização

Ao abrir a tela inicial:

1. o aplicativo atualiza as duas fontes;
2. recalcula os totais;
3. recalcula o saldo;
4. recalcula os percentuais;
5. atualiza os controles visuais.

## Fórmulas conceituais

### Valor necessário

`Soma dos valores da lista Materiais`

### Valor arrecadado

`Soma dos valores da lista Rifas`

### Valor restante

`Valor necessário - Valor arrecadado`

### Progresso das compras

`Materiais comprados / Total de materiais`

## Observação

As listas permanecem independentes no SharePoint. A integração é realizada pela camada de lógica do Power Apps durante o cálculo dos indicadores.
