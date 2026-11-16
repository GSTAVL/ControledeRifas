# Modelo de dados

## Visão geral

O aplicativo **RifasJess** utiliza duas listas do **Microsoft SharePoint** como fontes de dados:

- **Materiais**, utilizada no cadastro e no controle de compra dos materiais;
- **RifasLista**, utilizada no cadastro e na consulta das rifas adquiridas.

Na AC3, as listas continuam independentes. A principal alteração no modelo é a utilização efetiva do campo `Status` da lista **Materiais** para controlar as compras.

## Lista Materiais

A lista **Materiais** armazena os itens necessários para a campanha.

### Campos utilizados

| Campo | Tipo no SharePoint | Obrigatório | Descrição | Exemplo |
|---|---|---:|---|---|
| ID | Número automático | Sim | Identificador único do registro | 7 |
| Title | Texto de linha única | Sim | Nome do material | Bisturi |
| Quantidade | Número | Sim | Quantidade necessária | 5 |
| Valor | Moeda | Sim | Valor total do material | R$ 100,00 |
| Status | Escolha | Sim | Situação de compra do material | Não Comprado |
| Condição | Escolha | Sim | Condição esperada do material | Novo |

### Opções do campo Status

- `Não Comprado`
- `Comprado`

O valor padrão recomendado é:

```text
Não Comprado
```

### Opções do campo Condição

- `Novo`
- outras opções definidas na lista, quando necessárias ao projeto.

### Uso do Status na AC3

Na AC1, o campo `Status` já fazia parte da estrutura da lista, mas a automação de compra ainda não era utilizada. Na AC3, o campo controla efetivamente o estado de cada material.

Fluxo esperado:

```text
Não Comprado → confirmação do usuário → Comprado
```

A alteração é persistida no SharePoint por meio de uma fórmula Power Fx. Como `Status` é uma coluna do tipo **Escolha**, a atualização pode seguir este formato:

```powerfx
Patch(
    Materiais;
    varMaterialCompra;
    { Status: { Value: "Comprado" } }
)
```

### Regras de integridade da lista Materiais

- `Title` não pode ficar vazio.
- `Quantidade` deve ser um número inteiro maior que zero.
- `Valor` deve ser um valor monetário igual ou maior que zero.
- `Status` deve conter somente uma das opções configuradas.
- Todo novo material deve iniciar, por padrão, como `Não Comprado`.
- A compra deve atualizar o registro pelo identificador do item selecionado, e não somente pelo nome do material.

## Lista RifasLista

A lista **RifasLista** armazena as rifas adquiridas na campanha.

### Campos utilizados na AC2 e preservados na AC3

| Nome exibido        | Tipo no SharePoint   | Obrigatório | Descrição                            | Exemplo                 |
|---------------------|----------------------|-------------|--------------------------------------|-------------------------|
| Comprador           | Texto de linha única | Sim         | Nome do comprador                    | Cliente Demonstração    |
| Quantidade          | Número               | Sim         | Quantidade de rifas adquiridas       | 5                       |
| Método de pagamento | Escolha              | Sim         | Forma de pagamento                   | PIX                     |
| Valor               | Moeda                | Sim         | Valor total do registro              | R$ 50,00                |
| Anexos              | Anexos               | Não         | Comprovante ou documento relacionado | comprovante-exemplo.pdf |

### Regras da lista RifasLista

- `Comprador` não pode ficar vazio.
- `Quantidade` deve ser um número inteiro maior que zero.
- `Método de pagamento` deve utilizar uma opção cadastrada na coluna de escolha.
- `Valor` deve ser armazenado como moeda.
- `Anexos` permanece opcional.

## Relacionamento entre as listas

As listas **Materiais** e **RifasLista** não possuem relacionamento direto na AC3.

- O módulo de materiais controla cadastro, edição e status de compra.
- O módulo de rifas controla compradores, quantidades, pagamentos e comprovantes.
- A integração financeira entre os módulos será implementada na Prova Final, com cálculos de valor necessário, valor arrecadado e saldo restante.
