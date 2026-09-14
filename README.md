# Controle de Rifas - Rifas da Jess

Aplicativo desenvolvido para gerenciamento de materiais e acompanhamento de uma campanha de arrecadação por meio de rifas.

## Objetivo

O objetivo do Controle de Rifas é centralizar o cadastro dos materiais necessários para uma campanha, registrar as rifas vendidas e acompanhar a evolução financeira da arrecadação.

## Tecnologias utilizadas

- Microsoft Power Apps Canvas
- Power Fx
- Microsoft SharePoint Lists

## Arquitetura

O projeto está organizado em três camadas:

- Front-end: Power Apps Canvas
- Lógica de negócio: fórmulas Power Fx
- Persistência de dados: listas do SharePoint

## Entrega atual

### AC1: Gerenciamento básico de materiais

A primeira entrega apresenta o cadastro, consulta, pesquisa e edição dos materiais.

## Funcionalidades da AC1

- Navegação entre as telas
- Cadastro de materiais
- Validação dos campos obrigatórios
- Armazenamento dos registros no SharePoint
- Listagem dos materiais em uma galeria
- Pesquisa de materiais pelo nome
- Edição de materiais existentes
- Mensagens de sucesso e erro

## Estrutura do repositório

- `app`: exportações do Canvas App
- `docs`: documentação técnica
- `sharepoint`: documentação das listas
- `entregas`: descrição de cada entrega
- `evidencias`: imagens das funcionalidades

## Como executar

1. Criar a lista do SharePoint conforme a documentação da pasta `sharepoint`.
2. Importar o arquivo `.msapp` disponível na pasta `app`.
3. Atualizar a conexão do aplicativo para apontar para a lista criada.
4. Salvar e publicar o aplicativo.

## Integrantes

- Gustavo Goncalves Silva

## Links

- GitHub Project Board: [adicionar link](https://github.com/users/GSTAVL/projects/2/views/1)
- Vídeo da AC1: [adicionar link](https://youtu.be/Fq4pXfdvAd0)
