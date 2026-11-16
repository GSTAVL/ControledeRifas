# AC1 - Gestão de materiais

## Status

Concluída.

## Objetivo

Implementar o módulo inicial de gerenciamento dos materiais necessários para a campanha, utilizando um aplicativo Canvas conectado a uma lista do Microsoft SharePoint.

## Escopo

A AC1 contempla:

- cadastro de materiais;
- listagem dos materiais cadastrados;
- pesquisa pelo nome;
- edição dos registros;
- validação dos campos do formulário;
- persistência no SharePoint;
- preparação do campo de status para entregas posteriores.

## Funcionalidades implementadas

### Cadastro de materiais

O usuário pode cadastrar um material informando:

- nome do material;
- quantidade necessária;
- valor;
- status;
- condição.

O status inicial utilizado é `Não Comprado`.

### Consulta e pesquisa

A tela **Materiais** apresenta os registros da lista `MateriaisLista` em uma galeria. O campo de pesquisa permite localizar um material pelo nome.

Exemplo de fórmula:

```powerfx
Filter(
    MateriaisLista;
    IsBlank(txtPesquisaMaterial.Text) ||
    StartsWith(Title; txtPesquisaMaterial.Text)
)
```

### Edição

O ícone de lápis armazena o registro selecionado, abre o formulário em modo de edição e permite atualizar o item existente.

Exemplo:

```powerfx
Set(varMaterialSelecionado; ThisItem);;
EditForm(frmMateriais);;
Navigate('Adicionar Materiais'; ScreenTransition.Fade)
```

### Inclusão

O botão **Adicionar Novo Material** limpa a seleção anterior e abre o formulário em modo de inclusão.

```powerfx
Set(varMaterialSelecionado; Blank());;
NewForm(frmMateriais);;
Navigate('Adicionar Materiais'; ScreenTransition.Fade)
```

## Fonte de dados

A AC1 utiliza a lista SharePoint **Materiais**, conectada ao Power Apps com o nome:

```text
MateriaisLista
```

Campos principais:

| Campo | Tipo | Finalidade |
|---|---|---|
| Material (`Title`) | Texto | Nome do material |
| Quantidade | Número | Quantidade necessária |
| Valor | Moeda | Valor total do material |
| Status | Escolha | Situação de compra |
| Condição | Escolha | Condição do material |

A estrutura completa está em [`sharepoint/LISTA_MATERIAIS.md`](./sharepoint/LISTA_MATERIAIS.md).

## Regras de validação

- o nome do material é obrigatório;
- a quantidade deve ser maior que zero;
- o valor deve ser igual ou maior que zero;
- o status deve utilizar uma opção válida da lista;
- novos materiais devem iniciar como `Não Comprado`.

## Telas relacionadas

- **Início:** acesso ao módulo de materiais;
- **Materiais:** consulta, pesquisa e edição;
- **Adicionar Materiais:** inclusão e atualização dos registros.

## Critérios de aceite

- [x] O usuário consegue cadastrar um material.
- [x] O registro é criado na lista do SharePoint.
- [x] A galeria exibe os materiais cadastrados.
- [x] A pesquisa localiza materiais pelo nome.
- [x] O usuário consegue editar um registro existente.
- [x] O formulário valida os campos obrigatórios.
- [x] O status inicial é `Não Comprado`.

## Limites da entrega

A AC1 não executa a compra do material. O campo `Status` é preparado para uso posterior, mas a alteração pelo carrinho é implementada somente na AC3.

## Arquivo do aplicativo

```text
app/RifasJess.msapp
```
