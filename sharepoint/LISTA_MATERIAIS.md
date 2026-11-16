# Lista SharePoint: Materiais

## Finalidade

Armazenar os materiais necessários para a campanha de arrecadação e controlar a situação de compra de cada item na AC3.

## Nome utilizado no Power Apps

```text
MateriaisLista
```

## Estrutura

| Nome exibido | Nome interno provável | Tipo no SharePoint   | Obrigatório | Exemplo      |
|--------------|-----------------------|----------------------|-------------|--------------|
| Material     | `Title`               | Texto de linha única | Sim         | Bisturi      |
| Quantidade   | `Quantidade`          | Número               | Sim         | 5            |
| Valor        | `Valor`               | Moeda                | Sim         | R$ 100,00    |
| Status       | `Status`              | Escolha              | Sim         | Não Comprado |
| Condição     | `Condição`            | Escolha              | Sim         | Novo         |

> Mesmo que a coluna `Title` seja renomeada visualmente para **Material**, o nome interno no SharePoint normalmente continua sendo `Title`.

## Configuração do campo Status

Tipo da coluna:

```text
Escolha
```

Opções:

- `Não Comprado`
- `Comprado`

Valor padrão:

```text
Não Comprado
```

Na AC3, esse campo é utilizado para registrar se o material já foi comprado. A alteração ocorre após a confirmação do usuário no aplicativo.

## Configuração do campo Condição

Tipo da coluna:

```text
Escolha
```

Opções iniciais:

- `Novo`
- outras opções existentes na lista, conforme a necessidade do projeto.

## Utilização no aplicativo

A lista é utilizada:

- pelo formulário `frmMateriais`;
- pela galeria `glrMateriais`;
- pelo campo de pesquisa de materiais;
- pela funcionalidade de inclusão;
- pela funcionalidade de edição;
- pelo ícone de carrinho da AC3;
- pela confirmação da compra;
- pelo contador de materiais comprados;
- pela indicação visual de itens comprados e pendentes.

## Fluxo de compra da AC3

1. O usuário seleciona o carrinho de um registro na galeria.
2. O aplicativo armazena o material selecionado.
3. Uma confirmação é apresentada ao usuário.
4. Se a operação for cancelada, o registro permanece inalterado.
5. Se a operação for confirmada, o campo `Status` é atualizado para `Comprado`.
6. A fonte `MateriaisLista` é atualizada.
7. A galeria e o contador refletem o novo status.

## Exemplo de atualização no Power Apps

Como `Status` é uma coluna do tipo **Escolha**, a atualização pode ser feita assim:

```powerfx
Patch(
    MateriaisLista;
    varMaterialCompra;
    {
        Status: { Value: "Comprado" }
    }
);;
Refresh(MateriaisLista)
```

A variável `varMaterialCompra` deve conter o próprio registro selecionado na galeria. Isso evita atualizar um item incorreto quando existirem materiais com nomes repetidos.

## Exemplo do contador da AC3

```powerfx
CountRows(
    Filter(
        MateriaisLista;
        Status.Value = "Comprado"
    )
) &
" de " &
CountRows(MateriaisLista) &
" materiais comprados"
```

Resultado esperado para dois itens comprados entre sete cadastrados:

```text
2 de 7 materiais comprados
```

## Regras de validação

- `Material` não pode ficar vazio.
- `Quantidade` deve ser um número inteiro maior que zero.
- `Valor` deve ser um valor monetário igual ou maior que zero.
- `Status` deve conter somente `Não Comprado` ou `Comprado`.
- Novos materiais devem iniciar com o status `Não Comprado`.
- A alteração para `Comprado` deve ocorrer somente após confirmação.

## Testes da AC3

- cadastrar um material e confirmar a criação na lista;
- editar um material e confirmar a atualização do registro existente;
- verificar se um material novo inicia como `Não Comprado`;
- clicar no carrinho e cancelar a confirmação;
- confirmar que o status não foi alterado após o cancelamento;
- clicar no carrinho e confirmar a compra;
- confirmar no SharePoint que o status mudou para `Comprado`;
- verificar a indicação visual do item comprado;
- verificar se o contador foi recalculado.
