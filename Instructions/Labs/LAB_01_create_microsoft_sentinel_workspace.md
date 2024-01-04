---
lab:
  title: 'Exercício 01: implantar o Microsoft Sentinel'
  module: Guided Project - Create and configure a Microsoft Sentinel workspace
---

>**Observação**: para concluir este laboratório, você precisará de uma [assinatura do Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) no qual você tem acesso administrativo.

## Diretrizes gerais

- Ao criar objetos, use as configurações padrão, a não ser que haja requisitos que exijam configurações diferentes.
- Somente crie, exclua ou modifique objetos para atingir os requisitos declarados. Alterações desnecessárias no ambiente podem afetar negativamente sua pontuação final.
- Se houver várias abordagens para alcançar uma meta, escolha sempre a abordagem que requer o mínimo de esforço administrativo.

Atualmente, estamos avaliando a postura de segurança em nosso ambiente corporativo. Precisamos de sua ajuda para configurar uma solução de SIEM (gerenciamento de eventos e informações de segurança) para ajudar a identificar ataques cibernéticos em andamento e futuros.

## Diagrama de arquitetura

![Diagrama com o workspace do Log Analytics.](../Media/apl-5001-lab-diagrams-01.png)

## Tarefas de habilidades

Você precisa implantar um workspace do Microsoft Sentinel. A solução deve atender aos seguintes requisitos:

- Verifique se o conjunto de dados do Sentinel está armazenado na região do Azure do oeste dos EUA.
- Garanta que todos os logs de análise do Sentinel sejam mantidos por 180 dias.
- Atribua funções ao Operador1 para garantir que ele possa gerenciar incidentes e executar guias estratégicos do Sentinel. A solução precisa usar o princípio de privilégios mínimos.

## Instruções para o exercício

### Tarefa 1 – Crie um workspace do Log Analytics

Crie um workspace do Log Analytics, incluindo a opção de região. Saiba mais sobre a [integração do Microsoft Sentinel](https://learn.microsoft.com/azure/sentinel/quickstart-onboard).

  1. No portal do Azure, pesquise e selecione `Microsoft Sentinel`.
  1. Selecione **+ Criar**.
  1. Selecione **Criar um workspace**.
  1. Selecione `RG2` como o grupo de recursos
  1. Insira um nome válido para o workspace do Log Analytics
  1. Selecione `West US` como a região do workspace.
  1. Selecione **Examinar + criar** para validar o novo workspace.
  1. Selecione **Criar** para implantar o workspace.

### Tarefa 2 – Implantar o Microsoft Sentinel em um workspace

Implantar o Microsoft Sentinel no workspace.

  1. Quando a implantação do `workspace` for concluída, selecione **Atualizar** para exibir o novo `workspace`.
  1. Selecione o `workspace` ao qual você deseja adicionar o Sentinel (criado na Tarefa 1).
  1. Selecione **Adicionar**.

### Tarefa 3 – Atribuir uma função do Microsoft Sentinel a um usuário

Atribua uma função do Microsoft Sentinel a um uso. Saiba mais sobre [Funções e permissões para trabalhar no Microsoft Sentinel](https://learn.microsoft.com/azure/sentinel/roles)

  1. Vá para o grupo de recursos RG2
  1. Selecione **IAM (Controle de acesso)** .
  1. Selecione **Adicionar** e `Add role assignment`.
  1. Na barra de pesquisa, procure e selecione a função `Microsoft Sentinel Contributor`.
  1. Selecione **Avançar**.
  1. Selecione a opção `User, group, or service principal`.
  1. Selecione **+ Selecionar membros**.
  1. Procure o `Operator1` atribuído em suas instruções `(operator1-XXXXXXXXX@LODSPRODMCA.onmicrosoft.com)` de laboratório.
  1. Selecione o `user icon`.
  1. Escolha **Selecionar**.
  1. Selecione “Revisar + atribuir“.
  1. Selecione “Revisar + atribuir“.

### Tarefa 4 – Configurar a retenção de dados

Configurar a retenção de dados [Saiba mais sobre a retenção de dados](https://learn.microsoft.com/azure/azure-monitor/logs/data-retention-archive).

  1. Vá para o `Log Analytics workspace` criado na Tarefa 1 etapa 5.
  1. Selecione **Uso e custos estimados**.
  1. Selecione **Retenção de dados**.
  1. Altere o período de retenção de dados para **180 dias**.
  1. Selecione **OK**.

>**Observação**: para prática adicional, conclua o módulo [Criar e gerenciar workspaces do Microsoft Sentinel](https://learn.microsoft.com/training/modules/create-manage-azure-sentinel-workspaces/).
