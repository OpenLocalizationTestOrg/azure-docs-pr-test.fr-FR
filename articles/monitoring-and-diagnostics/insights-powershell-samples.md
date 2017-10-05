---
title: "Exemples de démarrage rapide Azure Monitor PowerShell. | Microsoft Docs"
description: "Utilisez PowerShell pour accéder aux fonctionnalités d’Azure Monitor telles que la mise à l’échelle, les alertes, les webhooks et la recherche dans les journaux d’activité."
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c0761814-7148-4ab5-8c27-a2c9fa4cfef5
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 48f064884c2a6d0a55cc58a44169ed03c62de46d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-monitor-powershell-quick-start-samples"></a><span data-ttu-id="8ed23-104">Exemples de démarrage rapide Azure Monitor PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ed23-104">Azure Monitor PowerShell quick start samples</span></span>
<span data-ttu-id="8ed23-105">Cet article vous présente des exemples de commandes PowerShell qui vous aideront à accéder rapidement aux fonctions de surveillance Azure Insights.</span><span class="sxs-lookup"><span data-stu-id="8ed23-105">This article shows you sample PowerShell commands to help you access Azure Monitor features.</span></span> <span data-ttu-id="8ed23-106">Azure Monitor permet une mise à l'échelle automatique des services cloud, des machines virtuelles et des applications web, et d’envoyer des notifications d'alerte ou d’appeler des URL web basées sur des valeurs de données de télémétrie configurées.</span><span class="sxs-lookup"><span data-stu-id="8ed23-106">Azure Monitor allows you to AutoScale Cloud Services, Virtual Machines, and Web Apps and to send alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="8ed23-107">Azure Monitor est le nouveau nom de ce qui était appelé « Azure Insights » jusqu’au 25 septembre 2016.</span><span class="sxs-lookup"><span data-stu-id="8ed23-107">Azure Monitor is the new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="8ed23-108">Toutefois, les espaces de noms et, par conséquent, les commandes suivantes contiennent toujours « insights ».</span><span class="sxs-lookup"><span data-stu-id="8ed23-108">However, the namespaces and thus the following commands still contain the "insights".</span></span>
> 
> 

## <a name="set-up-powershell"></a><span data-ttu-id="8ed23-109">Configurer PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ed23-109">Set up PowerShell</span></span>
<span data-ttu-id="8ed23-110">Si vous ne l’avez déjà fait, configurez PowerShell pour s’exécuter sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8ed23-110">If you haven't already, set up PowerShell to run on your computer.</span></span> <span data-ttu-id="8ed23-111">Pour plus d’informations, consultez l’article [Guide pratique pour installer et configurer PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8ed23-111">For more information, see [How to Install and Configure PowerShell](/powershell/azure/overview).</span></span>

## <a name="examples-in-this-article"></a><span data-ttu-id="8ed23-112">Exemples de cet article</span><span class="sxs-lookup"><span data-stu-id="8ed23-112">Examples in this article</span></span>
<span data-ttu-id="8ed23-113">Les exemples de cet article montrent comment utiliser les applets de commande Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="8ed23-113">The examples in the article illustrate how you can use Azure Monitor cmdlets.</span></span> <span data-ttu-id="8ed23-114">Vous pouvez également consulter la liste complète des applets de commande PowerShell Azure Monitor dans la rubrique [Applets de commande Azure Monitor (Insights)](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span><span class="sxs-lookup"><span data-stu-id="8ed23-114">You can also review the entire list of Azure Monitor PowerShell cmdlets at [Azure Monitor (Insights) Cmdlets](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span></span>

## <a name="sign-in-and-use-subscriptions"></a><span data-ttu-id="8ed23-115">Se connecter et utiliser des abonnements</span><span class="sxs-lookup"><span data-stu-id="8ed23-115">Sign in and use subscriptions</span></span>
<span data-ttu-id="8ed23-116">Tout d’abord, connectez-vous à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="8ed23-116">First, log in to your Azure subscription.</span></span>

```PowerShell
Login-AzureRmAccount
```

<span data-ttu-id="8ed23-117">Vous devez vous identifier.</span><span class="sxs-lookup"><span data-stu-id="8ed23-117">This requires you to sign in.</span></span> <span data-ttu-id="8ed23-118">Vos informations de compte, d’ID de locataire et d’ID d’abonnement par défaut s’affichent alors.</span><span class="sxs-lookup"><span data-stu-id="8ed23-118">Once you do, your Account, TenantID and default Subscription ID are displayed.</span></span> <span data-ttu-id="8ed23-119">Toutes les applets de commande Azure fonctionnent dans le cadre de votre abonnement par défaut.</span><span class="sxs-lookup"><span data-stu-id="8ed23-119">All the Azure cmdlets work in the context of your default subscription.</span></span> <span data-ttu-id="8ed23-120">Pour afficher la liste des abonnements auxquels vous avez accès, utilisez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="8ed23-120">To view the list of subscriptions you have access to, use the following command.</span></span>

```PowerShell
Get-AzureRmSubscription
```

<span data-ttu-id="8ed23-121">Pour remplacer votre contexte de travail par un autre abonnement, utilisez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="8ed23-121">To change your working context to a different subscription, use the following command.</span></span>

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a><span data-ttu-id="8ed23-122">Récupérer le journal d’activité d’un abonnement</span><span class="sxs-lookup"><span data-stu-id="8ed23-122">Retrieve Activity log for a subscription</span></span>
<span data-ttu-id="8ed23-123">Utilisez l’applet de commande `Get-AzureRmLog` .</span><span class="sxs-lookup"><span data-stu-id="8ed23-123">Use the `Get-AzureRmLog` cmdlet.</span></span>  <span data-ttu-id="8ed23-124">Voici quelques exemples courants.</span><span class="sxs-lookup"><span data-stu-id="8ed23-124">The following are some common examples.</span></span>

<span data-ttu-id="8ed23-125">Obtenir les entrées de journal à partir de cette date/heure :</span><span class="sxs-lookup"><span data-stu-id="8ed23-125">Get log entries from this time/date to present:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2016-03-01T10:30
```

<span data-ttu-id="8ed23-126">Obtenir les entrées de journal entre une plage de dates/heures :</span><span class="sxs-lookup"><span data-stu-id="8ed23-126">Get log entries between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="8ed23-127">Obtenir les entrées de journal à partir d'un groupe de ressources spécifique :</span><span class="sxs-lookup"><span data-stu-id="8ed23-127">Get log entries from a specific resource group:</span></span>

```PowerShell
Get-AzureRmLog -ResourceGroup 'myrg1'
```

<span data-ttu-id="8ed23-128">Obtenir les entrées de journal à partir d'un fournisseur de ressources spécifique entre une plage de dates/heures :</span><span class="sxs-lookup"><span data-stu-id="8ed23-128">Get log entries from a specific resource provider between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -ResourceProvider 'Microsoft.Web' -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="8ed23-129">Obtenir toutes les entrées de journal avec un appelant spécifique :</span><span class="sxs-lookup"><span data-stu-id="8ed23-129">Get all log entries with a specific caller:</span></span>

```PowerShell
Get-AzureRmLog -Caller 'myname@company.com'
```

<span data-ttu-id="8ed23-130">La commande suivante récupère les 1000 derniers événements du journal d'activité :</span><span class="sxs-lookup"><span data-stu-id="8ed23-130">The following command retrieves the last 1000 events from the activity log:</span></span>

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

<span data-ttu-id="8ed23-131">`Get-AzureRmLog` prend en charge de nombreux autres paramètres.</span><span class="sxs-lookup"><span data-stu-id="8ed23-131">`Get-AzureRmLog` supports many other parameters.</span></span> <span data-ttu-id="8ed23-132">Pour plus d'informations, consultez `Get-AzureRmLog` .</span><span class="sxs-lookup"><span data-stu-id="8ed23-132">See the `Get-AzureRmLog` reference for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="8ed23-133">`Get-AzureRmLog` fournit uniquement 15 jours d'historique.</span><span class="sxs-lookup"><span data-stu-id="8ed23-133">`Get-AzureRmLog` only provides 15 days of history.</span></span> <span data-ttu-id="8ed23-134">Le paramètre **-MaxEvents** vous permet d'interroger les N derniers événements, au-delà de 15 jours.</span><span class="sxs-lookup"><span data-stu-id="8ed23-134">Using the **-MaxEvents** parameter allows you to query the last N events, beyond 15 days.</span></span> <span data-ttu-id="8ed23-135">Pour accéder aux événements antérieurs à 15 jours, utilisez l'API REST ou le Kit SDK (exemple de code C# à l'aide du SDK).</span><span class="sxs-lookup"><span data-stu-id="8ed23-135">To access events older than 15 days, use the REST API or SDK (C# sample using the SDK).</span></span> <span data-ttu-id="8ed23-136">Si vous n'incluez pas **StartTime**, la valeur par défaut est **EndTime** moins une heure.</span><span class="sxs-lookup"><span data-stu-id="8ed23-136">If you do not include **StartTime**, then the default value is **EndTime** minus one hour.</span></span> <span data-ttu-id="8ed23-137">Si vous n'incluez pas **EndTime**, la valeur par défaut est l'heure actuelle.</span><span class="sxs-lookup"><span data-stu-id="8ed23-137">If you do not include **EndTime**, then the default value is current time.</span></span> <span data-ttu-id="8ed23-138">Toutes les heures sont exprimées en heure UTC.</span><span class="sxs-lookup"><span data-stu-id="8ed23-138">All times are in UTC.</span></span>
> 
> 

## <a name="retrieve-alerts-history"></a><span data-ttu-id="8ed23-139">Récupérer l'historique des alertes</span><span class="sxs-lookup"><span data-stu-id="8ed23-139">Retrieve alerts history</span></span>
<span data-ttu-id="8ed23-140">Pour afficher tous les événements d'alerte, vous pouvez interroger les journaux Azure Resource Manager en utilisant les exemples suivants.</span><span class="sxs-lookup"><span data-stu-id="8ed23-140">To view all alert events, you can query the Azure Resource Manager logs using the following examples.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="8ed23-141">Pour afficher l'historique d'une règle d'alerte spécifique, vous pouvez utiliser l’applet de commande `Get-AzureRmAlertHistory` , en passant l'ID de ressource de la règle d'alerte.</span><span class="sxs-lookup"><span data-stu-id="8ed23-141">To view the history for a specific alert rule, you can use the `Get-AzureRmAlertHistory` cmdlet, passing in the resource ID of the alert rule.</span></span>

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

<span data-ttu-id="8ed23-142">L’applet de commande `Get-AzureRmAlertHistory` prend en charge différents paramètres.</span><span class="sxs-lookup"><span data-stu-id="8ed23-142">The `Get-AzureRmAlertHistory` cmdlet supports various parameters.</span></span> <span data-ttu-id="8ed23-143">Plus d'informations, consultez [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span><span class="sxs-lookup"><span data-stu-id="8ed23-143">More information, see [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span></span>

## <a name="retrieve-information-on-alert-rules"></a><span data-ttu-id="8ed23-144">Récupérer des informations sur les règles d'alerte</span><span class="sxs-lookup"><span data-stu-id="8ed23-144">Retrieve information on alert rules</span></span>
<span data-ttu-id="8ed23-145">Toutes les commandes suivantes s’appliquent à un groupe de ressources nommé « montest ».</span><span class="sxs-lookup"><span data-stu-id="8ed23-145">All of the following commands act on a Resource Group named "montest".</span></span>

<span data-ttu-id="8ed23-146">Afficher toutes les propriétés de la règle d'alerte :</span><span class="sxs-lookup"><span data-stu-id="8ed23-146">View all the properties of the alert rule:</span></span>

```PowerShell
Get-AzureRmAlertRule -Name simpletestCPU -ResourceGroup montest -DetailedOutput
```

<span data-ttu-id="8ed23-147">Récupérer toutes les alertes d'un groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="8ed23-147">Retrieve all alerts on a resource group:</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest
```

<span data-ttu-id="8ed23-148">Récupérer toutes les règles d'alerte définies pour une ressource cible.</span><span class="sxs-lookup"><span data-stu-id="8ed23-148">Retrieve all alert rules set for a target resource.</span></span> <span data-ttu-id="8ed23-149">Par exemple, toutes les règles d'alerte définies sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8ed23-149">For example, all alert rules set on a VM.</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest -TargetResourceId /subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig
```

<span data-ttu-id="8ed23-150">`Get-AzureRmAlertRule` prend en charge d'autres paramètres.</span><span class="sxs-lookup"><span data-stu-id="8ed23-150">`Get-AzureRmAlertRule` supports other parameters.</span></span> <span data-ttu-id="8ed23-151">Consultez [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) pour plus d'informations.</span><span class="sxs-lookup"><span data-stu-id="8ed23-151">See [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) for more information.</span></span>

## <a name="create-metric-alerts"></a><span data-ttu-id="8ed23-152">Créer des alertes de métriques</span><span class="sxs-lookup"><span data-stu-id="8ed23-152">Create metric alerts</span></span>
<span data-ttu-id="8ed23-153">Vous pouvez utiliser l’applet de commande `Add-AlertRule` pour créer, mettre à jour ou désactiver une règle d'alerte.</span><span class="sxs-lookup"><span data-stu-id="8ed23-153">You can use the `Add-AlertRule` cmdlet to create, update or disable an alert rule.</span></span>

<span data-ttu-id="8ed23-154">Vous pouvez créer des propriétés de messagerie et webhook à l'aide de `New-AzureRmAlertRuleEmail` et `New-AzureRmAlertRuleWebhook`, respectivement.</span><span class="sxs-lookup"><span data-stu-id="8ed23-154">You can create email and webhook properties using  `New-AzureRmAlertRuleEmail` and `New-AzureRmAlertRuleWebhook`, respectively.</span></span> <span data-ttu-id="8ed23-155">Dans l'applet de commande de la règle d'alerte, affectez ces éléments comme des actions à la propriété **Actions** de la règle d'alerte.</span><span class="sxs-lookup"><span data-stu-id="8ed23-155">In the Alert rule cmdlet, assign these as actions to the **Actions** property of the Alert Rule.</span></span>

<span data-ttu-id="8ed23-156">Le tableau suivant décrit les paramètres et les valeurs utilisés pour créer une alerte à l'aide d'une mesure.</span><span class="sxs-lookup"><span data-stu-id="8ed23-156">The following table describes the parameters and values used to create an alert using a metric.</span></span>

| <span data-ttu-id="8ed23-157">paramètre</span><span class="sxs-lookup"><span data-stu-id="8ed23-157">parameter</span></span> | <span data-ttu-id="8ed23-158">value</span><span class="sxs-lookup"><span data-stu-id="8ed23-158">value</span></span> |
| --- | --- |
| <span data-ttu-id="8ed23-159">Nom</span><span class="sxs-lookup"><span data-stu-id="8ed23-159">Name</span></span> |<span data-ttu-id="8ed23-160">simpletestdiskwrite</span><span class="sxs-lookup"><span data-stu-id="8ed23-160">simpletestdiskwrite</span></span> |
| <span data-ttu-id="8ed23-161">Emplacement de cette règle d'alerte</span><span class="sxs-lookup"><span data-stu-id="8ed23-161">Location of this alert rule</span></span> |<span data-ttu-id="8ed23-162">Est des États-Unis</span><span class="sxs-lookup"><span data-stu-id="8ed23-162">East US</span></span> |
| <span data-ttu-id="8ed23-163">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8ed23-163">ResourceGroup</span></span> |<span data-ttu-id="8ed23-164">montest</span><span class="sxs-lookup"><span data-stu-id="8ed23-164">montest</span></span> |
| <span data-ttu-id="8ed23-165">TargetResourceId</span><span class="sxs-lookup"><span data-stu-id="8ed23-165">TargetResourceId</span></span> |<span data-ttu-id="8ed23-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span><span class="sxs-lookup"><span data-stu-id="8ed23-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span></span> |
| <span data-ttu-id="8ed23-167">MetricName de l'alerte créée</span><span class="sxs-lookup"><span data-stu-id="8ed23-167">MetricName of the alert that is created</span></span> |<span data-ttu-id="8ed23-168">\PhysicalDisk \Disk écritures par seconde. Consultez le `Get-MetricDefinitions` applet de commande sur la façon de récupérer les noms exacts des mesures</span><span class="sxs-lookup"><span data-stu-id="8ed23-168">\PhysicalDisk(_Total)\Disk Writes/sec. See the `Get-MetricDefinitions` cmdlet about how to retrieve the exact metric names</span></span> |
| <span data-ttu-id="8ed23-169">operator</span><span class="sxs-lookup"><span data-stu-id="8ed23-169">operator</span></span> |<span data-ttu-id="8ed23-170">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="8ed23-170">GreaterThan</span></span> |
| <span data-ttu-id="8ed23-171">Valeur de seuil (nombre/s pour cette métrique)</span><span class="sxs-lookup"><span data-stu-id="8ed23-171">Threshold value (count/sec in for this metric)</span></span> |<span data-ttu-id="8ed23-172">1</span><span class="sxs-lookup"><span data-stu-id="8ed23-172">1</span></span> |
| <span data-ttu-id="8ed23-173">WindowSize (format hh:mm:ss)</span><span class="sxs-lookup"><span data-stu-id="8ed23-173">WindowSize (hh:mm:ss format)</span></span> |<span data-ttu-id="8ed23-174">00:05:00</span><span class="sxs-lookup"><span data-stu-id="8ed23-174">00:05:00</span></span> |
| <span data-ttu-id="8ed23-175">agrégation (statistique de la métrique, qui utilise la valeur Average dans ce cas)</span><span class="sxs-lookup"><span data-stu-id="8ed23-175">aggregator (statistic of the metric, which uses Average count, in this case)</span></span> |<span data-ttu-id="8ed23-176">Moyenne</span><span class="sxs-lookup"><span data-stu-id="8ed23-176">Average</span></span> |
| <span data-ttu-id="8ed23-177">courriers électroniques personnalisés (tableau de chaînes)</span><span class="sxs-lookup"><span data-stu-id="8ed23-177">custom emails (string array)</span></span> |<span data-ttu-id="8ed23-178">'foo@example.com','bar@example.com'</span><span class="sxs-lookup"><span data-stu-id="8ed23-178">'foo@example.com','bar@example.com'</span></span> |
| <span data-ttu-id="8ed23-179">envoyer un courrier électronique aux propriétaires, contributeurs et lecteurs</span><span class="sxs-lookup"><span data-stu-id="8ed23-179">send email to owners, contributors and readers</span></span> |<span data-ttu-id="8ed23-180">-SendToServiceOwners</span><span class="sxs-lookup"><span data-stu-id="8ed23-180">-SendToServiceOwners</span></span> |

<span data-ttu-id="8ed23-181">Créer un courrier électronique</span><span class="sxs-lookup"><span data-stu-id="8ed23-181">Create an Email action</span></span>

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

<span data-ttu-id="8ed23-182">Créer une action Webhook</span><span class="sxs-lookup"><span data-stu-id="8ed23-182">Create a Webhook action</span></span>

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

<span data-ttu-id="8ed23-183">Créer la règle d'alerte sur la mesure CPU% sur une machine virtuelle classique</span><span class="sxs-lookup"><span data-stu-id="8ed23-183">Create the alert rule on the CPU% metric on a classic VM</span></span>

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

<span data-ttu-id="8ed23-184">Récupérer la règle d'alerte</span><span class="sxs-lookup"><span data-stu-id="8ed23-184">Retrieve the alert rule</span></span>

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="8ed23-185">L'applet de commande Add alert met également à jour la règle, s'il existe une règle d'alerte pour les propriétés spécifiées.</span><span class="sxs-lookup"><span data-stu-id="8ed23-185">The Add alert cmdlet also updates the rule if an alert rule already exists for the given properties.</span></span> <span data-ttu-id="8ed23-186">Pour désactiver une règle d’alerte, incluez le paramètre **-DisableRule**.</span><span class="sxs-lookup"><span data-stu-id="8ed23-186">To disable an alert rule, include the parameter **-DisableRule**.</span></span>

## <a name="get-a-list-of-available-metrics-for-alerts"></a><span data-ttu-id="8ed23-187">Obtenir la liste des mesures disponibles pour les alertes</span><span class="sxs-lookup"><span data-stu-id="8ed23-187">Get a list of available metrics for alerts</span></span>
<span data-ttu-id="8ed23-188">Vous pouvez utiliser l’applet de commande `Get-AzureRmMetricDefinition` pour afficher la liste de toutes les métriques pour une ressource spécifique.</span><span class="sxs-lookup"><span data-stu-id="8ed23-188">You can use the `Get-AzureRmMetricDefinition` cmdlet to view the list of all metrics for a specific resource.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

<span data-ttu-id="8ed23-189">L'exemple suivant génère une table avec le nom de la mesure et son unité.</span><span class="sxs-lookup"><span data-stu-id="8ed23-189">The following example generates a table with the metric Name and the Unit for it.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

<span data-ttu-id="8ed23-190">Une liste complète des options disponibles pour `Get-AzureRmMetricDefinition` est disponible dans [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span><span class="sxs-lookup"><span data-stu-id="8ed23-190">A full list of available options for `Get-AzureRmMetricDefinition` is available at [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span></span>

## <a name="create-and-manage-autoscale-settings"></a><span data-ttu-id="8ed23-191">Créer et gérer les paramètres de mise à l'échelle automatique</span><span class="sxs-lookup"><span data-stu-id="8ed23-191">Create and manage AutoScale settings</span></span>
<span data-ttu-id="8ed23-192">Une ressource, par exemple une application web, une machine virtuelle, un service cloud ou un groupe de machines virtuelles identiques, ne peut avoir qu’un seul paramètre de mise à l’échelle automatique configuré.</span><span class="sxs-lookup"><span data-stu-id="8ed23-192">A resource, such as a Web app, VM, Cloud Service or Virtual Machine Scale Set can have only one autoscale setting configured for it.</span></span>
<span data-ttu-id="8ed23-193">Cependant, chaque paramètre de mise à l'échelle automatique peut avoir plusieurs profils.</span><span class="sxs-lookup"><span data-stu-id="8ed23-193">However, each autoscale setting can have multiple profiles.</span></span> <span data-ttu-id="8ed23-194">Par exemple, un pour un profil de mise à l’échelle en fonction des performances et un autre pour un profil basé sur une planification.</span><span class="sxs-lookup"><span data-stu-id="8ed23-194">For example, one for a performance-based scale profile and a second one for a schedule-based profile.</span></span> <span data-ttu-id="8ed23-195">Chaque profil peut avoir plusieurs règles configurées.</span><span class="sxs-lookup"><span data-stu-id="8ed23-195">Each profile can have multiple rules configured on it.</span></span> <span data-ttu-id="8ed23-196">Pour plus d’informations sur la mise à l’échelle automatique, voir [Mise à l’échelle automatique d’une application](../cloud-services/cloud-services-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="8ed23-196">For more information about Autoscale, see [How to Autoscale an Application](../cloud-services/cloud-services-how-to-scale.md).</span></span>

<span data-ttu-id="8ed23-197">Voici la procédure que nous allons suivre :</span><span class="sxs-lookup"><span data-stu-id="8ed23-197">Here are the steps we will use:</span></span>

1. <span data-ttu-id="8ed23-198">Créez une ou plusieurs règles.</span><span class="sxs-lookup"><span data-stu-id="8ed23-198">Create rule(s).</span></span>
2. <span data-ttu-id="8ed23-199">Créez un ou plusieurs profils correspondant aux règles que vous avez créées précédemment pour les profils.</span><span class="sxs-lookup"><span data-stu-id="8ed23-199">Create profile(s) mapping the rules that you created previously to the profiles.</span></span>
3. <span data-ttu-id="8ed23-200">Facultatif : créez des notifications de mise à l'échelle automatique en configurant les propriétés de courrier électronique et webhook.</span><span class="sxs-lookup"><span data-stu-id="8ed23-200">Optional: Create notifications for autoscale by configuring webhook and email properties.</span></span>
4. <span data-ttu-id="8ed23-201">Créez un paramètre de mise à l'échelle automatique avec un nom pour la ressource cible en mappant les profils et les notifications que vous avez créés aux étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="8ed23-201">Create an autoscale setting with a name on the target resource by mapping the profiles and notifications that you created in the previous steps.</span></span>

<span data-ttu-id="8ed23-202">Les exemples suivants montrent comment créer un paramètre de mise à l’échelle automatique pour un groupe de machines virtuelles identiques sur un système d’exploitation Windows à l’aide de la métrique d’utilisation du processeur.</span><span class="sxs-lookup"><span data-stu-id="8ed23-202">The following examples show you how you can create an Autoscale setting for a Virtual Machine Scale Set for a Windows operating system based by using the CPU utilization metric.</span></span>

<span data-ttu-id="8ed23-203">Tout d’abord, créez une règle de montée en charge, avec augmentation du nombre d’instances.</span><span class="sxs-lookup"><span data-stu-id="8ed23-203">First, create a rule to scale-out, with an instance count increase.</span></span>

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

<span data-ttu-id="8ed23-204">Créez ensuite une règle de baisse de charge, avec une diminution du nombre d’instances.</span><span class="sxs-lookup"><span data-stu-id="8ed23-204">Next, create a rule to scale-in, with an instance count decrease.</span></span>

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

<span data-ttu-id="8ed23-205">Puis créez un profil pour les règles.</span><span class="sxs-lookup"><span data-stu-id="8ed23-205">Then, create a profile for the rules.</span></span>

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

<span data-ttu-id="8ed23-206">Créez une propriété webhook</span><span class="sxs-lookup"><span data-stu-id="8ed23-206">Create a webhook property.</span></span>

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

<span data-ttu-id="8ed23-207">Créez la propriété de notification pour le paramètre de mise à l'échelle automatique, y compris les propriétés de courrier électronique et webhook que vous avez créées précédemment.</span><span class="sxs-lookup"><span data-stu-id="8ed23-207">Create the notification property for the autoscale setting, including email and the webhook that you created previously.</span></span>

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

<span data-ttu-id="8ed23-208">Enfin, créez le paramètre de mise à l'échelle automatique pour ajouter le profil que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="8ed23-208">Finally, create the autoscale setting to add the profile that you created above.</span></span>

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

<span data-ttu-id="8ed23-209">Pour plus d’informations sur la gestion des paramètres de mise à l’échelle automatique, voir [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span><span class="sxs-lookup"><span data-stu-id="8ed23-209">For more information about managing Autoscale settings, see [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span></span>

## <a name="autoscale-history"></a><span data-ttu-id="8ed23-210">Historique de la mise à l'échelle automatique</span><span class="sxs-lookup"><span data-stu-id="8ed23-210">Autoscale history</span></span>
<span data-ttu-id="8ed23-211">L'exemple suivant vous montre comment consulter les dernières mises à l'échelle automatiques et les derniers événements d'alerte.</span><span class="sxs-lookup"><span data-stu-id="8ed23-211">The following example shows you how you can view recent autoscale and alert events.</span></span> <span data-ttu-id="8ed23-212">Utilisez la recherche du journal d’activité pour afficher l'historique de mise à l'échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="8ed23-212">Use the activity log search to view the autoscale history.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="8ed23-213">Vous pouvez utiliser l’applet de commande `Get-AzureRmAutoScaleHistory` pour récupérer l’historique de mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="8ed23-213">You can use the `Get-AzureRmAutoScaleHistory` cmdlet to retrieve AutoScale history.</span></span>

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

<span data-ttu-id="8ed23-214">Pour plus d’informations, voir [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span><span class="sxs-lookup"><span data-stu-id="8ed23-214">For more information, see [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span></span>

### <a name="view-details-for-an-autoscale-setting"></a><span data-ttu-id="8ed23-215">Afficher les détails d'un paramètre de mise à l'échelle automatique</span><span class="sxs-lookup"><span data-stu-id="8ed23-215">View details for an autoscale setting</span></span>
<span data-ttu-id="8ed23-216">Vous pouvez utiliser l’applet de commande `Get-Autoscalesetting` pour récupérer des informations supplémentaires sur le paramètre de mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="8ed23-216">You can use the `Get-Autoscalesetting` cmdlet to retrieve more information about the autoscale setting.</span></span>

<span data-ttu-id="8ed23-217">L'exemple suivant affiche des détails concernant tous les paramètres de mise à l'échelle automatique dans le groupe de ressources ’myrg1’.</span><span class="sxs-lookup"><span data-stu-id="8ed23-217">The following example shows details about all autoscale settings in the resource group 'myrg1'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="8ed23-218">L'exemple suivant affiche des détails concernant tous les paramètres de mise à l'échelle automatique dans le groupe de ressources ’myrg1’, et en particulier le paramètre de mise à l'échelle automatique nommé ’MyScaleVMSSSetting’.</span><span class="sxs-lookup"><span data-stu-id="8ed23-218">The following example shows details about all autoscale settings in the resource group 'myrg1' and specifically the autoscale setting named 'MyScaleVMSSSetting'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a><span data-ttu-id="8ed23-219">Supprimer un paramètre de mise à l'échelle automatique</span><span class="sxs-lookup"><span data-stu-id="8ed23-219">Remove an autoscale setting</span></span>
<span data-ttu-id="8ed23-220">Vous pouvez utiliser l’applet de commande `Remove-Autoscalesetting` pour supprimer un paramètre de mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="8ed23-220">You can use the `Remove-Autoscalesetting` cmdlet to delete an autoscale setting.</span></span>

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a><span data-ttu-id="8ed23-221">Gérer les profils de journal pour le journal d’activité</span><span class="sxs-lookup"><span data-stu-id="8ed23-221">Manage log profiles for activity log</span></span>
<span data-ttu-id="8ed23-222">Vous pouvez créer un *profil de journal* et exporter des données de votre journal d’activité vers un compte de stockage, puis configurer la rétention de données pour celui-ci.</span><span class="sxs-lookup"><span data-stu-id="8ed23-222">You can create a *log profile* and export data from your activity log to a storage account and you can configure data retention for it.</span></span> <span data-ttu-id="8ed23-223">Si vous le souhaitez, vous pouvez aussi transmettre en continu les données vers votre hub d'événements.</span><span class="sxs-lookup"><span data-stu-id="8ed23-223">Optionally, you can also stream the data to your Event Hub.</span></span> <span data-ttu-id="8ed23-224">Notez que cette fonctionnalité est actuellement en version préliminaire et vous ne pouvez créer qu'un seul profil de journal par abonnement.</span><span class="sxs-lookup"><span data-stu-id="8ed23-224">Note that this feature is currently in Preview and you can only create one log profile per subscription.</span></span> <span data-ttu-id="8ed23-225">Vous pouvez utiliser les applets de commande suivantes avec votre abonnement actuel pour créer et gérer des profils de journal.</span><span class="sxs-lookup"><span data-stu-id="8ed23-225">You can use the following cmdlets with your current subscription to create and manage log profiles.</span></span> <span data-ttu-id="8ed23-226">Vous pouvez également choisir un abonnement spécifique.</span><span class="sxs-lookup"><span data-stu-id="8ed23-226">You can also choose a particular subscription.</span></span> <span data-ttu-id="8ed23-227">Bien que PowerShell utilise par défaut l’abonnement actif, vous pouvez toujours modifier ce paramètre avec `Set-AzureRmContext`.</span><span class="sxs-lookup"><span data-stu-id="8ed23-227">Although PowerShell defaults to the current subscription, you can always change that using `Set-AzureRmContext`.</span></span> <span data-ttu-id="8ed23-228">Vous pouvez configurer le journal d’activité afin d’acheminer les données vers n'importe quel compte de stockage ou un hub d'événements au sein de cet abonnement.</span><span class="sxs-lookup"><span data-stu-id="8ed23-228">You can configure activity log to route data to any storage account or Event Hub within that subscription.</span></span> <span data-ttu-id="8ed23-229">Les données sont écrites en tant que fichiers blob au format JSON.</span><span class="sxs-lookup"><span data-stu-id="8ed23-229">Data is written as blob files in JSON format.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="8ed23-230">Obtenir un profil de journal</span><span class="sxs-lookup"><span data-stu-id="8ed23-230">Get a log profile</span></span>
<span data-ttu-id="8ed23-231">Pour extraire vos profils de journal existants, utilisez l’applet de commande `Get-AzureRmLogProfile` .</span><span class="sxs-lookup"><span data-stu-id="8ed23-231">To fetch your existing log profiles, use the `Get-AzureRmLogProfile` cmdlet.</span></span>

### <a name="add-a-log-profile-without-data-retention"></a><span data-ttu-id="8ed23-232">Ajouter un profil de journal sans conservation des données</span><span class="sxs-lookup"><span data-stu-id="8ed23-232">Add a log profile without data retention</span></span>
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="8ed23-233">Supprimer un profil de journal</span><span class="sxs-lookup"><span data-stu-id="8ed23-233">Remove a log profile</span></span>
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a><span data-ttu-id="8ed23-234">Ajouter un profil de journal avec conservation des données</span><span class="sxs-lookup"><span data-stu-id="8ed23-234">Add a log profile with data retention</span></span>
<span data-ttu-id="8ed23-235">Vous pouvez spécifier la propriété **-RetentionInDays** en indiquant le nombre de jours (sous la forme d’un entier positif) durant lequel les données seront conservées.</span><span class="sxs-lookup"><span data-stu-id="8ed23-235">You can specify the **-RetentionInDays** property with the number of days, as a positive integer, where the data is retained.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="8ed23-236">Ajouter un profil de journal avec conservation des données et hub d'événements</span><span class="sxs-lookup"><span data-stu-id="8ed23-236">Add log profile with retention and EventHub</span></span>
<span data-ttu-id="8ed23-237">En plus du routage de vos données vers un compte de stockage, vous pouvez également transmettre en continu ces données vers un hub d'événements.</span><span class="sxs-lookup"><span data-stu-id="8ed23-237">In addition to routing your data to storage account, you can also stream it to an Event Hub.</span></span> <span data-ttu-id="8ed23-238">Notez que dans cette version préliminaire, la configuration du compte de stockage est obligatoire mais la configuration du hub d'événements est facultative.</span><span class="sxs-lookup"><span data-stu-id="8ed23-238">Note that in this preview release and the storage account configuration is mandatory but Event Hub configuration is optional.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a><span data-ttu-id="8ed23-239">Configuration des journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="8ed23-239">Configure diagnostics logs</span></span>
<span data-ttu-id="8ed23-240">De nombreux services Azure fournissent des journaux et des télémétries supplémentaires qui peuvent être configurés pour enregistrer des données dans votre compte de stockage Azure, les envoyer à Event Hubs et/ou les envoyer à un espace de travail Log Analytics OMS.</span><span class="sxs-lookup"><span data-stu-id="8ed23-240">Many Azure services provide additional logs and telemetry that can be configured to save data in your Azure Storage account, send to Event Hubs, and/or sent to an OMS Log Analytics workspace.</span></span> <span data-ttu-id="8ed23-241">Cette opération ne peut être effectuée qu’au niveau d’une ressource, et le compte de stockage ou l’Event Hub doit être présent dans la même région que la ressource cible où les paramètres de diagnostic sont configurés.</span><span class="sxs-lookup"><span data-stu-id="8ed23-241">That operation can only be performed at a resource level and the storage account or event hub should be present in the same region as the target resource where the diagnostics setting is configured.</span></span>

### <a name="get-diagnostic-setting"></a><span data-ttu-id="8ed23-242">Obtenir le paramètre de diagnostic</span><span class="sxs-lookup"><span data-stu-id="8ed23-242">Get diagnostic setting</span></span>
```PowerShell
Get-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp
```

<span data-ttu-id="8ed23-243">Désactiver le paramètre de diagnostic</span><span class="sxs-lookup"><span data-stu-id="8ed23-243">Disable diagnostic setting</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $false
```

<span data-ttu-id="8ed23-244">Activer le paramètre de diagnostic sans conservation</span><span class="sxs-lookup"><span data-stu-id="8ed23-244">Enable diagnostic setting without retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true
```

<span data-ttu-id="8ed23-245">Activer le paramètre de diagnostic avec conservation</span><span class="sxs-lookup"><span data-stu-id="8ed23-245">Enable diagnostic setting with retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="8ed23-246">Activer un paramètre diagnostic avec conservation pour une catégorie de journal spécifique</span><span class="sxs-lookup"><span data-stu-id="8ed23-246">Enable diagnostic setting with retention for a specific log category</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/sakteststorage -Categories NetworkSecurityGroupEvent -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="8ed23-247">Activer le paramètre de diagnostic pour Event Hubs</span><span class="sxs-lookup"><span data-stu-id="8ed23-247">Enable diagnostic setting for Event Hubs</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Enable $true
```

<span data-ttu-id="8ed23-248">Activer le paramètre de diagnostic pour OMS</span><span class="sxs-lookup"><span data-stu-id="8ed23-248">Enable diagnostic setting for OMS</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -WorkspaceId 76d785fd-d1ce-4f50-8ca3-858fc819ca0f -Enabled $true

```
