# Lista SharePoint: Materiais

## Finalidade

Armazenar os materiais necessários para a campanha de arrecadação.

## Nome utilizado no Power Apps

MateriaisLista

## Estrutura

| Nome exibido | Tipo SharePoint      | Obrigatório | Exemplo      |
|--------------|----------------------|-------------|--------------|
| Material     | Texto de linha única | Sim         | Bisturi      |
| Quantidade   | Número               | Sim         | 5            |
| Valor        | Moeda                | Sim         | 100,00       |
| Status       | Escolha              | Sim         | Não Comprado |
| Condição     | Escolha              | Sim         | Novo         |

## Configuração do campo Status

Opções:

- Comprado
- Não Comprado

Valor utilizado inicialmente:

- Não Comprado

## Configuração do campo Condição

Opções:

- Novo
- Adicionar outras opções existentes

## Utilização no aplicativo

A lista é utilizada:

- pelo formulário `frmMateriais`;
- pela galeria `glrMateriais`;
- pelo campo de pesquisa;
- pela funcionalidade de edição.