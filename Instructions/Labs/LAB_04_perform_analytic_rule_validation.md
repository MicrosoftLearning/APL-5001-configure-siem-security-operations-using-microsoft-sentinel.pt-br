---
lab:
  title: 'Exercício 04: realizar ataque simulado'
  module: Guided Project - Perform a simulated attack to validate Analytic and Automation rules
---

>**Observação**: este laboratório baseia-se nos laboratórios 01, 02 e 03. Para concluir este laboratório, você precisará de uma [assinatura do Azure](https://azure.microsoft.com/free/?azure-portal=true). no qual você tem acesso administrativo.

## Diretrizes gerais

- Ao criar objetos, use as configurações padrão, a não ser que haja requisitos que exijam configurações diferentes.
- Somente crie, exclua ou modifique objetos para atingir os requisitos declarados. Alterações desnecessárias no ambiente podem afetar negativamente sua pontuação final.
- Se houver várias abordagens para alcançar uma meta, escolha sempre a abordagem que requer o mínimo de esforço administrativo.

É preciso validar que nossa implantação do Microsoft Sentinel está recebendo eventos de segurança e criando incidentes de máquinas virtuais que executam o Windows.

## Diagrama de arquitetura

![Diagrama de ataque simulado ](../Media/apl-5001-lab-diagrams-lab04.png)

## Tarefas de habilidades

Execute um ataque simulado para validar se as regras de análise e automação criam um incidente e o atribuem ao `Operator1`. Você executará um ataque de `Privilege Escalation` simples em `vm1`.

## Instruções para o exercício

### Tarefa 1 – Executar um ataque simulado de escalonamento de privilégio

Use ataques simulados para testar regras analíticas no Microsoft Sentinel. Saiba mais sobre [simulação de ataque de escalonamento de privilégio](https://github.com/redcanaryco/atomic-red-team/blob/master/atomics/T1078.003/T1078.003.md).

1. Localize e selecione a máquina virtual **vm1** no Azure e role os itens de menu até **Operações** e selecione **Executar comando**
1. No painel **executar comando**, selecione **RunPowerShellScript**
1. Copie os comandos abaixo para simular a criação de uma conta de administrador no formulário `PowerShell Script` e selecione **Executar**

    ```CommandPrompt
    net user theusernametoadd /add
    net user theusernametoadd ThePassword1!
    net localgroup administrators theusernametoadd /add
    ```

>**Observação**: certifique-se de que há apenas um comando por linha e você pode executar novamente os comandos alterando o nome de usuário.

1. Na janela `Output` você deve ver `The command completed successfully` três vezes

### Tarefa 2 – Verificar se um incidente foi criado a partir do ataque simulado

Verifique se foi criado um incidente que corresponda aos critérios da regra analítica e da automação. Saiba mais sobre o [gerenciamento de incidentes no Microsoft Sentinel](https://learn.microsoft.com/azure/sentinel/incident-investigation).

1. No `Microsoft Sentinel`, vá para a seção do menu `Threat management` e selecione **Incidentes**
1. Você verá um incidente que corresponde ao `Severity` e `Title` que você configurou na regra de `NRT` criada
1. Selecione o `Incident` e o painel `detail` será aberto
1. A atribuição `Owner` deve ser **Operator1**, criada a partir do `Automation rule`, e o `Tactics and techniques` deve ser **elevação de privilégio** (da regra `NRT`)
1. Selecione **Exibir detalhes completos** para ver todos os recursos do `Incident management` e `Incident actions`
