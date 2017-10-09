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
# <a name="migrate-azure-alerts-on-management-events-tooactivity-log-alerts"></a><span data-ttu-id="57f50-104">Migrer des alertes Azure sur la gestion des événements tooActivity journal des alertes</span><span class="sxs-lookup"><span data-stu-id="57f50-104">Migrate Azure alerts on management events tooActivity Log alerts</span></span>


> [!WARNING]
> <span data-ttu-id="57f50-105">Les alertes pour les événements de gestion seront désactivées à partir du 1er octobre.</span><span class="sxs-lookup"><span data-stu-id="57f50-105">Alerts on management events will be turned off on or after October 1.</span></span> <span data-ttu-id="57f50-106">Utilisez les instructions hello toounderstand si ces alertes et les migrer cas dans ce.</span><span class="sxs-lookup"><span data-stu-id="57f50-106">Use hello directions below toounderstand if you have these alerts and migrate them if so.</span></span>
>
> 

## <a name="what-is-changing"></a><span data-ttu-id="57f50-107">Changements</span><span class="sxs-lookup"><span data-stu-id="57f50-107">What is changing</span></span>

<span data-ttu-id="57f50-108">Moniteur de Azure (anciennement Azure Insights) proposé une capacité toocreate une alerte déclenchée sur les événements de gestion et généré des notifications tooa webhook URL ou les adresses e-mail.</span><span class="sxs-lookup"><span data-stu-id="57f50-108">Azure Monitor (formerly Azure Insights) offered a capability toocreate an alert that triggered off of management events and generated notifications tooa webhook URL or email addresses.</span></span> <span data-ttu-id="57f50-109">Vous avez peut-être créé une de ces alertes d’une des manières suivantes :</span><span class="sxs-lookup"><span data-stu-id="57f50-109">You may have created one of these alerts any of these ways:</span></span>
* <span data-ttu-id="57f50-110">Dans le portail Azure pour certains types de ressources de hello, sous Analyse -> alertes -> Ajouter une alerte, où « Alerte sur » est définie trop « Événements »</span><span class="sxs-lookup"><span data-stu-id="57f50-110">In hello Azure portal for certain resource types, under Monitoring -> Alerts -> Add Alert, where “Alert on” is set too“Events”</span></span>
* <span data-ttu-id="57f50-111">Applet de commande de Add-AzureRmLogAlertRule PowerShell hello en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="57f50-111">By running hello Add-AzureRmLogAlertRule PowerShell cmdlet</span></span>
* <span data-ttu-id="57f50-112">En utilisant directement [hello alerte API REST](http://docs.microsoft.com/rest/api/monitor/alertrules) avec odata.type = « ManagementEventRuleCondition » et dataSource.odata.type = « RuleManagementEventDataSource »</span><span class="sxs-lookup"><span data-stu-id="57f50-112">By directly using [hello alert REST API](http://docs.microsoft.com/rest/api/monitor/alertrules) with odata.type = “ManagementEventRuleCondition” and dataSource.odata.type = “RuleManagementEventDataSource”</span></span>
 
<span data-ttu-id="57f50-113">Hello script PowerShell suivant retourne une liste de toutes les alertes sur les événements de gestion que vous avez dans votre abonnement, ainsi que les conditions de hello définies pour chaque alerte.</span><span class="sxs-lookup"><span data-stu-id="57f50-113">hello following PowerShell script returns a list of all alerts on management events that you have in your subscription, as well as hello conditions set on each alert.</span></span>

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

<span data-ttu-id="57f50-114">Si vous n’avez aucune alerte sur les événements de gestion, hello applet de commande PowerShell ci-dessus aura pour résultat une série de messages d’avertissement similaire à celle-ci :</span><span class="sxs-lookup"><span data-stu-id="57f50-114">If you have no alerts on management events, hello PowerShell cmdlet above will output a series of warning messages like this one:</span></span>

`WARNING: hello output of this cmdlet will be flattened, i.e. elimination of hello properties field, in a future release tooimprove hello user experience.`

<span data-ttu-id="57f50-115">Ces messages d’avertissement peuvent être ignorés.</span><span class="sxs-lookup"><span data-stu-id="57f50-115">These warning messages can be ignored.</span></span> <span data-ttu-id="57f50-116">Si vous avez des alertes sur les événements de gestion, la sortie de hello de cette applet de commande PowerShell ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="57f50-116">If you do have alerts on management events, hello output of this PowerShell cmdlet will look like this:</span></span>

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

<span data-ttu-id="57f50-117">Chaque alerte est séparé par une ligne en pointillés et les détails incluent l’ID de ressource hello hello et des alertes règle spécifique de hello en cours d’analyse.</span><span class="sxs-lookup"><span data-stu-id="57f50-117">Each alert is separated by a dashed line and details include hello resource ID of hello alert and hello specific rule being monitored.</span></span>

<span data-ttu-id="57f50-118">Cette fonctionnalité a été migrée trop[Azure analyse vous alerte journal activité](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="57f50-118">This functionality has been transitioned too[Azure Monitor Activity Log Alerts](monitoring-activity-log-alerts.md).</span></span> <span data-ttu-id="57f50-119">Ces nouvelles alertes vous tooset une condition sur les événements du journal d’activité et recevoir une notification lorsqu’un nouvel événement correspond à la condition de hello.</span><span class="sxs-lookup"><span data-stu-id="57f50-119">These new alerts enable you tooset a condition on Activity Log events and receive a notification when a new event matches hello condition.</span></span> <span data-ttu-id="57f50-120">Elles apportent également plusieurs améliorations au niveau des alertes sur des événements de gestion :</span><span class="sxs-lookup"><span data-stu-id="57f50-120">They also offer several improvements from alerts on management events:</span></span>
* <span data-ttu-id="57f50-121">Vous pouvez réutiliser votre groupe de destinataires de notification (« actions ») dans le nombre d’alertes à l’aide de [groupes d’actions](monitoring-action-groups.md), réduction de la complexité hello de modification qui doit recevoir une alerte.</span><span class="sxs-lookup"><span data-stu-id="57f50-121">You can reuse your group of notification recipients (“actions”) across many alerts using [Action Groups](monitoring-action-groups.md), reducing hello complexity of changing who should receive an alert.</span></span>
* <span data-ttu-id="57f50-122">Grâce aux groupes d’actions, vous pouvez recevoir une notification directement par SMS sur votre téléphone.</span><span class="sxs-lookup"><span data-stu-id="57f50-122">You can receive a notification directly on your phone using SMS with Action Groups.</span></span>
* <span data-ttu-id="57f50-123">Vous pouvez [créer des alertes de journal d’activité à l’aide de modèles Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="57f50-123">You can [create Activity Log Alerts with Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>
* <span data-ttu-id="57f50-124">Vous pouvez créer des conditions avec toomeet plu de souplesse et la complexité de vos besoins spécifiques.</span><span class="sxs-lookup"><span data-stu-id="57f50-124">You can create conditions with greater flexibility and complexity toomeet your specific needs.</span></span>
* <span data-ttu-id="57f50-125">Les notifications sont remises plus rapidement.</span><span class="sxs-lookup"><span data-stu-id="57f50-125">Notifications are delivered more quickly.</span></span>
 
## <a name="how-toomigrate"></a><span data-ttu-id="57f50-126">Comment toomigrate</span><span class="sxs-lookup"><span data-stu-id="57f50-126">How toomigrate</span></span>
 
<span data-ttu-id="57f50-127">toocreate une nouvelle alerte journal d’activité, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="57f50-127">toocreate a new Activity Log Alert, you can either:</span></span>
* <span data-ttu-id="57f50-128">Suivez [notre guide sur comment toocreate une alerte dans hello portail Azure](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="57f50-128">Follow [our guide on how toocreate an alert in hello Azure portal](monitoring-activity-log-alerts.md)</span></span>
* <span data-ttu-id="57f50-129">Découvrez comment trop[créer une alerte à l’aide d’un modèle de gestionnaire de ressources](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="57f50-129">Learn how too[create an alert using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
 
<span data-ttu-id="57f50-130">Alertes pour les événements de gestion que vous avez créé précédemment ne sera pas automatiquement migré tooActivity journal des alertes.</span><span class="sxs-lookup"><span data-stu-id="57f50-130">Alerts on management events that you have previously created will not be automatically migrated tooActivity Log Alerts.</span></span> <span data-ttu-id="57f50-131">Vous devez hello toouse précédant les alertes de hello PowerShell script toolist sur les événements de gestion que vous avez actuellement configurée et les recréez manuellement en tant qu’alertes de journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="57f50-131">You need toouse hello preceding PowerShell script toolist hello alerts on management events that you currently have configured and manually recreate them as Activity Log Alerts.</span></span> <span data-ttu-id="57f50-132">Ces opérations doivent être effectuées avant le 1er octobre. Après cette date, les alertes sur des événements de gestion n’apparaîtront plus dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="57f50-132">This must be done before October 1, after which alerts on management events will no longer be visible in your Azure subscription.</span></span> <span data-ttu-id="57f50-133">Cette modification n’affecte pas les autres types d’alertes Azure comme les alertes de métrique Azure Monitor, les alertes Application Insights et les alertes Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="57f50-133">Other types of Azure alerts, including Azure Monitor metric alerts, Application Insights alerts, and Log Analytics alerts are unaffected by this change.</span></span> <span data-ttu-id="57f50-134">Si vous avez des questions, publier dans des commentaires hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="57f50-134">If you have any questions, post in hello comments below.</span></span>


## <a name="next-steps"></a><span data-ttu-id="57f50-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="57f50-135">Next steps</span></span>

* <span data-ttu-id="57f50-136">En savoir plus sur les [journaux d’activité](monitoring-overview-activity-logs.md)</span><span class="sxs-lookup"><span data-stu-id="57f50-136">Learn more about [Activity Log](monitoring-overview-activity-logs.md)</span></span>
* <span data-ttu-id="57f50-137">Configurer les [alertes de journal d’activité par le biais du portail Azure](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="57f50-137">Configure [Activity Log Alerts via Azure portal](monitoring-activity-log-alerts.md)</span></span>
* <span data-ttu-id="57f50-138">Configurer les [alertes de journal d’activité au moyen de Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="57f50-138">Configure [Activity Log Alerts via Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
* <span data-ttu-id="57f50-139">Hello de révision [webhook alerte schéma des journaux d’activité](monitoring-activity-log-alerts-webhook.md)</span><span class="sxs-lookup"><span data-stu-id="57f50-139">Review hello [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md)</span></span>
* <span data-ttu-id="57f50-140">Apprenez-en plus sur les [notifications de service](monitoring-service-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="57f50-140">Learn more about [Service Notifications](monitoring-service-notifications.md)</span></span>
* <span data-ttu-id="57f50-141">En savoir plus sur les [groupes d’actions](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="57f50-141">Learn more about [Action Groups](monitoring-action-groups.md)</span></span>
