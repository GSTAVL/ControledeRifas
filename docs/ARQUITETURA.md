# Arquitetura do projeto

## Visão geral

O **RifasJess** utiliza uma arquitetura de três camadas baseada nos recursos da **Microsoft Power Platform**. Na AC3, o aplicativo preserva os módulos de materiais e rifas das entregas anteriores e acrescenta o controle de compra dos materiais.

## Camada de apresentação

A camada de apresentação foi construída com **Microsoft Power Apps Canvas**.

Responsabilidades:

- exibição das telas **Início**, **Rifas**, **Adicionar Rifas**, **Materiais** e **Adicionar Materiais**;
- navegação entre as telas;
- formulários de inclusão e edição;
- galerias de rifas e materiais;
- pesquisa de registros por nome;
- acionamento da compra pelo ícone de carrinho;
- confirmação antes da alteração do status;
- indicação visual dos materiais comprados e pendentes;
- exibição do contador de materiais comprados;
- mensagens de sucesso, aviso e erro.

## Camada de lógica

A lógica de negócio foi implementada com fórmulas **Power Fx**.

Responsabilidades:

- definição do modo de inclusão ou edição;
- armazenamento do registro selecionado;
- pesquisa de rifas e materiais;
- validação dos formulários;
- envio e atualização dos dados;
- alteração do campo `Status` do material;
- confirmação da compra antes da persistência;
- atualização da galeria após a alteração;
- contagem dinâmica de materiais comprados e cadastrados;
- navegação após o salvamento.

### Regra de compra da AC3

O ícone de carrinho disponível em cada item da galeria inicia o fluxo de compra. O material selecionado é armazenado temporariamente e o aplicativo solicita confirmação. Após a confirmação, o campo `Status` do registro é atualizado de **Não Comprado** para **Comprado** na lista do SharePoint.

O aplicativo utiliza o próprio registro selecionado na galeria para realizar a atualização, evitando localizar materiais apenas pelo nome.

Exemplo de atualização em Power Fx:

```powerfx
Patch(
    Materiais;
    varMaterialCompra;
    { Status: { Value: "Comprado" } }
);;
Refresh(Materiais)
```

> O formato do valor atribuído ao campo `Status` depende do tipo da coluna. Para uma coluna SharePoint do tipo **Escolha**, utiliza-se `{ Value: "Comprado" }`.

### Contador de materiais

O contador da tela **Materiais** apresenta a quantidade comprada em relação ao total cadastrado, no formato:

```text
2 de 7 materiais comprados
```

Exemplo de fórmula:

```powerfx
CountRows(Filter(Materiais; Status.Value = "Comprado")) &
" de " &
CountRows(Materiais) &
" materiais comprados"
```

## Camada de dados

A persistência dos registros é realizada por listas do **Microsoft SharePoint**.

- A lista **Materiais** armazena os materiais, as quantidades, os valores, as condições e os respectivos status de compra.
- A lista **RifasLista** armazena os compradores, as quantidades de rifas, os métodos de pagamento, os valores e os anexos.

As listas permanecem independentes na AC3. A integração financeira entre rifas e materiais será realizada na Prova Final.

## Fluxo principal de materiais

1. O usuário acessa o aplicativo.
2. O usuário abre a tela **Materiais**.
3. O aplicativo consulta os registros da lista **Materiais** no SharePoint.
4. A galeria apresenta os materiais cadastrados e seus status.
5. O usuário pode pesquisar, cadastrar, editar ou iniciar a compra de um material.
6. Após cada operação, a fonte de dados e os indicadores da tela são atualizados.

## Fluxo de inclusão e edição

1. O usuário seleciona **Adicionar Novo Material** ou o ícone de edição.
2. O aplicativo define o formulário em modo de inclusão ou edição.
3. No modo de edição, o aplicativo armazena o registro selecionado.
4. O usuário preenche ou altera os dados.
5. O formulário valida os campos obrigatórios.
6. O registro é criado ou atualizado no SharePoint.
7. A galeria apresenta os dados atualizados.

## Fluxo de compra da AC3

1. O usuário seleciona o ícone de carrinho de um material.
2. O aplicativo armazena o material selecionado.
3. Uma mensagem solicita a confirmação da compra.
4. Se o usuário cancelar, nenhuma alteração é realizada.
5. Se o usuário confirmar, o status é atualizado para **Comprado** no SharePoint.
6. A galeria passa a exibir a indicação visual de material comprado.
7. O contador de materiais comprados é recalculado.
8. Uma mensagem informa que a operação foi concluída.

## Fluxo do módulo de rifas

1. O usuário abre a tela **Rifas**.
2. O aplicativo consulta os registros da lista **RifasLista**.
3. O usuário pode pesquisar um comprador, adicionar uma nova rifa ou editar um registro.
4. O formulário valida e envia os dados ao SharePoint.
5. A galeria apresenta os dados atualizados.

## Limites da AC3

A AC3 não realiza a integração financeira entre os módulos. Os cálculos de valor arrecadado, valor necessário e saldo restante ficam reservados para a Prova Final.
