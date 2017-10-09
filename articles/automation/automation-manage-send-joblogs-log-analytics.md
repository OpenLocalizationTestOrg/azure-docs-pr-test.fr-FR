---
title: "aaaForward tooOMS de données de tâche Azure Automation Analytique de journal | Documents Microsoft"
description: "Cet article explique comment toosend état et le runbook projet flux gestion un éclairage supplémentaire tooMicrosoft Operations Management Suite journal Analytique toodeliver."
services: automation
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: c12724c6-01a9-4b55-80ae-d8b7b99bd436
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/02/2017
ms.author: magoedte
ms.openlocfilehash: e78b6c6677d6502711ce828e2d32b7a91922ae26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="forward-job-status-and-job-streams-from-automation-toolog-analytics-oms"></a>Transférer l’état du travail et flux de travail à partir de l’Automation tooLog Analytique (OMS)
Automation peut envoyer des runbook travail état et la tâche de flux de données tooyour Analytique de journal de Microsoft Operations Management Suite (OMS) espace de travail.  Journaux du travail et flux de travail sont visibles dans hello portail Azure, ou avec PowerShell, pour des travaux individuels et cela vous permet des enquêtes simple tooperform. Désormais avec Log Analytics, vous pouvez :

* Obtenir des informations sur vos travaux Automation
* Déclencher un e-mail ou une alerte basé(e) sur le statut de votre travail de runbook (par exemple, échec ou état suspendu)
* Écrire des requêtes avancées sur vos flux de travail
* Mettre en corrélation des travaux sur différents comptes Automation
* Visualiser l’historique de vos travaux dans le temps     

## <a name="prerequisites-and-deployment-considerations"></a>Conditions préalables et considérations relatives au déploiement
toostart envoyer votre automatisation consigne tooLog Analytique, vous devez :

1. Hello novembre 2016 ou une version plus récente de [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) (v2.3.0).
2. Un espace de travail Log Analytics. Pour plus d’informations, consultez l’article [Prise en main de Log Analytics](../log-analytics/log-analytics-get-started.md). 
3. Hello ResourceId pour votre compte Azure Automation

toofind hello ResourceId pour votre compte Azure Automation et l’espace de travail Analytique de journal, exécutez hello suivant PowerShell :

```powershell
# Find hello ResourceId for hello Automation Account
Find-AzureRmResource -ResourceType "Microsoft.Automation/automationAccounts"

# Find hello ResourceId for hello Log Analytics workspace
Find-AzureRmResource -ResourceType "Microsoft.OperationalInsights/workspaces"
```

Si vous possédez plusieurs comptes Automation ou espaces de travail, dans la sortie de hello de hello précédant les commandes, recherche hello *nom* vous devez tooconfigure et copiez la valeur hello pour *ResourceId*.

Si vous avez besoin de toofind hello *nom* de votre compte Automation, Bonjour portail Azure Sélectionnez votre compte Automation à partir de hello **compte Automation** panneau et sélectionnez **tous les paramètres**.  À partir de hello **tous les paramètres** panneau, sous **les paramètres de compte** sélectionnez **propriétés**.  Bonjour **propriétés** panneau, vous pouvez noter ces valeurs.<br> ![Propriétés du compte Automation](media/automation-manage-send-joblogs-log-analytics/automation-account-properties.png).

## <a name="set-up-integration-with-log-analytics"></a>Configurer l’intégration avec Log Analytics
1. Sur votre ordinateur, démarrez **Windows PowerShell** de hello **Démarrer** écran.  
2. Copiez et collez hello suivant PowerShell, puis modifier la valeur hello pour hello `$workspaceId` et `$automationAccountId`.  Pourquoi `-Environment` paramètre, les valeurs valides sont *cloud Azure* ou *AzureUSGovernment* en fonction de l’environnement en nuage hello vous travaillez dans.     

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check toosee which cloud environment toosign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment} 
   }

# if you have one Log Analytics workspace you can use hello following command tooget hello resource id of hello workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $automationAccountId -WorkspaceId $workspaceId -Enabled $true

```

Après avoir exécuté ce script, les enregistrements s’affichent dans Log Analytics dans les 10 minutes suivant l’écriture des nouveaux JobLogs ou JobStreams.

journaux de hello toosee, exécutez hello suivant la requête de recherche de journal Analytique de journal :`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`

### <a name="verify-configuration"></a>Vérifier la configuration
espace de travail Analytique de journal tooyour les journaux de tooconfirm l’envoi de votre compte Automation, vérifiez que les diagnostics sont correctement définies sur le compte d’automatisation de hello à l’aide de hello suivant PowerShell :

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check toosee which cloud environment toosign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment} 
   }
# if you have one Log Analytics workspace you can use hello following command tooget hello resource id of hello workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO" 

Get-AzureRmDiagnosticSetting -ResourceId $automationAccountId
```

Dans la sortie de hello Vérifiez que :
+ Sous *journaux*, hello valeur pour *activé* est *True*
+ Hello valeur *Id_espace_de_travail* a la valeur toohello ResourceId de votre espace de travail Analytique des journaux


## <a name="log-analytics-records"></a>Enregistrements Log Analytics
Le diagnostic d’Azure Automation crée deux types d’enregistrements dans Log Analytics, balisés par **Type=AzureDiagnostics**.

### <a name="job-logs"></a>Journaux de travail
| Propriété | Description |
| --- | --- |
| TimeGenerated |Date et heure à l’exécution de tâche du runbook hello. |
| RunbookName_s |nom de Hello de hello runbook. |
| Caller_s |Qui a lancé une opération hello.  Les valeurs possibles sont une adresse de messagerie ou un système pour les travaux planifiés. |
| Tenant_g | GUID qui identifie le client hello pour hello appelant. |
| JobId_g |GUID qui est hello Id de tâche du runbook hello. |
| ResultType |état de Hello de tâche du runbook hello.  Les valeurs possibles sont les suivantes :<br>Démarré<br>Arrêté<br>Interrompu<br>Échec<br>- Terminé |
| Catégorie | Classification de type hello de données.  Pour l’automatisation, la valeur de hello est JobLogs. |
| Nom d'opération | Spécifie le type hello d’opération exécutée dans Azure.  Pour l’automatisation, valeur de hello est le travail. |
| Ressource | Nom du compte Automation de hello |
| SourceSystem | Comment Analytique de journal collecté des données de hello. Toujours *Azure* pour les diagnostics Azure. |
| resultDescription |Décrit l’état de résultat du travail de runbook hello.  Les valeurs possibles sont les suivantes :<br>- Job is started<br>- Job Failed<br>- Job Completed |
| CorrelationId |GUID qui est hello Id de corrélation de tâche du runbook hello. |
| ResourceId |Spécifie les id de ressource Azure Automation compte hello de hello runbook. |
| SubscriptionId | Bonjour abonnement Azure Id (GUID) pour hello compte Automation. |
| ResourceGroup | Nom du groupe de ressources hello pour hello compte Automation. |
| ResourceProvider | MICROSOFT.AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |


### <a name="job-streams"></a>Flux de travail
| Propriété | Description |
| --- | --- |
| TimeGenerated |Date et heure à l’exécution de tâche du runbook hello. |
| RunbookName_s |nom de Hello de hello runbook. |
| Caller_s |Qui a lancé une opération hello.  Les valeurs possibles sont une adresse de messagerie ou un système pour les travaux planifiés. |
| StreamType_s |type de Hello du flux de travail. Les valeurs possibles sont les suivantes :<br>progress<br>Sortie<br>Avertissement<br>error<br>DEBUG<br>- Verbose |
| Tenant_g | GUID qui identifie le client hello pour hello appelant. |
| JobId_g |GUID qui est hello Id de tâche du runbook hello. |
| ResultType |état de Hello de tâche du runbook hello.  Les valeurs possibles sont les suivantes :<br>- In Progress |
| Catégorie | Classification de type hello de données.  Pour l’automatisation, la valeur de hello est JobStreams. |
| Nom d'opération | Spécifie le type hello d’opération exécutée dans Azure.  Pour l’automatisation, valeur de hello est le travail. |
| Ressource | Nom du compte Automation de hello |
| SourceSystem | Comment Analytique de journal collecté des données de hello. Toujours *Azure* pour les diagnostics Azure. |
| resultDescription |Inclut le flux de sortie hello hello runbook. |
| CorrelationId |GUID qui est hello Id de corrélation de tâche du runbook hello. |
| ResourceId |Spécifie les id de ressource Azure Automation compte hello de hello runbook. |
| SubscriptionId | Bonjour abonnement Azure Id (GUID) pour hello compte Automation. |
| ResourceGroup | Nom du groupe de ressources hello pour hello compte Automation. |
| ResourceProvider | MICROSOFT.AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |

## <a name="viewing-automation-logs-in-log-analytics"></a>Affichage d’Automation Logs dans Log Analytics
Maintenant que vous avez démarré l’envoi de votre tooLog journaux du travail Automation Analytique, vous allez voir ce que vous pouvez faire avec ces journaux à l’intérieur d’Analytique de journal.

journaux de hello toosee, exécutez hello suivant la requête :`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`

### <a name="send-an-email-when-a-runbook-job-fails-or-suspends"></a>Envoyer un e-mail en cas d’échec ou de suspension d’un travail de runbook
Un de nos clients supérieure demande concerne hello capacité toosend un message électronique ou un texte lorsqu’une erreur survient avec une tâche de runbook.   

la règle toocreate une alerte, vous commencez par créer une recherche de journal pour les runbook hello travaux qui doit appeler l’alerte de hello.  Cliquez sur hello **alerte** bouton toocreate et configurer une règle d’alerte hello.

1. Dans la page de vue d’ensemble Analytique de journal hello, cliquez sur **recherche de journal**.
2. Créer une requête de recherche de journal pour l’alerte en tapant hello suivant recherche dans le champ de requête hello : `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended)` vous pouvez également regrouper par hello RunbookName à l’aide de :`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended) | measure Count() by RunbookName_s`   

   Si vous avez défini des journaux à partir de plusieurs Automation compte ou abonnement tooyour espace de travail, vous pouvez regrouper vos alertes par abonnement et compte Automation.  Nom du compte Automation peut être dérivé d’un champ de ressource hello dans la recherche de hello de JobLogs.  
3. tooopen hello **ajouter une règle d’alerte** , cliquez sur **alerte** en hello haut hello. Pour plus d’informations sur l’alerte de hello tooconfigure hello options, consultez [alertes dans le journal Analytique](../log-analytics/log-analytics-alerts.md#alert-rules).

### <a name="find-all-jobs-that-have-completed-with-errors"></a>Rechercher tous les travaux qui ont rencontré des erreurs
Tooalerting sur les échecs, vous pouvez également trouver lorsqu’une tâche du runbook a une erreur sans fin d’exécution. Dans ces cas PowerShell génère un flux d’erreur, mais les erreurs sans fin d’exécution de hello ne pas entraîner votre toosuspend de travail ou d’échouer.    

1. Dans votre espace de travail Log Analytics, cliquez sur **Recherche de journal**.
2. Dans le champ de requête hello, tapez `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams StreamType_s=Error | measure count() by JobId_g` puis cliquez sur **recherche**.

### <a name="view-job-streams-for-a-job"></a>Afficher les flux de travail pour un travail
Lorsque vous déboguez un travail, vous pouvez également toolook en flux de travail hello.  Hello requête suivante affiche tous les flux hello pour un seul travail avec GUID 2ebd22ea-e05e-4eb9 - 9d 76-d73cbd4356e0 :   

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams JobId_g="2ebd22ea-e05e-4eb9-9d76-d73cbd4356e0" | sort TimeGenerated | select ResultDescription`

### <a name="view-historical-job-status"></a>Afficher l’état de travail historique
Enfin, vous souhaiterez peut-être toovisualize votre historique des travaux au fil du temps.  Vous pouvez utiliser cette toosearch de requête pour état hello des travaux au fil du temps.

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs NOT(ResultType="started") | measure Count() by ResultType interval 1hour`  
<br> ![Graphique d’état de travail historique OMS](media/automation-manage-send-joblogs-log-analytics/historical-job-status-chart.png)<br>

## <a name="summary"></a>Résumé
En envoyant votre Automation travail état et les flux de données tooLog Analytique, vous pouvez obtenir plus de détails sur état hello de vos tâches Automation par :
+ La configuration des alertes toonotify vous lorsqu’il existe un problème
+ À l’aide des vues personnalisées et toovisualize de requêtes de recherche vos résultats de runbook, runbook état du travail et d’autres liées indicateurs clés ou les métriques.  

Analytique de journal fournit des tâches d’automatisation tooyour une plus grande visibilité opérationnelle et peut aider aux incidents adresse plus rapides.  

## <a name="next-steps"></a>Étapes suivantes
* toolearn en savoir plus sur la façon dont des journaux d’Analytique de journal, de travail de tooconstruct les requêtes de recherche différente et révision hello Automation voir [connectez-vous recherche Analytique de journal](../log-analytics/log-analytics-log-searches.md)
* toounderstand comment les messages de sortie et d’erreur toocreate et récupérer à partir de procédures opérationnelles, consultez [Runbook de sortie et des messages](automation-runbook-output-and-messages.md)
* toolearn plus d’informations sur l’exécution du runbook, comment les tâches de runbook toomonitor et d’autres détails techniques, consultez [suivre un travail de runbook](automation-runbook-execution.md)
* toolearn en savoir plus sur l’Analytique des journaux OMS et les sources de collection de données, consultez [les données de stockage Azure de collecte dans la vue d’ensemble Analytique de journal](../log-analytics/log-analytics-azure-storage.md)
