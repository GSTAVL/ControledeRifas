# Lista SharePoint: Rifas

## Finalidade

Armazenar os registros das vendas de rifas realizados pelo aplicativo RifasJess.

## Nome utilizado no Power Apps

RifasLista

## Estruturas

| Nome exibido        | Tipo SharePoint      | Obrigatório | Exemplo                 |
|---------------------|----------------------|-------------|-------------------------|
| Comprador           | Texto de linha única | Sim         | Cliente Demonstração    |
| Quantidade          | Número               | Sim         | 5                       |
| Método de pagamento | Escolha              | Sim         | PIX                     |
| Valor               | Moeda                | Sim         | 25,00                   |
| Anexos              | Anexos               | Não         | comprovante-exemplo.pdf |

## Opções de método de pagamento

- PIX
- Dinheiro
- Cartão

## Regras

- O comprador deve ser informado.
- A quantidade deve ser maior que zero.
- O método de pagamento deve ser selecionado.
- O valor corresponde à quantidade multiplicada pelo valor unitário da rifa.
- A edição deve atualizar o registro existente.

## Utilização no aplicativo

A lista é utilizada:

- pelo formulário `frmRifas`;
- pela galeria `glrRifas`;
- pela pesquisa por comprador;
- pela funcionalidade de edição.
