---
title: "aaaMigrate Azure Alerts sur tooActivity d’événements de gestion des alertes de journal | Documents Microsoft"
description: "Les alertes pour les événements de gestion seront supprimées le 1er octobre. Préparez-vous en migrant les alertes existantes."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: johnkem
ms.openlocfilehash: e00bc4f0bad4e8f97443310770c333d250e343ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-alerts-on-management-events-tooactivity-log-alerts"></a>Migrer des alertes Azure sur la gestion des événements tooActivity journal des alertes


> [!WARNING]
> Les alertes pour les événements de gestion seront désactivées à partir du 1er octobre. Utilisez les instructions hello toounderstand si ces alertes et les migrer cas dans ce.
>
> 

## <a name="what-is-changing"></a>Changements

Moniteur de Azure (anciennement Azure Insights) proposé une capacité toocreate une alerte déclenchée sur les événements de gestion et généré des notifications tooa webhook URL ou les adresses e-mail. Vous avez peut-être créé une de ces alertes d’une des manières suivantes :
* Dans le portail Azure pour certains types de ressources de hello, sous Analyse -> alertes -> Ajouter une alerte, où « Alerte sur » est définie trop « Événements »
* Applet de commande de Add-AzureRmLogAlertRule PowerShell hello en cours d’exécution
* En utilisant directement [hello alerte API REST](http://docs.microsoft.com/rest/api/monitor/alertrules) avec odata.type = « ManagementEventRuleCondition » et dataSource.odata.type = « RuleManagementEventDataSource »
 
Hello script PowerShell suivant retourne une liste de toutes les alertes sur les événements de gestion que vous avez dans votre abonnement, ainsi que les conditions de hello définies pour chaque alerte.

```powershell
Login-AzureRmAccount
$alerts = $null
foreach ($rg in Get-AzureRmResourceGroup ) {
  $alerts += Get-AzureRmAlertRule -ResourceGroup $rg.ResourceGroupName
}
foreach ($alert in $alerts) {
  if($alert.Properties.Condition.DataSource.GetType().Name.Equals("RuleManagementEventDataSource")) {
    "Alert Name: " + $alert.Name
    "Alert Resource ID: " + $alert.Id
    "Alert conditions:"
    $alert.Properties.Condition.DataSource
    "---------------------------------"
  }
} 
```

Si vous n’avez aucune alerte sur les événements de gestion, hello applet de commande PowerShell ci-dessus aura pour résultat une série de messages d’avertissement similaire à celle-ci :

`WARNING: hello output of this cmdlet will be flattened, i.e. elimination of hello properties field, in a future release tooimprove hello user experience.`

Ces messages d’avertissement peuvent être ignorés. Si vous avez des alertes sur les événements de gestion, la sortie de hello de cette applet de commande PowerShell ressemble à ceci :

```
Alert Name: webhookEvent1
Alert Resource ID: /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/microsoft.insights/alertrules/webhookEvent1
Alert conditions:

EventName            : 
EventSource          : 
Level                : 
OperationName        : microsoft.web/sites/start/action
ResourceGroupName    : 
ResourceProviderName : 
Status               : succeeded
SubStatus            : 
Claims               : Microsoft.Azure.Management.Monitor.Management.Models.RuleManagementEventClaimsDataSource
ResourceUri          : /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/Microsoft.Web/sites/samplealertapp

---------------------------------
Alert Name: someclilogalert
Alert Resource ID: /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/microsoft.insights/alertrules/someclilogalert
Alert conditions:

EventName            : 
EventSource          : 
Level                : 
OperationName        : Start
ResourceGroupName    : 
ResourceProviderName : 
Status               : 
SubStatus            : 
Claims               : Microsoft.Azure.Management.Monitor.Management.Models.RuleManagementEventClaimsDataSource
ResourceUri          : /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/Microsoft.Compute/virtualMachines/Seaofclouds

---------------------------------
```

Chaque alerte est séparé par une ligne en pointillés et les détails incluent l’ID de ressource hello hello et des alertes règle spécifique de hello en cours d’analyse.

Cette fonctionnalité a été migrée trop[Azure analyse vous alerte journal activité](monitoring-activity-log-alerts.md). Ces nouvelles alertes vous tooset une condition sur les événements du journal d’activité et recevoir une notification lorsqu’un nouvel événement correspond à la condition de hello. Elles apportent également plusieurs améliorations au niveau des alertes sur des événements de gestion :
* Vous pouvez réutiliser votre groupe de destinataires de notification (« actions ») dans le nombre d’alertes à l’aide de [groupes d’actions](monitoring-action-groups.md), réduction de la complexité hello de modification qui doit recevoir une alerte.
* Grâce aux groupes d’actions, vous pouvez recevoir une notification directement par SMS sur votre téléphone.
* Vous pouvez [créer des alertes de journal d’activité à l’aide de modèles Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md).
* Vous pouvez créer des conditions avec toomeet plu de souplesse et la complexité de vos besoins spécifiques.
* Les notifications sont remises plus rapidement.
 
## <a name="how-toomigrate"></a>Comment toomigrate
 
toocreate une nouvelle alerte journal d’activité, vous pouvez :
* Suivez [notre guide sur comment toocreate une alerte dans hello portail Azure](monitoring-activity-log-alerts.md)
* Découvrez comment trop[créer une alerte à l’aide d’un modèle de gestionnaire de ressources](monitoring-create-activity-log-alerts-with-resource-manager-template.md)
 
Alertes pour les événements de gestion que vous avez créé précédemment ne sera pas automatiquement migré tooActivity journal des alertes. Vous devez hello toouse précédant les alertes de hello PowerShell script toolist sur les événements de gestion que vous avez actuellement configurée et les recréez manuellement en tant qu’alertes de journal d’activité. Ces opérations doivent être effectuées avant le 1er octobre. Après cette date, les alertes sur des événements de gestion n’apparaîtront plus dans votre abonnement Azure. Cette modification n’affecte pas les autres types d’alertes Azure comme les alertes de métrique Azure Monitor, les alertes Application Insights et les alertes Log Analytics. Si vous avez des questions, publier dans des commentaires hello ci-dessous.


## <a name="next-steps"></a>Étapes suivantes

* En savoir plus sur les [journaux d’activité](monitoring-overview-activity-logs.md)
* Configurer les [alertes de journal d’activité par le biais du portail Azure](monitoring-activity-log-alerts.md)
* Configurer les [alertes de journal d’activité au moyen de Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)
* Hello de révision [webhook alerte schéma des journaux d’activité](monitoring-activity-log-alerts-webhook.md)
* Apprenez-en plus sur les [notifications de service](monitoring-service-notifications.md)
* En savoir plus sur les [groupes d’actions](monitoring-action-groups.md)
