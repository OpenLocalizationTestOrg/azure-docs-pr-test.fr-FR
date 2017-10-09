---
title: "aaaCollecting données Analytique de journal avec un runbook dans Azure Automation | Documents Microsoft"
description: "Didacticiel étape par étape qui guide à travers la création d’un runbook dans le référentiel d’OMS hello pour l’analyse par Analytique de journal dans les données de toocollect Azure Automation."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: operations-management-suite
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: bwren
ms.openlocfilehash: e644dc3ef20fb1e930cae02e0fd44ccca31dc13d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-data-in-log-analytics-with-an-azure-automation-runbook"></a>Collecter des données dans Log Analytics avec un runbook Azure Automation
Vous pouvez collecter une quantité importante de données dans Log Analytics à partir de diverses sources, y compris des [sources de données](../log-analytics/log-analytics-data-sources.md) sur les agents et les [données recueillies à partir d’Azure](../log-analytics/log-analytics-azure-storage.md).  Il existe un scénario où vous avez besoin des données de toocollect qui n’est pas accessible via ces sources standards.  Dans ce cas, vous pouvez utiliser hello [API du collecteur de données HTTP](../log-analytics/log-analytics-data-collector-api.md) toowrite données tooLog Analytique à partir de n’importe quel client de l’API REST.  Un tooperform méthode commune cette collecte de données à l’aide un runbook dans Azure Automation.   

Ce didacticiel vous guide tout au long processus hello pour la création et la planification d’un runbook dans Azure Automation toowrite données tooLog Analytique.


## <a name="prerequisites"></a>Composants requis
Ce scénario nécessite hello suivant les ressources configurées dans votre abonnement Azure.  Les deux peuvent être des comptes gratuits.

- [Espace de travail Log Analytics](../log-analytics/log-analytics-get-started.md).
- [Compte Azure Automation](../automation/automation-offering-get-started.md).

## <a name="overview-of-scenario"></a>Présentation du scénario
Pour ce didacticiel, vous allez écrire un runbook qui collecte les informations sur les tâches Automation.  Runbooks d’Azure Automation sont implémentés avec PowerShell, afin que vous allez commencer à écrire et tester un script dans l’éditeur d’Azure Automation hello.  Une fois que vous avez vérifié que vous collectez des informations de hello requis, vous écrire ce tooLog données Analytique et vérifier le type de données personnalisé hello.  Enfin, vous allez créer un runbook de hello planification toostart à intervalles réguliers.

> [!NOTE]
> Vous pouvez configurer Azure Automation toosend travail informations tooLog Analytique sans ce runbook.  Ce scénario est principalement le didacticiel de hello toosupport utilisés, et il est recommandé que vous envoyez un espace de travail de test à tooa hello données.  


## <a name="1-install-data-collector-api-module"></a>1. Installer le module de l’API du collecteur de données
Chaque [demande à partir de l’API du collecteur de données HTTP de hello](../log-analytics/log-analytics-data-collector-api.md#create-a-request) doit être correctement mises en forme et d’inclure un en-tête d’autorisation.  Vous pouvez l’effectuer dans votre runbook, mais vous pouvez réduire hello code nécessaire à l’aide d’un module qui simplifie ce processus.  Un module que vous pouvez utiliser est [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI) Bonjour PowerShell Gallery.

toouse un [module](../automation/automation-integration-modules.md) dans un runbook, il doit être installé dans votre compte Automation.  N’importe quel runbook dans le même compte peut ensuite utiliser de hello hello fonctions hello module.  Vous pouvez installer un module en sélectionnant **Ressources** > **Modules** > **Ajouter un module** dans votre compte Automation.  

Hello PowerShell Gallery cependant vous donne un toodeploy option rapide un module directement tooyour automation compte afin de pouvoir utiliser cette option pour ce didacticiel.  

![Module OMSIngestionAPI](media/operations-management-suite-runbook-datacollect/OMSIngestionAPI.png)

1. Accédez trop[PowerShell Gallery](https://www.powershellgallery.com/).
2. Recherchez **OMSIngestionAPI**.
3. Cliquez sur hello **déployer tooAzure Automation** bouton.
4. Sélectionnez votre compte automation, cliquez sur **OK** module de hello tooinstall.


## <a name="2-create-automation-variables"></a>2. Créer des variables Automation
Les [variables Automation](..\automation\automation-variables.md) contiennent des valeurs qui peuvent être utilisées par tous les runbooks de votre compte Automation.  Celles-ci permettent de procédures opérationnelles plus flexible en vous toochange ces valeurs sans avoir à modifier hello runbook réel. Chaque demande hello API du collecteur de données HTTP nécessite une ID de hello et la clé de l’espace de travail OMS hello et les ressources de variables toostore idéale ces informations.  

![variables](media/operations-management-suite-runbook-datacollect/variables.png)

1. Bonjour portail Azure, accédez à compte Automation de tooyour.
2. Sélectionnez **Variables** sous **Ressources partagées**.
2. Cliquez sur **ajouter une variable** et créer des deux variables hello Bonjour tableau suivant.

| Propriété | Valeur d’ID d’espace de travail | Valeur de clé d’espace de travail |
|:--|:--|:--|
| Nom | WorkspaceID | WorkspaceKey |
| Type | String | String |
| Valeur | Collez hello ID de l’espace de travail de votre espace de travail Analytique de journal. | Coller avec hello clé primaire ou secondaire de votre espace de travail Analytique de journal. |
| Chiffré | Non | Oui |



## <a name="3-create-runbook"></a>3. Créer un runbook

Azure Automation dispose d’un éditeur dans le portail hello où vous pouvez modifier et tester votre runbook.  Vous avez hello option toouse hello script éditeur toowork avec [PowerShell directement](../automation/automation-edit-textual-runbook.md) ou [créer un runbook graphique](../automation/automation-graphical-authoring-intro.md).  Pour ce didacticiel, vous allez travailler avec un script PowerShell. 

![Modifier un runbook](media/operations-management-suite-runbook-datacollect/edit-runbook.png)

1. Accédez à compte Automation de tooyour.  
2. Cliquez sur **Runbooks** > **Ajouter un runbook** > **Create a new runbook** (Créer un runbook).
3. Pour le nom du runbook hello, tapez **tâches d’automatisation collecter**.  Pour le type de runbook hello, sélectionnez **PowerShell**.
4. Cliquez sur **créer** toocreate hello runbook et démarrer hello l’éditeur.
5. Copiez et collez hello après le code dans les runbook hello.  Consultez toohello des commentaires dans le script de hello pour une explication du code de hello.
    
        # Get information required for hello automation account from parameter values when hello runbook is started.
        Param
        (
            [Parameter(Mandatory = $True)]
            [string]$resourceGroupName,
            [Parameter(Mandatory = $True)]
            [string]$automationAccountName
        )
        
        # Authenticate toohello Automation account using hello Azure connection created when hello Automation account was created.
        # Code copied from hello runbook AzureAutomationTutorial.
        $connectionName = "AzureRunAsConnection"
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         
        Add-AzureRmAccount `
            -ServicePrincipal `
            -TenantId $servicePrincipalConnection.TenantId `
            -ApplicationId $servicePrincipalConnection.ApplicationId `
            -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
        
        # Set hello $VerbosePreference variable so that we get verbose output in test environment.
        $VerbosePreference = "Continue"
        
        # Get information required for Log Analytics workspace from Automation variables.
        $customerId = Get-AutomationVariable -Name 'WorkspaceID'
        $sharedKey = Get-AutomationVariable -Name 'WorkspaceKey'
        
        # Set hello name of hello record type.
        $logType = "AutomationJob"
        
        # Get hello jobs from hello past hour.
        $jobs = Get-AzureRmAutomationJob -ResourceGroupName $resourceGroupName -AutomationAccountName $automationAccountName -StartTime (Get-Date).AddHours(-1)
        
        if ($jobs -ne $null) {
            # Convert hello job data toojson
            $body = $jobs | ConvertTo-Json
        
            # Write hello body tooverbose output so we can inspect it if verbose logging is on for hello runbook.
            Write-Verbose $body
        
            # Send hello data tooLog Analytics.
            Send-OMSAPIIngestionFile -customerId $customerId -sharedKey $sharedKey -body $body -logType $logType -TimeStampField CreationTime
        }


## <a name="4-test-runbook"></a>4. Tester le runbook
Azure Automation inclut un environnement trop[tester votre runbook](../automation/automation-testing-runbook.md) avant de le publier.  Vous pouvez inspecter les données hello collectées par les runbook hello et vérifiez qu’il écrit tooLog Analytique comme prévu avant sa publication tooproduction. 
 
![Tester le runbook](media/operations-management-suite-runbook-datacollect/test-runbook.png)

6. Cliquez sur **enregistrer** toosave hello runbook.
1. Cliquez sur **Test volet** runbook de hello tooopen dans l’environnement de test hello.
3. Depuis votre runbook possède des paramètres, vous êtes valeurs demandées par invite tooenter pour eux.  Entrez le nom hello hello du groupe de ressources et automatisation de hello qui compte vos informations de tâche toocollect continu à partir de.
4. Cliquez sur **Démarrer** toohello démarrer hello runbook.
3. Hello runbook démarre avec l’état **en file d’attente** avant d’entrer trop**en cours d’exécution**.  
3. Hello runbook doit afficher la sortie des commentaires avec les travaux hello collectées au format json.  Si aucune tâche n’est répertorié, puis qu’il n’y ait aucune tâche créée dans le compte d’automatisation hello Bonjour dernière heure.  Essayez de démarrer n’importe quel runbook dans le compte d’automatisation hello et puis effectuez à nouveau le test de hello.
4. Vérifiez que la sortie de hello n’affiche pas que les erreurs de hello valider commande tooLog Analytique.  Vous devez disposer d’un message similaire toohello.

    ![Sortie post](media/operations-management-suite-runbook-datacollect/post-output.png)

## <a name="5-verify-records-in-log-analytics"></a>5. Vérifier les enregistrements dans Log Analytics
Une fois hello runbook s’est terminée dans le test, et vous avez vérifié que le résultat de hello a été reçue, vous pouvez vérifier que les enregistrements de hello ont été créés à l’aide un [recherche de journal dans le journal Analytique](../log-analytics/log-analytics-log-searches.md).

![Sortie du journal](media/operations-management-suite-runbook-datacollect/log-output.png)

1. Bonjour portail Azure, sélectionnez votre espace de travail Analytique de journal.
2. Cliquez sur **Recherche dans les journaux**.
3. Hello type commande suivante `Type=AutomationJob_CL` et cliquez sur le bouton de recherche hello. Notez que le type d’enregistrement hello inclut _CL n’est pas spécifié dans le script de hello.  Ce suffixe est ajouté automatiquement toohello journal type tooindicate qu’il s’agit d’un type de journal personnalisé.
4. Vous devez voir un ou plusieurs enregistrements retournées indiquant que ce runbook hello fonctionne comme prévu.


## <a name="6-publish-hello-runbook"></a>6. Publier hello runbook
Une fois que vous avez vérifié que runbook hello fonctionne correctement, vous devez toopublish il est donc vous pouvez l’exécuter en production.  Vous pouvez continuer tooedit et hello runbook de test sans modifier la version publiée de hello.  

![Publier le runbook](media/operations-management-suite-runbook-datacollect/publish-runbook.png)

1. Compte d’automatisation tooyour de retour.
2. Cliquez sur **Runbooks** et sélectionnez **Collect-Automation-jobs**.
3. Cliquez sur **Modifier**, puis sur **Publier**.
4. Cliquez sur **Oui** lorsque tooverify fréquentes que vous souhaitez toooverwrite hello précédemment version publiée.

## <a name="7-set-logging-options"></a>7. Définir les options de journalisation 
Pour le test, vous ont été en mesure de tooview [documenté](../automation/automation-runbook-output-and-messages.md#message-streams) car vous définir la variable de hello $VerbosePreference dans le script de hello.  Pour la production, vous devez les propriétés de journalisation de hello de tooset pour hello runbook si vous souhaitez que la sortie des commentaires tooview.  Runbook hello utilisé dans ce didacticiel, les données de json hello envoyées tooLog Analytique s’affiche.

![Journalisation et suivi](media/operations-management-suite-runbook-datacollect/logging.png)

1. Dans Propriétés hello votre runbook sélectionnez **journalisation et le suivi** sous **Runbook paramètres**.
2. Modification du paramètre hello pour **journaliser les enregistrements détaillés** trop**sur**.
3. Cliquez sur **Enregistrer**.

## <a name="8-schedule-runbook"></a>8. Planifier un runbook
Bonjour courants toostart façon un runbook qui collecte les données d’analyse est tooschedule il toorun automatiquement.  Pour cela, vous devez créer un [planification dans Azure Automation](../automation/automation-schedules.md) et en l’attachant tooyour runbook.

![Planifier un runbook](media/operations-management-suite-runbook-datacollect/schedule-runbook.png)

1. Dans Propriétés hello votre runbook, sélectionnez **planifications** sous **ressources**.
2. Cliquez sur **ajouter une planification** > **liez un runbook de tooyour planification** > **créer une planification**.
5. Type Bonjour suivant de valeurs pour la planification de hello et cliquez sur **créer**.

| Propriété | Valeur |
|:--|:--|
| Nom | AutomationJobs-Hourly |
| Démarrages | Sélectionnez n’importe quel moment passées au moins 5 minutes hello heure actuelle. |
| Périodicité | Récurrent |
| Répéter toutes les | 1 heure |
| Définir une expiration | Non |

Une fois que la planification de hello est créée, vous devez tooset les valeurs de paramètre hello qui seront utilisés chaque fois que cette planification démarre hello runbook.

6. Cliquez sur **Configure parameters and run settings (Configurer les paramètres et les paramètres d’exécution)**.
7. Renseignez les valeurs pour **ResourceGroupName** et **AutomationAccountName**.
8. Cliquez sur **OK**. 

## <a name="9-verify-runbook-starts-on-schedule"></a>9. Vérifier la conformité du démarrage du runbook avec la planification
À chaque démarrage d’un runbook, [un travail est créé](../automation/automation-runbook-execution.md) et toute sortie est enregistrée.  En fait, il s’agit de hello collecte les mêmes tâches que hello runbook.  Vous pouvez vérifier que ce runbook hello démarre comme prévu en vérifiant les travaux hello pour hello runbook après hello pour la planification de hello a commencé.

![Tâches](media/operations-management-suite-runbook-datacollect/jobs.png)

1. Dans Propriétés hello votre runbook, sélectionnez **travaux** sous **ressources**.
2. Vous devez voir qu'une liste de tâches pour chaque runbook hello de temps a été démarrée.
3. Cliquez sur l’un des hello travaux tooview ses détails.
4. Cliquez sur **tous les journaux** tooview hello journaux et sortie à partir de runbook de hello.
5. Faites défiler toohello bas toofind une entrée toohello une image similaire ci-dessous.<br>![Détaillé](media/operations-management-suite-runbook-datacollect/verbose.png)
6. Cliquez sur cette entrée tooview hello détaillées des données json qui a été envoyées tooLog Analytique.



## <a name="next-steps"></a>Étapes suivantes
- Utilisez [Concepteur de vue](../log-analytics/log-analytics-view-designer.md) toocreate un affichage hello des données que vous avez collectées référentiel d’Analytique de journal toohello.
- Package de votre runbook dans un [solution de gestion](operations-management-suite-solutions-creating.md) toodistribute toocustomers.
- En savoir plus sur [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).
- En savoir plus sur [Azure Automation](https://docs.microsoft.com/azure/automation/).
- En savoir plus sur hello [API du collecteur de données HTTP](../log-analytics/log-analytics-data-collector-api.md).
