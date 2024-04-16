---
lab:
  title: 'Exercício 03: validar a implantação do Sentinel'
  module: 'Guided Project - Configure Microsoft Sentinel Data Collection rules, NRT Analytic rule and Automation'
---

>**Observação**: este laboratório baseia-se nos laboratórios 01 e 02. Para concluir este laboratório, você precisará de uma [assinatura do Azure](https://azure.microsoft.com/free/?azure-portal=true). no qual você tem acesso administrativo.

## Diretrizes gerais

- Ao criar objetos, use as configurações padrão, a não ser que haja requisitos que exijam configurações diferentes.
- Somente crie, exclua ou modifique objetos para atingir os requisitos declarados. Alterações desnecessárias no ambiente podem afetar negativamente sua pontuação final.
- Se houver várias abordagens para alcançar uma meta, escolha sempre a abordagem que requer o mínimo de esforço administrativo.

Precisamos configurar o Microsoft Sentinel para receber eventos de segurança de máquinas virtuais que executam o Windows.

## Diagrama de arquitetura

![Diagrama de eventos de segurança do Windows via AMA usando DCR](../Media/apl-5001-lab-diagrams-lab03.png)

## Tarefas de habilidades

Você precisa validar a implantação do Microsoft Sentinel para atender aos seguintes requisitos:

- Configure os eventos de segurança do Windows por meio do conector AMA para coletar todos os eventos de segurança somente de uma máquina virtual chamada VM1.
- Crie uma regra de consulta NRT (quase em tempo real) para gerar um incidente com base na consulta a seguir.

```KQL
SecurityEvent 
| where EventID == 4732
| where TargetAccount == "Builtin\\Administrators"
```

- Crie uma regra de automação que atribua ao Operador1 a função Proprietário para incidentes gerados pela regra NRT.

## Instruções para o exercício

>**Observação**: nas tarefas a seguir, para acessar `Microsoft Sentinel`, selecione o `workspace` que você criou no Laboratório 01.

### Tarefa 1 – Configurar as DCRs (regras de coleta de dados) no Microsoft Sentinel

Configurar eventos de segurança do Windows via conector AMA. Aprenda mais sobre [eventos de segurança do Windows via conector AMA](https://learn.microsoft.com/azure/sentinel/data-connectors/windows-security-events-via-ama).

 1. No `Microsoft Sentinel`, vá para a seção do menu `Configuration` e selecione **Conectores de dados**
 1. Procure e selecione **eventos de segurança do Windows via AMA**
 1. Clique em **Abrir página do conector**
 1. Na área de `Configuration`, selecione **+Criar regra de coleta de dados**
 1. Na guia `Basics` insira um `Rule Name`
 1. Na guia, `Resources` expanda sua assinatura e o grupo de recursos `RG1` na coluna `Scope`
 1. Selecione `VM1` e selecione **Avançar: Coletar >**
 1. Na guia `Collect` deixe `All Security Events` com o padrão
 1. Selecione **Avançar: Revisar + criar >** e escolha **Criar**

### Tarefa 2 – Criar uma detecção de consulta NRT (quase em tempo real)

Detectar ameaças com regras de análise NRT (quase em tempo real) no Microsoft Sentinel. Saiba mais sobre [regras de análise NRT (quase em tempo real) no Microsoft Sentinel](https://learn.microsoft.com/azure/sentinel/near-real-time-rules).

 1. No `Microsoft Sentinel`, vá para a seção do menu `Configuration` e selecione **Análise**
 1. Selecione **+ Criar** e **regra de consulta NRT (Versão prévia)**
 1. Insira um `Name` para a regra e selecione **Elevação de Privilégios** em `Tactics and techniques`.
 1. Selecione **Avançar: Definir lógica da regra >**
 1. Insira a consulta KQL no formulário `Rule query`

    ```KQL
    SecurityEvent 
    | where EventID == 4732
    | where TargetAccount == "Builtin\\Administrators"
    ```

 1. Selecione **Avançar: Configurações de incidente >** e selecione **Avançar: Resposta automatizada >**
 1. Selecione **Avançar: Examinar + Criar**
 1. Após a conclusão da validação, escolha **Salvar**

### Tarefa 3 – Configurar a automação no Microsoft Sentinel 

Configurar a automação no Microsoft Sentinel. Saiba mais sobre [Criar e usar regras de automação do Microsoft Sentinel](https://learn.microsoft.com/azure/sentinel/create-manage-use-automation-rules).

 1. No `Microsoft Sentinel`, vá para a seção do menu `Configuration` e selecione **Automação**
 1. Selecione **+ Criar** e Regra de automação
 1. Insira um `Automation rule name` e selecione **Atribuir proprietário** em `Actions`
 1. Atribua **Operator1** como proprietário.
 1. Selecione **Aplicar**.
