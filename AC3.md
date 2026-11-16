# AC3 - Controle de compra dos materiais

## Status

Concluída.

## Objetivo

Implementar o controle de compra dos materiais cadastrados, permitindo confirmar uma compra, atualizar o status no SharePoint e acompanhar o progresso diretamente na tela **Materiais**.

## Contexto

A AC3 evolui o módulo de materiais criado na AC1 e preserva o módulo de rifas da AC2. A principal mudança é a utilização efetiva do campo `Status` da lista `MateriaisLista`.

## Requisitos funcionais

1. Exibir o ícone de carrinho em cada material da galeria.
2. Armazenar o material selecionado ao clicar no carrinho.
3. Solicitar confirmação antes de alterar o status.
4. Manter o registro inalterado quando a operação for cancelada.
5. Atualizar o campo `Status` para `Comprado` após a confirmação.
6. Salvar a alteração na lista SharePoint.
7. Destacar visualmente os materiais comprados.
8. Exibir a quantidade comprada em relação ao total cadastrado.
9. Atualizar a galeria e o contador após a operação.
10. Preservar as funcionalidades implementadas nas AC1 e AC2.

## Fluxo de compra

1. O usuário acessa a tela **Materiais**.
2. O usuário seleciona o carrinho do material desejado.
3. O aplicativo armazena o registro selecionado em uma variável.
4. Uma confirmação é apresentada.
5. O usuário escolhe entre confirmar ou cancelar.
6. Ao confirmar, o aplicativo atualiza o campo `Status` para `Comprado`.
7. A fonte de dados é atualizada.
8. O material recebe uma indicação visual de compra.
9. O contador é recalculado.

## Implementação em Power Fx

### Seleção do material

No `OnSelect` do carrinho:

```powerfx
Set(varMaterialCompra; ThisItem);;
Set(varConfirmarCompra; true)
```

### Confirmação da compra

No botão **Confirmar**:

```powerfx
Patch(
    MateriaisLista;
    varMaterialCompra;
    {
        Status: { Value: "Comprado" }
    }
);;
Refresh(MateriaisLista);;
Set(varConfirmarCompra; false);;
Notify(
    "Material marcado como comprado.";
    NotificationType.Success
)
```

### Cancelamento

No botão **Cancelar**:

```powerfx
Set(varConfirmarCompra; false);;
Set(varMaterialCompra; Blank())
```

### Contador

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

Exemplo de resultado:

```text
2 de 7 materiais comprados
```

### Destaque visual

Exemplo para a propriedade `TemplateFill` da galeria:

```powerfx
If(
    ThisItem.Status.Value = "Comprado";
    RGBA(220; 252; 231; 1);
    Color.Transparent
)
```

Exemplo de texto de situação:

```powerfx
If(
    ThisItem.Status.Value = "Comprado";
    "Comprado";
    "Pendente"
)
```

## Fonte de dados

A AC3 utiliza a fonte:

```text
MateriaisLista
```

O campo utilizado para controlar a compra é:

| Campo | Tipo | Valores |
|---|---|---|
| Status | Escolha | `Não Comprado`, `Comprado` |

O valor padrão deve ser `Não Comprado`.

## Telas impactadas

### Materiais

Alterações principais:

- carrinho ativo;
- confirmação da compra;
- atualização do status;
- indicação dos materiais comprados;
- contador dinâmico;
- preservação da pesquisa e da edição.

### Início

A tela permanece como menu de navegação. Os indicadores financeiros não fazem parte da AC3.

### Rifas e Adicionar Rifas

As funcionalidades da AC2 permanecem disponíveis, sem integração financeira com os materiais nesta etapa.

### Adicionar Materiais

O cadastro e a edição implementados na AC1 permanecem disponíveis. Todo novo material deve iniciar como `Não Comprado`.

## Critérios de aceite

- [x] O carrinho aparece na galeria de materiais.
- [x] O material selecionado é identificado corretamente.
- [x] O aplicativo solicita confirmação.
- [x] Cancelar não altera o registro.
- [x] Confirmar atualiza o status para `Comprado`.
- [x] A mudança é persistida no SharePoint.
- [x] O item comprado recebe indicação visual.
- [x] O contador exibe comprados e total cadastrado.
- [x] A galeria é atualizada após a compra.
- [x] Cadastro, pesquisa e edição de materiais continuam funcionando.
- [x] O módulo de rifas continua funcionando.

## Testes

| Cenário | Ação | Resultado esperado |
|---|---|---|
| Cancelamento | Clicar no carrinho e cancelar | O status permanece `Não Comprado` |
| Confirmação | Clicar no carrinho e confirmar | O status muda para `Comprado` |
| Persistência | Abrir a lista SharePoint | O registro apresenta `Comprado` |
| Contador | Confirmar uma compra | A quantidade comprada aumenta em uma unidade |
| Atualização visual | Confirmar uma compra | O material recebe o destaque configurado |
| Inclusão | Cadastrar um novo material | O registro inicia como `Não Comprado` |
| Edição | Editar um material existente | O mesmo registro é atualizado |

## Limites da entrega

A AC3 não implementa:

- cálculo do valor total arrecadado;
- cálculo do valor necessário para os materiais;
- cálculo do saldo restante;
- dashboard financeiro integrado.

Essas funcionalidades serão desenvolvidas na Prova Final.

## Arquivo do aplicativo

```text
app/RifasJess_AC3.msapp
```

## Documentação relacionada

- [`README.md`](./README.md)
- [`docs/ARQUITETURA.md`](./docs/ARQUITETURA.md)
- [`docs/MODELO_DE_DADOS.md`](./docs/MODELO_DE_DADOS.md)
- [`sharepoint/LISTA_MATERIAIS.md`](./sharepoint/LISTA_MATERIAIS.md)
- [`sharepoint/README.md`](./sharepoint/README.md)
