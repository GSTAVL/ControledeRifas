<img width="4032" height="202" alt="image" src="https://github.com/user-attachments/assets/1ed52632-21b0-4c59-a664-26a6d11e809e" /># Modelo de dados

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

## Lista Rifas

A lista Rifas armanzena as rifas compradas na campanha

## Campos Utilizados na AC2

| Nome exibido        | Tipo SharePoint      | Obrigatório | Exemplo                 |
|---------------------|----------------------|-------------|-------------------------|
| Comprador           | Texto de linha única | Sim         | Cliente Demonstração    |
| Quantidade          | Número               | Sim         | 5                       |
| Método de pagamento | Escolha              | Sim         | PIX                     |
| Valor               | Moeda                | Sim         | 25,00                   |
| Anexos              | Anexos               | Não         | comprovante-exemplo.pdf |

As listas Materiais e Rifas são fontes independentes nesta etapa. A integração financeira entre os dois módulos será implementada na Prova Final por meio dos cálculos de valor necessário e valor arrecadado.
