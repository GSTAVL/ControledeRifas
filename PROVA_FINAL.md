# Prova Final: Dashboard e integração do RifasJess

## Objetivo

A Prova Final conclui o desenvolvimento do RifasJess por meio da integração dos módulos de materiais, rifas e controle de compras.

A nova funcionalidade desta etapa é o dashboard financeiro, responsável por apresentar uma visão consolidada da campanha.

## Evolução do projeto

### AC1: Gestão de materiais

A primeira entrega implementou:

- cadastro de materiais;
- consulta dos registros;
- pesquisa pelo nome;
- edição;
- validação;
- persistência no SharePoint.

### AC2: Gestão de rifas

A segunda entrega implementou:

- cadastro das vendas de rifas;
- consulta dos registros;
- pesquisa por comprador;
- edição;
- método de pagamento;
- valor da venda;
- anexo opcional;
- persistência no SharePoint.

### AC3: Controle de compras

A terceira entrega implementou:

- alteração do status do material;
- ação de compra pelo ícone de carrinho;
- identificação visual dos materiais comprados;
- contador de compras;
- atualização do registro no SharePoint.

### Prova Final: Dashboard integrado

A entrega final acrescenta:

- valor necessário para os materiais;
- valor arrecadado pelas rifas;
- valor restante ou excedente;
- percentual de arrecadação;
- quantidade de materiais comprados;
- quantidade de materiais pendentes;
- atualização dos indicadores a partir das listas do SharePoint.

## Arquitetura

O projeto utiliza:

- **Front-end:** Microsoft Power Apps Canvas;
- **Lógica:** Power Fx;
- **Dados:** Microsoft SharePoint Lists.

As duas fontes utilizadas são:

- `MateriaisLista`;
- `RifasLista`.

## Dashboard financeiro

### Valor necessário

O valor necessário corresponde à soma do campo Valor da lista de materiais.

Fórmula conceitual:

`Valor necessário = soma dos valores dos materiais`

### Valor arrecadado

O valor arrecadado corresponde à soma do campo Valor da lista de rifas.

Fórmula conceitual:

`Valor arrecadado = soma dos valores das vendas`

### Valor restante

O valor restante corresponde à diferença entre o valor necessário e o valor arrecadado.

Fórmula:

`Valor restante = Valor necessário - Valor arrecadado`

Quando o resultado é negativo, o aplicativo apresenta o valor absoluto como excedente.

### Percentual de arrecadação

Fórmula:

`Percentual = Valor arrecadado / Valor necessário`

### Progresso das compras

O progresso corresponde à quantidade de materiais com status `Comprado` em relação ao total de materiais cadastrados.

## Exemplo financeiro

Considerando:

- Valor necessário: R$ 1.265,00;
- Valor arrecadado: R$ 730,00.

O valor restante será:

`R$ 1.265,00 - R$ 730,00 = R$ 535,00`

O percentual arrecadado será aproximadamente:

`R$ 730,00 / R$ 1.265,00 = 57,7%`

## Fluxo completo

1. O usuário cadastra um material.
2. O material é armazenado no SharePoint.
3. O valor necessário é atualizado.
4. O usuário registra uma venda de rifa.
5. A venda é armazenada no SharePoint.
6. O valor arrecadado é atualizado.
7. O sistema recalcula o valor restante.
8. O usuário marca um material como comprado.
9. O status é atualizado para `Comprado`.
10. O indicador de materiais comprados é atualizado.
11. O dashboard consolida os resultados.

## Funcionalidades preservadas

### Materiais

- cadastro;
- consulta;
- pesquisa;
- edição;
- controle da compra.

### Rifas

- cadastro;
- consulta;
- pesquisa;
- edição;
- método de pagamento;
- anexos.

## Tratamentos implementados

- validação de campos obrigatórios;
- atualização de registros existentes;
- prevenção de duplicação durante a edição;
- tratamento de listas vazias;
- tratamento de divisão por zero;
- exibição de valor excedente quando a arrecadação supera a meta;
- atualização dos dados ao abrir a tela inicial.

## Canvas App

A versão final está disponível em:

`app/RifasJess_Final.msapp`

## Evidências

As evidências estão disponíveis em:

`evidencias/prova-final`

## GitHub Project Board

ADICIONAR_LINK_DO_BOARD

## Vídeo

ADICIONAR_LINK_DO_VIDEO

## Resultado

O RifasJess passa a oferecer um fluxo completo, desde o cadastro das necessidades até o acompanhamento da arrecadação e da compra dos materiais.
