# RifasJess

Aplicativo desenvolvido em Microsoft Power Apps para gerenciar materiais, registrar vendas de rifas, acompanhar compras e controlar financeiramente uma campanha de arrecadação.

## Objetivo

O RifasJess foi criado para centralizar o acompanhamento de uma campanha baseada na venda de rifas.

O sistema permite:

- cadastrar os materiais necessários;
- registrar as vendas de rifas;
- pesquisar e editar registros;
- controlar quais materiais já foram comprados;
- acompanhar o valor necessário;
- acompanhar o valor arrecadado;
- calcular o valor restante ou excedente;
- visualizar o progresso das compras.

## Tecnologias utilizadas

- Microsoft Power Apps Canvas;
- Power Fx;
- Microsoft SharePoint Lists;
- Microsoft 365;
- GitHub;
- GitHub Projects.

## Arquitetura

O projeto utiliza uma arquitetura de três camadas:

- **Front-end:** Microsoft Power Apps Canvas;
- **Lógica de negócio:** fórmulas Power Fx;
- **Persistência de dados:** listas do Microsoft SharePoint.

## Fontes de dados

O aplicativo utiliza duas listas do SharePoint:

### MateriaisLista

Armazena os materiais necessários para a campanha.

Principais campos:

- Material;
- Quantidade;
- Valor;
- Status;
- Condição.

### RifasLista

Armazena as vendas de rifas.

Principais campos:

- Nome do comprador;
- Quantidade de rifas;
- Método de pagamento;
- Valor;
- Anexos.

## Entregas do projeto

### AC1: Gestão de materiais

Status: concluída.

Funcionalidades:

- tela inicial;
- navegação;
- cadastro de materiais;
- consulta dos materiais;
- pesquisa pelo nome;
- edição;
- validação dos campos;
- integração com a lista de materiais do SharePoint.

### AC2: Gestão de rifas

Status: concluída.

Funcionalidades:

- acesso ao módulo de rifas;
- cadastro de vendas;
- consulta dos registros;
- pesquisa pelo comprador;
- edição;
- método de pagamento;
- cálculo do valor da venda;
- anexo opcional;
- integração com a lista de rifas do SharePoint.

### AC3: Controle de compra dos materiais

Status: concluída.

Funcionalidades:

- utilização do ícone de carrinho;
- confirmação da compra;
- atualização do status do material;
- identificação visual de material comprado;
- contador de materiais comprados;
- persistência da mudança de status no SharePoint.

### Prova Final: Dashboard integrado

Status: concluída.

Funcionalidades:

- cálculo do valor necessário;
- cálculo do valor arrecadado;
- cálculo do valor restante ou excedente;
- quantidade de materiais comprados;
- quantidade de materiais pendentes;

## Regras financeiras

### Valor necessário

Corresponde à soma dos valores cadastrados na lista de materiais.

### Valor arrecadado

Corresponde à soma dos valores registrados nas vendas de rifas.

### Valor restante

É calculado por:

`Valor necessário - Valor arrecadado`

Quando o valor arrecadado é maior que o necessário, o sistema apresenta o valor como excedente.

### Progresso da arrecadação

É calculado por:

`Valor arrecadado / Valor necessário`

### Progresso das compras

É calculado pela quantidade de materiais com status `Comprado` em relação ao total de materiais cadastrados.

## Estrutura do repositório

- `app`: exportações do Canvas App;
- `docs`: documentação técnica;
- `sharepoint`: documentação das listas;
- `entregas`: documentação de cada etapa;
- `evidencias`: capturas das funcionalidades;
- `CHANGELOG.md`: histórico de evolução do projeto.

## Como executar

1. Criar as listas de SharePoint conforme a documentação da pasta `sharepoint`.
2. Importar o arquivo `RifasJess_Final.msapp` no Power Apps.
3. Atualizar as conexões com as listas SharePoint.
4. Confirmar os nomes das fontes `MateriaisLista` e `RifasLista`.
5. Salvar e publicar o aplicativo.
6. Executar os testes de inclusão, edição, compra e atualização do dashboard.

## Integrante

- Gustavo Goncalves Silva

## Links

- GitHub Project Board: ADICIONAR_LINK_DO_BOARD
- Vídeo da AC1: ADICIONAR_LINK
- Vídeo da AC2: ADICIONAR_LINK
- Vídeo da AC3: ADICIONAR_LINK
- Vídeo da Prova Final: ADICIONAR_LINK
