---
title: "aaaForward tooOMS de données reporting Azure Automation DSC Analytique de journal | Documents Microsoft"
description: "Cet article explique comment toosend souhaité reporting données tooMicrosoft Operations Management Suite journal Analytique toodeliver un éclairage supplémentaire et la gestion de Configuration (DSC) de l’état."
services: automation
documentationcenter: 
author: eslesar
manager: carmonm
editor: tysonn
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: eslesar
ms.openlocfilehash: 21f78d5549d53ba3d7e237f55d9086f380cf3351
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="forward-azure-automation-dsc-reporting-data-toooms-log-analytics"></a>Transférer des données tooOMS Analytique de journal de création de rapports Azure Automation DSC

Automation peut envoyer DSC nœud État tooyour Analytique de journal de Microsoft Operations Management Suite (OMS) espace de travail données.  
État de conformité n’est visible dans hello portail Azure, ou avec PowerShell, pour les nœuds et des ressources DSC individuelles dans les configurations de nœuds. Avec Log Analytics, vous pouvez :

* Obtenir des informations de conformité pour les nœuds gérés et les ressources individuelles
* Déclencher un e-mail ou une alerte en fonction de l’état de conformité
* Écrire des requêtes avancées dans vos nœuds gérés
* Mettre en corrélation l’état de conformité dans les comptes Automation
* Visualiser votre historique de conformité associé aux nœuds au fil du temps

## <a name="prerequisites"></a>Composants requis

toostart envoyer votre Automation DSC signale tooLog Analytique, vous devez :

* Hello novembre 2016 ou une version plus récente de [Azure PowerShell](/powershell/azure/overview) (v2.3.0).
* Un compte Azure Automation. Pour plus d’informations, consultez la page [Prise en main d’Azure Automation](automation-offering-get-started.md).
* Un espace de travail Log Analytics avec une offre de service **Automation & Control**. Pour plus d’informations, consultez l’article [Prise en main de Log Analytics](../log-analytics/log-analytics-get-started.md).
* Au moins un nœud Azure Automation DSC. Pour plus d’informations, consultez [Gestion de machines avec Azure Automation DSC](automation-dsc-onboarding.md). 

## <a name="set-up-integration-with-log-analytics"></a>Configurer l’intégration avec Log Analytics

toobegin l’importation de données à partir d’Azure Automation DSC dans le journal Analytique, hello complète comme suit :

1. Ouvrez une session dans tooyour compte Azure dans PowerShell. Consultez [Log in with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/authenticate-azureps?view=azurermps-4.0.0) (Se connecter avec Azure PowerShell).
1. Obtenir hello _ResourceId_ de votre compte automation en exécutant hello suivant de commande PowerShell : (si vous avez plusieurs comptes automation, choisissez hello _ResourceID_ compte hello tooconfigure).

  ```powershell
  # Find hello ResourceId for hello Automation Account
  Find-AzureRmResource -ResourceType "Microsoft.Automation/automationAccounts"
  ```
1. Obtenir hello _ResourceId_ de votre espace de travail Analytique de journal en exécutant hello suivant de commande PowerShell : (si vous avez plus d’un espace de travail, choisissez hello _ResourceID_ pour hello espace de travail tooconfigure).

  ```powershell
  # Find hello ResourceId for hello Log Analytics workspace
  Find-AzureRmResource -ResourceType "Microsoft.OperationalInsights/workspaces"
  ```
1. Exécution hello suivant de commande PowerShell, en remplaçant `<AutomationResourceId>` et `<WorkspaceResourceId>` avec hello _ResourceId_ valeurs à partir de chacune des étapes précédentes de hello :

  ```powershell
  Set-AzureRmDiagnosticSetting -ResourceId <AutomationResourceId> -WorkspaceId <WorkspaceResourceId> -Enabled $true -Categories "DscNodeStatus"
  ```

Si vous souhaitez toostop l’importation de données à partir d’Azure Automation DSC dans Analytique de journal, exécutez hello suivant de commande PowerShell.

```powershell
Set-AzureRmDiagnosticSetting -ResourceId <AutomationResourceId> -WorkspaceId <WorkspaceResourceId> -Enabled $false -Categories "DscNodeStatus"
```

## <a name="view-hello-dsc-logs"></a>Afficher les journaux hello DSC

Après avoir configuré l’intégration avec Analytique de journal pour vos données Automation DSC, un **recherche de journal** bouton s’affiche dans hello **nœuds DSC** Panneau de votre compte automation. Cliquez sur hello **recherche de journal** bouton tooview des journaux de hello pour les données du nœud DSC.

![Bouton Recherche dans les journaux](media/automation-dsc-diagnostics/log-search-button.png)

Hello **recherche de journal** panneau s’ouvre et vous voyez un **DscNodeStatusData** opération pour chaque nœud DSC et un **DscResourceStatusData** opération pour chaque [DSC ressource](https://msdn.microsoft.com/powershell/dsc/resources) appelé dans hello nœud configuration appliquée toothat nœud.

Hello **DscResourceStatusData** opération contient des informations d’erreur pour toutes les ressources DSC qui a échoué.

Cliquez sur chaque opération dans les données de salutation liste toosee hello pour cette opération.

Vous pouvez également afficher les journaux hello par [recherche dans le journal Analytique. Consultez [Recherche de données à l’aide de recherches de journal](../log-analytics/log-analytics-log-searches.md).
Tapez ce qui suit hello interroger toofind votre DSC journaux :`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category = "DscNodeStatus"`

Vous pouvez également limiter les requêtes hello par nom de l’opération hello. Par exemple : « Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category = "DscNodeStatus" OperationName = "DscNodeStatusData" »

### <a name="send-an-email-when-a-dsc-compliance-check-fails"></a>Envoyer un e-mail si une vérification de la conformité DSC échoue

Un de nos principales demandes des clients est pour hello capacité toosend un message électronique ou un texte lorsqu’une erreur survient avec une configuration DSC.   

toocreate une alerte de la règle, commencez par créer une recherche de journal pour les enregistrements de rapport DSC hello qui doit appeler l’alerte de hello.  Cliquez sur hello **alerte** bouton toocreate et configurer une règle d’alerte hello.

1. Dans la page de vue d’ensemble Analytique de journal hello, cliquez sur **recherche de journal**.
1. Créer une requête de recherche de journal pour l’alerte en tapant hello suivant recherche dans le champ de requête hello :`Type=AzureDiagnostics Category=DscNodeStatus NodeName_s=DSCTEST1 OperationName=DscNodeStatusData ResultType=Failed`

  Si vous avez défini des journaux à partir de plusieurs Automation compte ou abonnement tooyour espace de travail, vous pouvez regrouper vos alertes par abonnement et compte Automation.  
  Nom du compte Automation peut être dérivé d’un champ de ressource hello dans la recherche de hello de DscNodeStatusData.  
1. tooopen hello **ajouter une règle d’alerte** , cliquez sur **alerte** en hello haut hello. Pour plus d’informations sur l’alerte de hello tooconfigure hello options, consultez [alertes dans le journal Analytique](../log-analytics/log-analytics-alerts.md#alert-rules).

### <a name="find-failed-dsc-resources-across-all-nodes"></a>Rechercher les ressources DSC ayant échoué dans tous les nœuds

L’un des avantages de l’utilisation de Log Analytics est que vous pouvez rechercher les vérifications ayant échoué dans les nœuds.
toofind toutes les instances de ressources DSC qui ont échoué.

1. Dans la page de vue d’ensemble Analytique de journal hello, cliquez sur **recherche de journal**.
1. Créer une requête de recherche de journal pour l’alerte en tapant hello suivant recherche dans le champ de requête hello :`Type=AzureDiagnostics Category=DscNodeStatus OperationName=DscResourceStatusData ResultType=Failed`

### <a name="view-historical-dsc-node-status"></a>Afficher l’état de nœud DSC historique

Enfin, vous souhaiterez peut-être toovisualize votre historique de l’état du nœud DSC au fil du temps.  
Vous pouvez utiliser cette toosearch de requête pour l’état hello de votre état de nœud DSC au fil du temps.

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=DscNodeStatus NOT(ResultType="started") | measure Count() by ResultType interval 1hour`  

Cette action affiche un graphique de l’état du nœud hello au fil du temps.

## <a name="log-analytics-records"></a>Enregistrements Log Analytics

La fonction de diagnostic d’Azure Automation crée deux catégories d’enregistrements dans Log Analytics.

### <a name="dscnodestatusdata"></a>DscNodeStatusData

| Propriété | Description |
| --- | --- |
| TimeGenerated |Date et heure lorsque la vérification de la conformité hello a exécuté. |
| Nom d'opération |DscNodeStatusData |
| ResultType |Si le nœud de hello est conforme. |
| NodeName_s |nom de Hello du nœud géré de hello. |
| NodeComplianceStatus_s |Si le nœud de hello est conforme. |
| DscReportStatus |Indique si la vérification de la conformité hello exécuté avec succès. |
| ConfigurationMode | Comment la configuration de hello est appliqué toohello nœud. Les valeurs possibles sont __« ApplyOnly »__,__« ApplyandMonitor »__ et __« ApplyandAutoCorrect »__. <ul><li>__ApplyOnly__: DSC d’appliquer la configuration de hello et ne fait rien de plus, sauf si une nouvelle configuration est transmise toohello ou cibles quand une nouvelle configuration est extraite d’un serveur. Après l’application initiale d’une nouvelle configuration, DSC ne vérifie pas l’écart par rapport à un état configuré précédemment. DSC tente de configuration de hello tooapply jusqu'à ce qu’il réussisse avant __ApplyOnly__ en vigueur. </li><li> __ApplyAndMonitor__: il s’agit par défaut hello. Hello LCM s’applique à chaque nouvelle configuration. Après l’application initiale d’une nouvelle configuration, si le nœud cible de hello diffère de l’état de hello souhaité, DSC signale écart hello dans les journaux. DSC tente de configuration de hello tooapply jusqu'à ce qu’il réussisse avant __ApplyAndMonitor__ en vigueur.</li><li>__ApplyAndAutoCorrect__ : DSC applique toutes les nouvelles configurations. Après l’application initiale d’une nouvelle configuration, si le nœud cible de hello diffère de l’état de hello souhaité, DSC signale l’écart hello dans les journaux et puis réapplique configuration actuelle de hello.</li></ul> |
| HostName_s | nom de Hello du nœud géré de hello. |
| IPAddress | adresse IPv4 Hello hello géré de nœud. |
| Catégorie | DscNodeStatus |
| Ressource | nom Hello Hello compte Azure Automation. |
| Tenant_g | GUID qui identifie le client hello pour hello appelant. |
| NodeId_g |GUID qui identifie le nœud géré de hello. |
| DscReportId_g |GUID qui identifie le rapport de hello. |
| LastSeenTime_t |Date et heure lorsque les rapports hello a été visualisée. |
| ReportStartTime_t |Date et heure de début de l’état de hello. |
| ReportEndTime_t |Date et heure de fin de l’état de hello. |
| NumberOfResources_d |nombre de Hello de ressources DSC appelé dans le nœud de toohello hello configuration est appliquée. |
| SourceSystem | Comment Analytique de journal collecté des données de hello. Toujours *Azure* pour les diagnostics Azure. |
| ResourceId |Spécifie le compte Azure Automation de hello. |
| resultDescription | description de Hello pour cette opération. |
| SubscriptionId | Bonjour abonnement Azure Id (GUID) pour hello compte Automation. |
| ResourceGroup | Nom du groupe de ressources hello pour hello compte Automation. |
| ResourceProvider | MICROSOFT.AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |
| CorrelationId |GUID qui est hello Id de corrélation du rapport de conformité hello. |

### <a name="dscresourcestatusdata"></a>DscResourceStatusData

| Propriété | Description |
| --- | --- |
| TimeGenerated |Date et heure lorsque la vérification de la conformité hello a exécuté. |
| Nom d'opération |DscResourceStatusData|
| ResultType |Si la ressource de hello est conforme. |
| NodeName_s |nom de Hello du nœud géré de hello. |
| Catégorie | DscNodeStatus |
| Ressource | nom Hello Hello compte Azure Automation. |
| Tenant_g | GUID qui identifie le client hello pour hello appelant. |
| NodeId_g |GUID qui identifie le nœud géré de hello. |
| DscReportId_g |GUID qui identifie le rapport de hello. |
| DscResourceId_s |nom Hello de l’instance de la ressource hello DSC. |
| DscResourceName_s |nom de Hello de ressource de hello DSC. |
| DscResourceStatus_s |Si hello ressource DSC est conforme. |
| DscModuleName_s |nom Hello du module PowerShell hello qui contient la ressource de DSC hello. |
| DscModuleVersion_s |version Hello du module PowerShell hello qui contient la ressource de DSC hello. |
| DscConfigurationName_s |nom de Hello de configuration de hello appliqué toohello nœud. |
| ErrorCode_s | code d’erreur Hello en cas d’échec de la ressource de hello. |
| ErrorMessage_s |message d’erreur Hello en cas d’échec de la ressource de hello. |
| DscResourceDuration_d |Hello durée, en secondes, pendant laquelle hello ressource DSC s’est exécutée. |
| SourceSystem | Comment Analytique de journal collecté des données de hello. Toujours *Azure* pour les diagnostics Azure. |
| ResourceId |Spécifie le compte Azure Automation de hello. |
| resultDescription | description de Hello pour cette opération. |
| SubscriptionId | Bonjour abonnement Azure Id (GUID) pour hello compte Automation. |
| ResourceGroup | Nom du groupe de ressources hello pour hello compte Automation. |
| ResourceProvider | MICROSOFT.AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |
| CorrelationId |GUID qui est hello Id de corrélation du rapport de conformité hello. |

## <a name="summary"></a>Résumé

En envoyant votre tooLog de données Analytique Automation DSC, vous pouvez obtenir plus de détails sur état hello vos nœuds Automation DSC par :

* La configuration des alertes toonotify vous lorsqu’il existe un problème
* À l’aide des vues personnalisées et toovisualize de requêtes de recherche vos résultats de runbook, runbook état du travail et d’autres liées indicateurs clés ou les métriques.  

Analytique de journal fournit des données Automation DSC tooyour visibilité opérationnelle supérieure et peut aider aux incidents adresse plus rapidement.  

## <a name="next-steps"></a>Étapes suivantes

* toolearn plus d’informations sur la façon dont les requêtes de recherche différente tooconstruct et révision hello Automation DSC consigne avec Analytique de journal, consultez [connectez-vous recherche Analytique de journal](../log-analytics/log-analytics-log-searches.md)
* toolearn savoir plus sur l’utilisation de Azure Automation DSC, consultez [prise en main d’Azure Automation DSC](automation-dsc-getting-started.md)
* toolearn en savoir plus sur l’Analytique des journaux OMS et les sources de collection de données, consultez [les données de stockage Azure de collecte dans la vue d’ensemble Analytique de journal](../log-analytics/log-analytics-azure-storage.md)

