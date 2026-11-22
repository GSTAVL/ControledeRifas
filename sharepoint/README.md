## Utilização na versão final

A versão final utiliza simultaneamente as listas Materiais e Rifas.

### Dados obtidos da lista Materiais

- valor necessário;
- total de materiais;
- materiais comprados;
- materiais pendentes.

### Dados obtidos da lista Rifas

- valor arrecadado.

### Integração

As listas não precisam possuir uma coluna de relacionamento.

O Power Apps consulta as duas fontes e calcula os indicadores do dashboard por meio de fórmulas Power Fx.

## Atualização dos dados

Ao abrir a tela inicial, o aplicativo executa a atualização das fontes e recalcula os indicadores.

## Exportação para Excel

A exportação para Excel pode ser usada como backup ou conferência.

O dashboard não utiliza Excel como fonte. Os indicadores são calculados diretamente a partir das listas do SharePoint.
