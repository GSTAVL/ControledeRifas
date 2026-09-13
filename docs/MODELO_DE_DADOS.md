# Modelo de dados

## Lista Materiais

A lista Materiais armazena os itens necessários para a campanha.

### Campos utilizados na AC1

| Campo      | Tipo              | Obrigatório | Descrição                 |
|------------|-------------------|-------------|---------------------------|
| ID         | Número automático | Sim         | Identificador do registro |
| Title      | Texto             | Sim         | Nome do material          |
| Quantidade | Número            | Sim         | Quantidade necessária     |
| Valor      | Moeda             | Sim         | Valor total do material   |
| Status     | Escolha           | Sim         | Situação de compra        |
| Condição   | Escolha           | Sim         | Condição do material      |

### Opções do campo Status

- Comprado
- Não Comprado

### Opções do campo Condição

- Novo
- Adicionar outras opções existentes

## Observação sobre a AC1

Embora Status e Condição já existam na estrutura da lista, a automação para marcar materiais como comprados será apresentada em uma entrega posterior.

Na AC1, o status inicial utilizado é Não Comprado.