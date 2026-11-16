# Controle de Rifas - Rifas da Jess

Aplicativo desenvolvido para gerenciar os materiais necessários para uma campanha, registrar rifas e controlar a compra dos materiais por meio da Microsoft Power Platform.

## Objetivo

O **Controle de Rifas** centraliza:

- o cadastro e a edição dos materiais necessários para a campanha;
- o registro e a consulta das rifas adquiridas;
- o acompanhamento do status de compra dos materiais;
- a contagem de materiais comprados e pendentes.

A integração financeira completa entre os valores das rifas e dos materiais será realizada na Prova Final.

## Tecnologias utilizadas

- Microsoft Power Apps Canvas;
- Power Fx;
- Microsoft SharePoint Lists;
- GitHub para versionamento e documentação.

## Arquitetura

O projeto está organizado em três camadas:

- **Apresentação:** Microsoft Power Apps Canvas;
- **Lógica de negócio:** fórmulas Power Fx;
- **Persistência de dados:** listas do Microsoft SharePoint.

Mais detalhes estão disponíveis em [`docs/ARQUITETURA.md`](./docs/ARQUITETURA.md).

## Entregas

### AC1: Gestão de materiais

**Status:** concluída.

Funcionalidades:

- cadastro de materiais;
- consulta em galeria;
- pesquisa pelo nome do material;
- edição de registros;
- validação dos campos;
- integração com a lista `MateriaisLista` no SharePoint;
- definição inicial do status como `Não Comprado`.

Documentação: [`AC1.md`](./AC1.md).

### AC2: Gestão de rifas

**Status:** concluída.

Funcionalidades:

- cadastro de rifas;
- registro do comprador;
- registro da quantidade;
- seleção do método de pagamento;
- inclusão opcional de anexos;
- pesquisa e consulta dos registros;
- edição de rifas;
- integração com a lista `RifasLista` no SharePoint.

Documentação: [`AC2.md`](./AC2.md).

### AC3: Controle de compra dos materiais

**Status:** concluída.

Funcionalidades:

- ativação do carrinho na galeria de materiais;
- seleção do material que será comprado;
- confirmação antes da alteração do status;
- atualização do campo `Status` para `Comprado` no SharePoint;
- indicação visual dos materiais comprados;
- contador dinâmico no formato `2 de 7 materiais comprados`;
- atualização da galeria após a compra;
- preservação das funcionalidades das AC1 e AC2.

Documentação: [`AC3.md`](./AC3.md).

### Prova Final: Dashboard integrado

**Status:** planejada.

Escopo previsto:

- valor necessário para a compra dos materiais;
- valor arrecadado com as rifas;
- saldo restante;
- indicadores financeiros integrados.

## Estrutura do repositório

```text
ControledeRifas/
├── app/
│   ├── RifasJess.msapp
│   ├── RifasJess_AC2.msapp
│   └── RifasJess_AC3.msapp
├── docs/
│   ├── ARQUITETURA.md
│   ├── INTEGRANTES.md
│   └── MODELO_DE_DADOS.md
├── sharepoint/
│   ├── LISTA_MATERIAIS.md
│   ├── LISTA_RIFASLISTA.md
│   └── README.md
├── AC1.md
├── AC2.md
├── AC3.md
└── README.md
```

## Como executar

1. Criar as listas do SharePoint conforme a documentação da pasta [`sharepoint`](./sharepoint/).
2. Baixar o arquivo `.msapp` correspondente à entrega na pasta [`app`](./app/).
3. Importar o aplicativo no Microsoft Power Apps.
4. Criar ou atualizar as conexões com as listas `MateriaisLista` e `RifasLista`.
5. Conferir se formulários e galerias apontam para as fontes corretas.
6. Salvar, publicar e testar o aplicativo.

Para utilizar a versão mais recente, importar:

```text
app/RifasJess_AC3.msapp
```

## Modelo de dados

- A lista **Materiais** armazena material, quantidade, valor, status e condição.
- A lista **RifasLista** armazena comprador, quantidade, método de pagamento, valor e anexos.
- Na AC3, o campo `Status` da lista **Materiais** controla os valores `Não Comprado` e `Comprado`.

Consulte [`docs/MODELO_DE_DADOS.md`](./docs/MODELO_DE_DADOS.md).

## Integrante

- Gustavo Goncalves Silva

## Links

- [GitHub Project Board](https://github.com/users/GSTAVL/projects/2/views/1)
- [Vídeo da AC1](https://youtu.be/Fq4pXfdvAd0)
