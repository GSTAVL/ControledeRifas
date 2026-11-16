# Configuração do SharePoint

## Visão geral

O aplicativo **RifasJess** utiliza listas do **Microsoft SharePoint** como fontes de dados. Na AC3, a configuração principal está na lista **Materiais**, cujo campo `Status` controla os itens comprados e não comprados.

## Pré-requisitos

- acesso a um site do SharePoint;
- permissão para criar e editar listas;
- permissão para criar conexões no Power Apps;
- acesso ao aplicativo Canvas do projeto.

## Lista Materiais

### Criação da lista

1. Criar uma lista chamada `Materiais`.
2. Renomear visualmente a coluna `Title` para `Material`, se desejado.
3. Criar a coluna `Quantidade` como **Número**.
4. Criar a coluna `Valor` como **Moeda**, preferencialmente em real brasileiro.
5. Criar a coluna `Status` como **Escolha**.
6. Adicionar as opções `Não Comprado` e `Comprado`.
7. Definir `Não Comprado` como valor padrão do campo `Status`.
8. Criar a coluna `Condição` como **Escolha**.
9. Adicionar `Novo` e as demais opções utilizadas pelo aplicativo.

A estrutura completa está documentada em [`LISTA_MATERIAIS.md`](./LISTA_MATERIAIS.md).

## Lista RifasLista

A lista utilizada pelo módulo de rifas deve conter os campos definidos em [`LISTA_RIFASLISTA.md`](./LISTA_RIFASLISTA.md), incluindo comprador, quantidade, método de pagamento, valor e anexos.

A AC3 preserva esse módulo sem criar relacionamento direto entre as listas de rifas e materiais.

## Conexão com o Power Apps

1. Abrir o aplicativo Canvas no Power Apps Studio.
2. Acessar **Adicionar dados**.
3. Selecionar o conector **SharePoint**.
4. Informar ou selecionar o site que contém as listas.
5. Selecionar a lista `Materiais`.
6. Confirmar que o nome da fonte de dados no aplicativo é `MateriaisLista`.
7. Selecionar a lista de rifas utilizada pelo projeto.
8. Confirmar que os formulários e galerias apontam para as fontes corretas.

## Configuração necessária para a AC3

Na fonte `MateriaisLista`, o campo `Status` deve:

- ser do tipo **Escolha**;
- possuir exatamente as opções utilizadas nas fórmulas do aplicativo;
- iniciar com o valor `Não Comprado`;
- permitir que o aplicativo atualize o valor para `Comprado` após a confirmação do usuário.

Para uma coluna SharePoint do tipo **Escolha**, um exemplo de atualização é:

```powerfx
Patch(
    MateriaisLista;
    varMaterialCompra;
    { Status: { Value: "Comprado" } }
);;
Refresh(MateriaisLista)
```

## Teste da conexão

### Inclusão

1. Criar um registro pelo formulário de materiais.
2. Abrir a lista `Materiais` no SharePoint.
3. Confirmar que o registro foi criado.
4. Confirmar que o status inicial é `Não Comprado`.

### Edição

1. Alterar um registro pelo aplicativo.
2. Abrir a lista no SharePoint.
3. Confirmar que o item existente foi atualizado e que um novo item não foi criado indevidamente.

### Compra na AC3

1. Selecionar o carrinho de um material.
2. Cancelar a confirmação e verificar que o status não mudou.
3. Selecionar novamente o carrinho.
4. Confirmar a compra.
5. Abrir a lista no SharePoint.
6. Confirmar que o campo `Status` foi alterado para `Comprado`.
7. Voltar ao aplicativo e verificar a indicação visual do item.
8. Confirmar que o contador de materiais comprados foi atualizado.

## Solução de problemas

### O campo Status não atualiza

- confirmar que `Status` é uma coluna do tipo **Escolha**;
- conferir se a opção está escrita exatamente como `Comprado`;
- usar `{ Value: "Comprado" }` no `Patch`;
- confirmar que a variável de compra contém o registro completo selecionado;
- atualizar a conexão da lista no Power Apps após mudanças feitas no SharePoint.

### O aplicativo não encontra a lista

- conferir se o ambiente e a conta possuem acesso ao site;
- recriar a conexão do SharePoint no ambiente de destino;
- adicionar novamente a lista como fonte de dados;
- verificar se o nome usado nas fórmulas é `MateriaisLista`.

### O contador não corresponde à lista

- atualizar a fonte com `Refresh(MateriaisLista)` após o `Patch`;
- confirmar se a fórmula compara `Status.Value` com `Comprado`;
- verificar se existem registros com o campo `Status` vazio;
- conferir possíveis avisos de delegação no Power Apps Studio.
