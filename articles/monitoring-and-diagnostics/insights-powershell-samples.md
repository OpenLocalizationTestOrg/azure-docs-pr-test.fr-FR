---
title: "exemples de démarrage rapide de PowerShell d’analyse aaaAzure. | Microsoft Docs"
description: "Utilisez PowerShell tooaccess les fonctionnalités de moniteur de Windows Azure telles que la mise à l’échelle, les alertes, webhooks et recherche les journaux d’activité."
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
ms.openlocfilehash: 6eece0b0227e0bbf08225bd330d0601169911f55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor-powershell-quick-start-samples"></a><span data-ttu-id="d4ba0-104">Exemples de démarrage rapide Azure Monitor PowerShell</span><span class="sxs-lookup"><span data-stu-id="d4ba0-104">Azure Monitor PowerShell quick start samples</span></span>
<span data-ttu-id="d4ba0-105">Cet article explique les exemples de toohelp de commandes PowerShell vous accéder aux fonctionnalités du moniteur de Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-105">This article shows you sample PowerShell commands toohelp you access Azure Monitor features.</span></span> <span data-ttu-id="d4ba0-106">Moniteur de Azure vous permet de tooAutoScale Services de cloud computing, Machines virtuelles et les applications Web et toosend des notifications d’alerte ou des URL web appel en fonction des valeurs de données de télémétrie configuré.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-106">Azure Monitor allows you tooAutoScale Cloud Services, Virtual Machines, and Web Apps and toosend alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="d4ba0-107">Moniteur de Azure est hello nouveau nom pour ce qui a été appelé « Azure Insights » jusqu'à 25 septembre 2016.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-107">Azure Monitor is hello new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="d4ba0-108">Toutefois, les espaces de noms hello et par conséquent hello suit toujours les commandes contient insights » l’hello ».</span><span class="sxs-lookup"><span data-stu-id="d4ba0-108">However, hello namespaces and thus hello following commands still contain hello "insights".</span></span>
> 
> 

## <a name="set-up-powershell"></a><span data-ttu-id="d4ba0-109">Configurer PowerShell</span><span class="sxs-lookup"><span data-stu-id="d4ba0-109">Set up PowerShell</span></span>
<span data-ttu-id="d4ba0-110">Si vous n’avez pas encore, définir toorun PowerShell sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-110">If you haven't already, set up PowerShell toorun on your computer.</span></span> <span data-ttu-id="d4ba0-111">Pour plus d’informations, consultez [comment tooInstall et configurer les PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d4ba0-111">For more information, see [How tooInstall and Configure PowerShell](/powershell/azure/overview).</span></span>

## <a name="examples-in-this-article"></a><span data-ttu-id="d4ba0-112">Exemples de cet article</span><span class="sxs-lookup"><span data-stu-id="d4ba0-112">Examples in this article</span></span>
<span data-ttu-id="d4ba0-113">exemples de Hello dans l’article de hello illustrent comment vous pouvez utiliser les applets de commande de moniteur de Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-113">hello examples in hello article illustrate how you can use Azure Monitor cmdlets.</span></span> <span data-ttu-id="d4ba0-114">Vous pouvez également examiner hello intégralité de la liste des applets de commande PowerShell d’analyse Azure à [applets de commande Azure moniteur (Insights)](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4ba0-114">You can also review hello entire list of Azure Monitor PowerShell cmdlets at [Azure Monitor (Insights) Cmdlets](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span></span>

## <a name="sign-in-and-use-subscriptions"></a><span data-ttu-id="d4ba0-115">Se connecter et utiliser des abonnements</span><span class="sxs-lookup"><span data-stu-id="d4ba0-115">Sign in and use subscriptions</span></span>
<span data-ttu-id="d4ba0-116">Tout d’abord, ouvrez une session dans tooyour abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-116">First, log in tooyour Azure subscription.</span></span>

```PowerShell
Login-AzureRmAccount
```

<span data-ttu-id="d4ba0-117">Cela vous toosign dans.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-117">This requires you toosign in.</span></span> <span data-ttu-id="d4ba0-118">Vos informations de compte, d’ID de locataire et d’ID d’abonnement par défaut s’affichent alors.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-118">Once you do, your Account, TenantID and default Subscription ID are displayed.</span></span> <span data-ttu-id="d4ba0-119">Tous les hello des applets de commande Azure fonctionnent dans le contexte de hello de votre abonnement par défaut.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-119">All hello Azure cmdlets work in hello context of your default subscription.</span></span> <span data-ttu-id="d4ba0-120">liste de hello tooview des abonnements que vous avez accès à, utilisez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-120">tooview hello list of subscriptions you have access to, use hello following command.</span></span>

```PowerShell
Get-AzureRmSubscription
```

<span data-ttu-id="d4ba0-121">toochange votre travail contexte tooa autre abonnement, hello utilisez commande suivante.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-121">toochange your working context tooa different subscription, use hello following command.</span></span>

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a><span data-ttu-id="d4ba0-122">Récupérer le journal d’activité d’un abonnement</span><span class="sxs-lookup"><span data-stu-id="d4ba0-122">Retrieve Activity log for a subscription</span></span>
<span data-ttu-id="d4ba0-123">Hello d’utilisation `Get-AzureRmLog` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-123">Use hello `Get-AzureRmLog` cmdlet.</span></span>  <span data-ttu-id="d4ba0-124">Hello Voici des exemples courants.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-124">hello following are some common examples.</span></span>

<span data-ttu-id="d4ba0-125">Obtenir les entrées de journal à partir de cette toopresent date/heure :</span><span class="sxs-lookup"><span data-stu-id="d4ba0-125">Get log entries from this time/date toopresent:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2016-03-01T10:30
```

<span data-ttu-id="d4ba0-126">Obtenir les entrées de journal entre une plage de dates/heures :</span><span class="sxs-lookup"><span data-stu-id="d4ba0-126">Get log entries between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="d4ba0-127">Obtenir les entrées de journal à partir d'un groupe de ressources spécifique :</span><span class="sxs-lookup"><span data-stu-id="d4ba0-127">Get log entries from a specific resource group:</span></span>

```PowerShell
Get-AzureRmLog -ResourceGroup 'myrg1'
```

<span data-ttu-id="d4ba0-128">Obtenir les entrées de journal à partir d'un fournisseur de ressources spécifique entre une plage de dates/heures :</span><span class="sxs-lookup"><span data-stu-id="d4ba0-128">Get log entries from a specific resource provider between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -ResourceProvider 'Microsoft.Web' -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="d4ba0-129">Obtenir toutes les entrées de journal avec un appelant spécifique :</span><span class="sxs-lookup"><span data-stu-id="d4ba0-129">Get all log entries with a specific caller:</span></span>

```PowerShell
Get-AzureRmLog -Caller 'myname@company.com'
```

<span data-ttu-id="d4ba0-130">Hello récupère hello 1000 derniers événements hello journal d’activité de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d4ba0-130">hello following command retrieves hello last 1000 events from hello activity log:</span></span>

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

<span data-ttu-id="d4ba0-131">`Get-AzureRmLog` prend en charge de nombreux autres paramètres.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-131">`Get-AzureRmLog` supports many other parameters.</span></span> <span data-ttu-id="d4ba0-132">Consultez hello `Get-AzureRmLog` référence pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-132">See hello `Get-AzureRmLog` reference for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="d4ba0-133">`Get-AzureRmLog` fournit uniquement 15 jours d'historique.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-133">`Get-AzureRmLog` only provides 15 days of history.</span></span> <span data-ttu-id="d4ba0-134">À l’aide de hello **- MaxEvents** paramètre vous permet de tooquery hello dernière N événements, au-delà de 15 jours.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-134">Using hello **-MaxEvents** parameter allows you tooquery hello last N events, beyond 15 days.</span></span> <span data-ttu-id="d4ba0-135">événements tooaccess plus de 15 jours, utilisez hello API REST ou le Kit de développement logiciel (exemple c# à l’aide du Kit de développement logiciel de hello).</span><span class="sxs-lookup"><span data-stu-id="d4ba0-135">tooaccess events older than 15 days, use hello REST API or SDK (C# sample using hello SDK).</span></span> <span data-ttu-id="d4ba0-136">Si vous n’incluez pas **StartTime**, la valeur par défaut hello **EndTime** moins d’une heure.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-136">If you do not include **StartTime**, then hello default value is **EndTime** minus one hour.</span></span> <span data-ttu-id="d4ba0-137">Si vous n’incluez pas **EndTime**, valeur par défaut de hello est l’heure actuelle.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-137">If you do not include **EndTime**, then hello default value is current time.</span></span> <span data-ttu-id="d4ba0-138">Toutes les heures sont exprimées en heure UTC.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-138">All times are in UTC.</span></span>
> 
> 

## <a name="retrieve-alerts-history"></a><span data-ttu-id="d4ba0-139">Récupérer l'historique des alertes</span><span class="sxs-lookup"><span data-stu-id="d4ba0-139">Retrieve alerts history</span></span>
<span data-ttu-id="d4ba0-140">tooview tous les événements d’alerte, vous pouvez interroger hello journaux Azure Resource Manager à l’aide de hello exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-140">tooview all alert events, you can query hello Azure Resource Manager logs using hello following examples.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="d4ba0-141">règle de l’historique de hello tooview pour une alerte spécifique, vous pouvez utiliser hello `Get-AzureRmAlertHistory` applet de commande, en passant un ID de ressource hello de règle d’alerte hello.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-141">tooview hello history for a specific alert rule, you can use hello `Get-AzureRmAlertHistory` cmdlet, passing in hello resource ID of hello alert rule.</span></span>

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

<span data-ttu-id="d4ba0-142">Hello `Get-AzureRmAlertHistory` applet de commande prend en charge les différents paramètres.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-142">hello `Get-AzureRmAlertHistory` cmdlet supports various parameters.</span></span> <span data-ttu-id="d4ba0-143">Plus d'informations, consultez [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4ba0-143">More information, see [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span></span>

## <a name="retrieve-information-on-alert-rules"></a><span data-ttu-id="d4ba0-144">Récupérer des informations sur les règles d'alerte</span><span class="sxs-lookup"><span data-stu-id="d4ba0-144">Retrieve information on alert rules</span></span>
<span data-ttu-id="d4ba0-145">Tous les hello suivant les commandes agissent sur un groupe de ressources nommé « montest ».</span><span class="sxs-lookup"><span data-stu-id="d4ba0-145">All of hello following commands act on a Resource Group named "montest".</span></span>

<span data-ttu-id="d4ba0-146">Afficher toutes les propriétés de hello de règle d’alerte hello :</span><span class="sxs-lookup"><span data-stu-id="d4ba0-146">View all hello properties of hello alert rule:</span></span>

```PowerShell
Get-AzureRmAlertRule -Name simpletestCPU -ResourceGroup montest -DetailedOutput
```

<span data-ttu-id="d4ba0-147">Récupérer toutes les alertes d'un groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="d4ba0-147">Retrieve all alerts on a resource group:</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest
```

<span data-ttu-id="d4ba0-148">Récupérer toutes les règles d'alerte définies pour une ressource cible.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-148">Retrieve all alert rules set for a target resource.</span></span> <span data-ttu-id="d4ba0-149">Par exemple, toutes les règles d'alerte définies sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-149">For example, all alert rules set on a VM.</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest -TargetResourceId /subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig
```

<span data-ttu-id="d4ba0-150">`Get-AzureRmAlertRule` prend en charge d'autres paramètres.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-150">`Get-AzureRmAlertRule` supports other parameters.</span></span> <span data-ttu-id="d4ba0-151">Consultez [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) pour plus d'informations.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-151">See [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) for more information.</span></span>

## <a name="create-metric-alerts"></a><span data-ttu-id="d4ba0-152">Créer des alertes de métriques</span><span class="sxs-lookup"><span data-stu-id="d4ba0-152">Create metric alerts</span></span>
<span data-ttu-id="d4ba0-153">Vous pouvez utiliser hello `Add-AlertRule` toocreate de l’applet de commande, mettre à jour ou désactiver une règle d’alerte.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-153">You can use hello `Add-AlertRule` cmdlet toocreate, update or disable an alert rule.</span></span>

<span data-ttu-id="d4ba0-154">Vous pouvez créer des propriétés de messagerie et webhook à l'aide de `New-AzureRmAlertRuleEmail` et `New-AzureRmAlertRuleWebhook`, respectivement.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-154">You can create email and webhook properties using  `New-AzureRmAlertRuleEmail` and `New-AzureRmAlertRuleWebhook`, respectively.</span></span> <span data-ttu-id="d4ba0-155">Dans l’applet de commande de règle d’alerte hello attribuer en tant qu’actions toohello **Actions** propriété Hello règle d’alerte.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-155">In hello Alert rule cmdlet, assign these as actions toohello **Actions** property of hello Alert Rule.</span></span>

<span data-ttu-id="d4ba0-156">Hello tableau suivant décrit les paramètres hello et valeurs utilisé toocreate une alerte à l’aide d’une métrique.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-156">hello following table describes hello parameters and values used toocreate an alert using a metric.</span></span>

| <span data-ttu-id="d4ba0-157">paramètre</span><span class="sxs-lookup"><span data-stu-id="d4ba0-157">parameter</span></span> | <span data-ttu-id="d4ba0-158">value</span><span class="sxs-lookup"><span data-stu-id="d4ba0-158">value</span></span> |
| --- | --- |
| <span data-ttu-id="d4ba0-159">Nom</span><span class="sxs-lookup"><span data-stu-id="d4ba0-159">Name</span></span> |<span data-ttu-id="d4ba0-160">simpletestdiskwrite</span><span class="sxs-lookup"><span data-stu-id="d4ba0-160">simpletestdiskwrite</span></span> |
| <span data-ttu-id="d4ba0-161">Emplacement de cette règle d'alerte</span><span class="sxs-lookup"><span data-stu-id="d4ba0-161">Location of this alert rule</span></span> |<span data-ttu-id="d4ba0-162">Est des États-Unis</span><span class="sxs-lookup"><span data-stu-id="d4ba0-162">East US</span></span> |
| <span data-ttu-id="d4ba0-163">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d4ba0-163">ResourceGroup</span></span> |<span data-ttu-id="d4ba0-164">montest</span><span class="sxs-lookup"><span data-stu-id="d4ba0-164">montest</span></span> |
| <span data-ttu-id="d4ba0-165">TargetResourceId</span><span class="sxs-lookup"><span data-stu-id="d4ba0-165">TargetResourceId</span></span> |<span data-ttu-id="d4ba0-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span><span class="sxs-lookup"><span data-stu-id="d4ba0-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span></span> |
| <span data-ttu-id="d4ba0-167">MetricName d’alerte de hello est créé</span><span class="sxs-lookup"><span data-stu-id="d4ba0-167">MetricName of hello alert that is created</span></span> |<span data-ttu-id="d4ba0-168">\PhysicalDisk \Disk écritures par seconde. Consultez hello `Get-MetricDefinitions` applet de commande sur comment tooretrieve hello des noms de métrique exactes</span><span class="sxs-lookup"><span data-stu-id="d4ba0-168">\PhysicalDisk(_Total)\Disk Writes/sec. See hello `Get-MetricDefinitions` cmdlet about how tooretrieve hello exact metric names</span></span> |
| <span data-ttu-id="d4ba0-169">operator</span><span class="sxs-lookup"><span data-stu-id="d4ba0-169">operator</span></span> |<span data-ttu-id="d4ba0-170">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="d4ba0-170">GreaterThan</span></span> |
| <span data-ttu-id="d4ba0-171">Valeur de seuil (nombre/s pour cette métrique)</span><span class="sxs-lookup"><span data-stu-id="d4ba0-171">Threshold value (count/sec in for this metric)</span></span> |<span data-ttu-id="d4ba0-172">1</span><span class="sxs-lookup"><span data-stu-id="d4ba0-172">1</span></span> |
| <span data-ttu-id="d4ba0-173">WindowSize (format hh:mm:ss)</span><span class="sxs-lookup"><span data-stu-id="d4ba0-173">WindowSize (hh:mm:ss format)</span></span> |<span data-ttu-id="d4ba0-174">00:05:00</span><span class="sxs-lookup"><span data-stu-id="d4ba0-174">00:05:00</span></span> |
| <span data-ttu-id="d4ba0-175">agrégation (statistique de mesure hello, qui utilise le nombre moyen de, dans ce cas)</span><span class="sxs-lookup"><span data-stu-id="d4ba0-175">aggregator (statistic of hello metric, which uses Average count, in this case)</span></span> |<span data-ttu-id="d4ba0-176">Moyenne</span><span class="sxs-lookup"><span data-stu-id="d4ba0-176">Average</span></span> |
| <span data-ttu-id="d4ba0-177">courriers électroniques personnalisés (tableau de chaînes)</span><span class="sxs-lookup"><span data-stu-id="d4ba0-177">custom emails (string array)</span></span> |<span data-ttu-id="d4ba0-178">'foo@example.com','bar@example.com'</span><span class="sxs-lookup"><span data-stu-id="d4ba0-178">'foo@example.com','bar@example.com'</span></span> |
| <span data-ttu-id="d4ba0-179">envoyer par courrier électronique tooowners, les collaborateurs et les lecteurs</span><span class="sxs-lookup"><span data-stu-id="d4ba0-179">send email tooowners, contributors and readers</span></span> |<span data-ttu-id="d4ba0-180">-SendToServiceOwners</span><span class="sxs-lookup"><span data-stu-id="d4ba0-180">-SendToServiceOwners</span></span> |

<span data-ttu-id="d4ba0-181">Créer un courrier électronique</span><span class="sxs-lookup"><span data-stu-id="d4ba0-181">Create an Email action</span></span>

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

<span data-ttu-id="d4ba0-182">Créer une action Webhook</span><span class="sxs-lookup"><span data-stu-id="d4ba0-182">Create a Webhook action</span></span>

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

<span data-ttu-id="d4ba0-183">Créer une règle d’alerte hello sur métrique de % processeur hello sur une machine virtuelle classique</span><span class="sxs-lookup"><span data-stu-id="d4ba0-183">Create hello alert rule on hello CPU% metric on a classic VM</span></span>

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

<span data-ttu-id="d4ba0-184">Récupérer la règle d’alerte hello</span><span class="sxs-lookup"><span data-stu-id="d4ba0-184">Retrieve hello alert rule</span></span>

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="d4ba0-185">applet de commande alerte Hello ajouter met également à jour les règles de hello si une règle d’alerte existe déjà pour hello propriété.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-185">hello Add alert cmdlet also updates hello rule if an alert rule already exists for hello given properties.</span></span> <span data-ttu-id="d4ba0-186">toodisable une règle d’alerte, incluez le paramètre hello **- DisableRule**.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-186">toodisable an alert rule, include hello parameter **-DisableRule**.</span></span>

## <a name="get-a-list-of-available-metrics-for-alerts"></a><span data-ttu-id="d4ba0-187">Obtenir la liste des mesures disponibles pour les alertes</span><span class="sxs-lookup"><span data-stu-id="d4ba0-187">Get a list of available metrics for alerts</span></span>
<span data-ttu-id="d4ba0-188">Vous pouvez utiliser hello `Get-AzureRmMetricDefinition` applet de commande tooview hello parmi toutes les métriques pour une ressource spécifique.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-188">You can use hello `Get-AzureRmMetricDefinition` cmdlet tooview hello list of all metrics for a specific resource.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

<span data-ttu-id="d4ba0-189">Hello exemple suivant génère une table avec mesure de hello nom et le hello unité pour celle-ci.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-189">hello following example generates a table with hello metric Name and hello Unit for it.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

<span data-ttu-id="d4ba0-190">Une liste complète des options disponibles pour `Get-AzureRmMetricDefinition` est disponible dans [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4ba0-190">A full list of available options for `Get-AzureRmMetricDefinition` is available at [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span></span>

## <a name="create-and-manage-autoscale-settings"></a><span data-ttu-id="d4ba0-191">Créer et gérer les paramètres de mise à l'échelle automatique</span><span class="sxs-lookup"><span data-stu-id="d4ba0-191">Create and manage AutoScale settings</span></span>
<span data-ttu-id="d4ba0-192">Une ressource, par exemple une application web, une machine virtuelle, un service cloud ou un groupe de machines virtuelles identiques, ne peut avoir qu’un seul paramètre de mise à l’échelle automatique configuré.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-192">A resource, such as a Web app, VM, Cloud Service or Virtual Machine Scale Set can have only one autoscale setting configured for it.</span></span>
<span data-ttu-id="d4ba0-193">Cependant, chaque paramètre de mise à l'échelle automatique peut avoir plusieurs profils.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-193">However, each autoscale setting can have multiple profiles.</span></span> <span data-ttu-id="d4ba0-194">Par exemple, un pour un profil de mise à l’échelle en fonction des performances et un autre pour un profil basé sur une planification.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-194">For example, one for a performance-based scale profile and a second one for a schedule-based profile.</span></span> <span data-ttu-id="d4ba0-195">Chaque profil peut avoir plusieurs règles configurées.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-195">Each profile can have multiple rules configured on it.</span></span> <span data-ttu-id="d4ba0-196">Pour plus d’informations sur l’échelle automatique, consultez [comment tooAutoscale une Application](../cloud-services/cloud-services-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="d4ba0-196">For more information about Autoscale, see [How tooAutoscale an Application](../cloud-services/cloud-services-how-to-scale.md).</span></span>

<span data-ttu-id="d4ba0-197">Voici les étapes hello que nous allons utiliser :</span><span class="sxs-lookup"><span data-stu-id="d4ba0-197">Here are hello steps we will use:</span></span>

1. <span data-ttu-id="d4ba0-198">Créez une ou plusieurs règles.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-198">Create rule(s).</span></span>
2. <span data-ttu-id="d4ba0-199">Créer des profils hello du mappage des règles que vous avez créé précédemment toohello profils.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-199">Create profile(s) mapping hello rules that you created previously toohello profiles.</span></span>
3. <span data-ttu-id="d4ba0-200">Facultatif : créez des notifications de mise à l'échelle automatique en configurant les propriétés de courrier électronique et webhook.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-200">Optional: Create notifications for autoscale by configuring webhook and email properties.</span></span>
4. <span data-ttu-id="d4ba0-201">Créez un paramètre de mise à l’échelle avec un nom de la ressource cible de hello en mappant les profils hello et les notifications que vous avez créé dans les étapes précédentes hello.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-201">Create an autoscale setting with a name on hello target resource by mapping hello profiles and notifications that you created in hello previous steps.</span></span>

<span data-ttu-id="d4ba0-202">Hello exemples suivants montrent comment vous pouvez créer un paramètre d’échelle automatique pour un ensemble d’échelle de Machine virtuelle pour un système d’exploitation de Windows basé l’aide de métriques d’utilisation du processeur de hello.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-202">hello following examples show you how you can create an Autoscale setting for a Virtual Machine Scale Set for a Windows operating system based by using hello CPU utilization metric.</span></span>

<span data-ttu-id="d4ba0-203">Tout d’abord, créez une règle tooscale à la sortie, avec une augmentation de nombre d’instance.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-203">First, create a rule tooscale-out, with an instance count increase.</span></span>

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

<span data-ttu-id="d4ba0-204">Ensuite, créez une règle tooscale dans, avec une diminution du nombre instance.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-204">Next, create a rule tooscale-in, with an instance count decrease.</span></span>

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

<span data-ttu-id="d4ba0-205">Ensuite, créez un profil pour les règles de hello.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-205">Then, create a profile for hello rules.</span></span>

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

<span data-ttu-id="d4ba0-206">Créez une propriété webhook</span><span class="sxs-lookup"><span data-stu-id="d4ba0-206">Create a webhook property.</span></span>

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

<span data-ttu-id="d4ba0-207">Créer une propriété de notification de hello pour le paramètre de mise à l’échelle hello, notamment le courrier électronique et hello webhook que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-207">Create hello notification property for hello autoscale setting, including email and hello webhook that you created previously.</span></span>

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

<span data-ttu-id="d4ba0-208">Enfin, créez hello échelle tooadd hello profil de paramètre que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-208">Finally, create hello autoscale setting tooadd hello profile that you created above.</span></span>

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

<span data-ttu-id="d4ba0-209">Pour plus d’informations sur la gestion des paramètres de mise à l’échelle automatique, voir [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4ba0-209">For more information about managing Autoscale settings, see [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span></span>

## <a name="autoscale-history"></a><span data-ttu-id="d4ba0-210">Historique de la mise à l'échelle automatique</span><span class="sxs-lookup"><span data-stu-id="d4ba0-210">Autoscale history</span></span>
<span data-ttu-id="d4ba0-211">Hello exemple suivant vous montre comment vous pouvez afficher les événements de mise à l’échelle et alerte récents.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-211">hello following example shows you how you can view recent autoscale and alert events.</span></span> <span data-ttu-id="d4ba0-212">Utilisez hello journal recherche tooview hello échelle historique de l’activité.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-212">Use hello activity log search tooview hello autoscale history.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="d4ba0-213">Vous pouvez utiliser hello `Get-AzureRmAutoScaleHistory` tooretrieve de l’applet de commande l’historique de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-213">You can use hello `Get-AzureRmAutoScaleHistory` cmdlet tooretrieve AutoScale history.</span></span>

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

<span data-ttu-id="d4ba0-214">Pour plus d’informations, voir [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4ba0-214">For more information, see [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span></span>

### <a name="view-details-for-an-autoscale-setting"></a><span data-ttu-id="d4ba0-215">Afficher les détails d'un paramètre de mise à l'échelle automatique</span><span class="sxs-lookup"><span data-stu-id="d4ba0-215">View details for an autoscale setting</span></span>
<span data-ttu-id="d4ba0-216">Vous pouvez utiliser hello `Get-Autoscalesetting` tooretrieve de l’applet de commande plus d’informations sur la configuration de mise à l’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-216">You can use hello `Get-Autoscalesetting` cmdlet tooretrieve more information about hello autoscale setting.</span></span>

<span data-ttu-id="d4ba0-217">Hello exemple suivant donne des détails sur tous les paramètres de mise à l’échelle dans le groupe de ressources hello 'myrg1'.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-217">hello following example shows details about all autoscale settings in hello resource group 'myrg1'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="d4ba0-218">Bonjour exemple suivant affiche les détails de tous les paramètres de mise à l’échelle dans le groupe de ressources hello 'myrg1' et spécifiquement hello nommé 'MyScaleVMSSSetting' de paramètre de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-218">hello following example shows details about all autoscale settings in hello resource group 'myrg1' and specifically hello autoscale setting named 'MyScaleVMSSSetting'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a><span data-ttu-id="d4ba0-219">Supprimer un paramètre de mise à l'échelle automatique</span><span class="sxs-lookup"><span data-stu-id="d4ba0-219">Remove an autoscale setting</span></span>
<span data-ttu-id="d4ba0-220">Vous pouvez utiliser hello `Remove-Autoscalesetting` toodelete de l’applet de commande un paramètre de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-220">You can use hello `Remove-Autoscalesetting` cmdlet toodelete an autoscale setting.</span></span>

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a><span data-ttu-id="d4ba0-221">Gérer les profils de journal pour le journal d’activité</span><span class="sxs-lookup"><span data-stu-id="d4ba0-221">Manage log profiles for activity log</span></span>
<span data-ttu-id="d4ba0-222">Vous pouvez créer un *connecter profil* et exporter des données à partir de votre compte de stockage tooa journal des activités et vous peuvent configurer la rétention des données pour qu’il.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-222">You can create a *log profile* and export data from your activity log tooa storage account and you can configure data retention for it.</span></span> <span data-ttu-id="d4ba0-223">Si vous le souhaitez, vous pouvez également transmettre en continu hello données tooyour concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-223">Optionally, you can also stream hello data tooyour Event Hub.</span></span> <span data-ttu-id="d4ba0-224">Notez que cette fonctionnalité est actuellement en version préliminaire et vous ne pouvez créer qu'un seul profil de journal par abonnement.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-224">Note that this feature is currently in Preview and you can only create one log profile per subscription.</span></span> <span data-ttu-id="d4ba0-225">Vous pouvez utiliser hello suivant d’applets de commande avec votre toocreate d’abonnement en cours et gérer les profils de journal.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-225">You can use hello following cmdlets with your current subscription toocreate and manage log profiles.</span></span> <span data-ttu-id="d4ba0-226">Vous pouvez également choisir un abonnement spécifique.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-226">You can also choose a particular subscription.</span></span> <span data-ttu-id="d4ba0-227">Bien que PowerShell par défaut toohello abonnement, vous pouvez toujours modifier que l’utilisation `Set-AzureRmContext`.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-227">Although PowerShell defaults toohello current subscription, you can always change that using `Set-AzureRmContext`.</span></span> <span data-ttu-id="d4ba0-228">Vous pouvez configurer le compte de stockage d’activité journal tooroute données tooany ou concentrateur d’événements au sein de cet abonnement.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-228">You can configure activity log tooroute data tooany storage account or Event Hub within that subscription.</span></span> <span data-ttu-id="d4ba0-229">Les données sont écrites en tant que fichiers blob au format JSON.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-229">Data is written as blob files in JSON format.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="d4ba0-230">Obtenir un profil de journal</span><span class="sxs-lookup"><span data-stu-id="d4ba0-230">Get a log profile</span></span>
<span data-ttu-id="d4ba0-231">toofetch vos profils journal existant, utilisez hello `Get-AzureRmLogProfile` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-231">toofetch your existing log profiles, use hello `Get-AzureRmLogProfile` cmdlet.</span></span>

### <a name="add-a-log-profile-without-data-retention"></a><span data-ttu-id="d4ba0-232">Ajouter un profil de journal sans conservation des données</span><span class="sxs-lookup"><span data-stu-id="d4ba0-232">Add a log profile without data retention</span></span>
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="d4ba0-233">Supprimer un profil de journal</span><span class="sxs-lookup"><span data-stu-id="d4ba0-233">Remove a log profile</span></span>
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a><span data-ttu-id="d4ba0-234">Ajouter un profil de journal avec conservation des données</span><span class="sxs-lookup"><span data-stu-id="d4ba0-234">Add a log profile with data retention</span></span>
<span data-ttu-id="d4ba0-235">Vous pouvez spécifier hello **- RetentionInDays** propriété hello nombre de jours, comme un entier positif, où les données de salutation sont conservées.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-235">You can specify hello **-RetentionInDays** property with hello number of days, as a positive integer, where hello data is retained.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="d4ba0-236">Ajouter un profil de journal avec conservation des données et hub d'événements</span><span class="sxs-lookup"><span data-stu-id="d4ba0-236">Add log profile with retention and EventHub</span></span>
<span data-ttu-id="d4ba0-237">Dans Ajout toorouting votre compte toostorage de données, vous pouvez également diffuser en continu tooan concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-237">In addition toorouting your data toostorage account, you can also stream it tooan Event Hub.</span></span> <span data-ttu-id="d4ba0-238">Notez que dans cette version préliminaire release et hello configuration de compte de stockage est obligatoire mais configuration du Hub d’événements est facultative.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-238">Note that in this preview release and hello storage account configuration is mandatory but Event Hub configuration is optional.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a><span data-ttu-id="d4ba0-239">Configuration des journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="d4ba0-239">Configure diagnostics logs</span></span>
<span data-ttu-id="d4ba0-240">Plusieurs services Azure fournissent des journaux supplémentaires et télémétrie qui peut être des données toosave configuré dans votre compte Azure Storage, envoyer tooEvent concentrateurs et/ou envoyés d’espace de travail Analytique des journaux OMS tooan.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-240">Many Azure services provide additional logs and telemetry that can be configured toosave data in your Azure Storage account, send tooEvent Hubs, and/or sent tooan OMS Log Analytics workspace.</span></span> <span data-ttu-id="d4ba0-241">Cette opération ne peut être effectuée qu’à un niveau de la ressource et le concentrateur de compte ou l’événement de stockage hello doit être présent dans hello même région en tant que ressource de hello cible où hello diagnostics est défini.</span><span class="sxs-lookup"><span data-stu-id="d4ba0-241">That operation can only be performed at a resource level and hello storage account or event hub should be present in hello same region as hello target resource where hello diagnostics setting is configured.</span></span>

### <a name="get-diagnostic-setting"></a><span data-ttu-id="d4ba0-242">Obtenir le paramètre de diagnostic</span><span class="sxs-lookup"><span data-stu-id="d4ba0-242">Get diagnostic setting</span></span>
```PowerShell
Get-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp
```

<span data-ttu-id="d4ba0-243">Désactiver le paramètre de diagnostic</span><span class="sxs-lookup"><span data-stu-id="d4ba0-243">Disable diagnostic setting</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $false
```

<span data-ttu-id="d4ba0-244">Activer le paramètre de diagnostic sans conservation</span><span class="sxs-lookup"><span data-stu-id="d4ba0-244">Enable diagnostic setting without retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true
```

<span data-ttu-id="d4ba0-245">Activer le paramètre de diagnostic avec conservation</span><span class="sxs-lookup"><span data-stu-id="d4ba0-245">Enable diagnostic setting with retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="d4ba0-246">Activer un paramètre diagnostic avec conservation pour une catégorie de journal spécifique</span><span class="sxs-lookup"><span data-stu-id="d4ba0-246">Enable diagnostic setting with retention for a specific log category</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/sakteststorage -Categories NetworkSecurityGroupEvent -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="d4ba0-247">Activer le paramètre de diagnostic pour Event Hubs</span><span class="sxs-lookup"><span data-stu-id="d4ba0-247">Enable diagnostic setting for Event Hubs</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Enable $true
```

<span data-ttu-id="d4ba0-248">Activer le paramètre de diagnostic pour OMS</span><span class="sxs-lookup"><span data-stu-id="d4ba0-248">Enable diagnostic setting for OMS</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -WorkspaceId 76d785fd-d1ce-4f50-8ca3-858fc819ca0f -Enabled $true

```
