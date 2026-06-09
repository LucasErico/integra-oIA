# Descrição da História:

**PARA** otimizar o atendimento de chamados e a rastreabilidade técnica de logs;

**COMO** Perfil Suporte da GSI;

**QUERO** incrementar o relatório de operações com busca por número de processo e filtros de status via toggles exclusivos.

## Critérios de Produto:

- O relatório de operações deve ser acessível **exclusivamente** para usuários com o perfil **SUPORTE**, mantendo-se independente da funcionalidade "Minhas operações".
- Deve ser implementado o campo de busca pelo **número do processo**, utilizando o componente padrão das páginas "Caixa de Entrada das Promotorias" e "Caixa de Entrada das Procuradorias".
- Devem ser incluídos dois componentes de **toggle** para filtragem de status:
    1. **Somente operações com erro**.
    2. **Somente operações com sucesso**.
- **Regra de Exclusividade**: O sistema não deve permitir que ambas as toggles estejam ligadas/habilitadas simultaneamente. Ao ligar uma, a outra deve ser desabilitada automaticamente.
- **Comportamento Padrão**: Caso ambas as toggles estejam desligadas, o sistema deve buscar **TODAS** as operações, independente do status.
- A coluna anteriormente denominada "Erro" deve ser renomeada para **"Status"**.
- A coluna **"Status"** deve estar visível em todos os cenários (todas, erro ou sucesso).
- **Estilização Visual**:
    - Operações com erro: Texto do log em **vermelho**.
    - Operações com sucesso: Exibir o texto **"Operação Realizada com Sucesso"** em **verde**.

## Critérios de Aceitação da História:

- **Controle de Acesso**: Validar que as novas opções de busca e filtros aparecem apenas para o perfil SUPORTE.
    
- **Busca por Processo**: O sistema deve filtrar corretamente as operações pelo número do processo digitado, seguindo o comportamento do componente de referência.

- **Lógica das Toggles (Filtros de Status)**:
    - **Cenário 1 (Default)**: Ambas as toggles desligadas. O sistema deve retornar todas as operações (Sucesso e Erro).
    - **Cenário 2 (Filtro Erro)**: Habilitar "Somente operações com erro". O sistema deve listar apenas falhas.
    - **Cenário 3 (Filtro Sucesso)**: Habilitar "Somente operações com sucesso". O sistema deve listar apenas sucessos.
    - **Cenário 4 (Exclusividade)**: Com a toggle de "Erro" ativa, tentar ativar a de "Sucesso". O sistema deve desativar a de "Erro" e manter apenas a de "Sucesso" ativa (e vice-versa).

- **Exibição da Coluna Status**:
    - **Sucesso**: Verificar se o texto "Operação Realizada com Sucesso" aparece em verde.
    - **Erro**: Verificar se a descrição do erro aparece em vermelho.
    - Validar que a coluna permanece visível mesmo quando o resultado da busca é misto (ambas as toggles desligadas).

## Critérios Técnicos da História:

- **Frontend**: Implementar a lógica de *interlock* nas toggles para garantir a exclusividade mútua no estado da aplicação.
- **UI/UX**: Aplicar as cores `green` (para sucesso) e `red` (para erro) na coluna Status conforme o protótipo enviado.
- **Backend/Query**: A consulta deve ser parametrizada para aceitar o filtro de status como opcional (null para todas, ou o valor específico quando uma toggle estiver ativa).

## Protótipo:

### Implementação de Filtros e Busca
![relatorio_operacoes_toggles.png](../../../_assets/ajuste_relatorio_operacoes/relatorio_operacoes_toggles.png)
*Demonstração da inclusão das duas toggles e do campo de busca por processo no cabeçalho do relatório.*

### Listagem de Operações com Erro
![relatorio_operacoes_erro.png](../../../_assets/ajuste_relatorio_operacoes/relatorio_operacoes_erro.png)
*Visualização da coluna "Status" renomeada e logs de erro destacados em vermelho.*

### Listagem de Operações com Sucesso
![relatorio_operacoes_sucesso.png](../../../_assets/ajuste_relatorio_operacoes/relatorio_operacoes_sucesso.png)
*Visualização da coluna "Status" preenchida com o texto padrão de sucesso destacado em verde.*