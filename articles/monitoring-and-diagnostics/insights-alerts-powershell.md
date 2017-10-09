---
title: aaaCreate des alertes pour les services Azure - PowerShell | Documents Microsoft
description: "Déclencher des messages électroniques, les notifications, les URL de sites Web d’appel (webhooks) ou automation lorsque les conditions hello spécifiées sont remplies."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d26ab15b-7b7e-42a9-81c8-3ce9ead5d252
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/20/2016
ms.author: robb
ms.openlocfilehash: 80d3a3f194fc6a5a09a81d04206ea7a1640bddb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---powershell"></a><span data-ttu-id="6dfe9-103">Création d’alertes de métrique dans Azure Monitor pour les services Azure - PowerShell</span><span class="sxs-lookup"><span data-stu-id="6dfe9-103">Create metric alerts in Azure Monitor for Azure services - PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6dfe9-104">Portail</span><span class="sxs-lookup"><span data-stu-id="6dfe9-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="6dfe9-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6dfe9-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="6dfe9-106">INTERFACE DE LIGNE DE COMMANDE</span><span class="sxs-lookup"><span data-stu-id="6dfe9-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="6dfe9-107">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="6dfe9-107">Overview</span></span>
<span data-ttu-id="6dfe9-108">Cet article vous explique comment tooset haut Azure mesure les alertes à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6dfe9-108">This article shows you how tooset up Azure metric alerts using PowerShell.</span></span>  

<span data-ttu-id="6dfe9-109">Vous pouvez recevoir une alerte en fonction de métriques de surveillance pour vos services Azure ou d'événements sur ces derniers.</span><span class="sxs-lookup"><span data-stu-id="6dfe9-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="6dfe9-110">**Valeurs de mesure** - hello déclencheurs d’alerte lorsque la valeur de hello d’une métrique spécifique dépasse un seuil que vous affectez dans les deux sens.</span><span class="sxs-lookup"><span data-stu-id="6dfe9-110">**Metric values** - hello alert triggers when hello value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="6dfe9-111">Autrement dit, elle déclenche à la fois lorsque hello condition est tout d’abord remplie et puis par la suite que lorsque la condition est n’est plus remplie.</span><span class="sxs-lookup"><span data-stu-id="6dfe9-111">That is, it triggers both when hello condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="6dfe9-112">**Événements du journal d’activité** : une alerte peut se déclencher sur *chaque* événement ou seulement quand un certain événement se produit.</span><span class="sxs-lookup"><span data-stu-id="6dfe9-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="6dfe9-113">toolearn plus d’informations sur les alertes de journal d’activité [cliquez ici](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="6dfe9-113">toolearn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="6dfe9-114">Vous pouvez configurer un hello métrique toodo alerte suivant lorsqu’il déclenche :</span><span class="sxs-lookup"><span data-stu-id="6dfe9-114">You can configure a metric alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="6dfe9-115">envoyer l’administrateur de service de messagerie des notifications toohello et coadministrateurs</span><span class="sxs-lookup"><span data-stu-id="6dfe9-115">send email notifications toohello service administrator and co-administrators</span></span>
* <span data-ttu-id="6dfe9-116">envoyer des e-mails tooadditional que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="6dfe9-116">send email tooadditional emails that you specify.</span></span>
* <span data-ttu-id="6dfe9-117">appeler un webhook</span><span class="sxs-lookup"><span data-stu-id="6dfe9-117">call a webhook</span></span>
* <span data-ttu-id="6dfe9-118">Démarrer l’exécution d’un runbook Azure (uniquement à partir de hello portail Azure)</span><span class="sxs-lookup"><span data-stu-id="6dfe9-118">start execution of an Azure runbook (only from hello Azure portal)</span></span>

<span data-ttu-id="6dfe9-119">Vous pouvez configurer et obtenir des informations sur les règles d’alerte avec</span><span class="sxs-lookup"><span data-stu-id="6dfe9-119">You can configure and get information about alert rules using</span></span>

* [<span data-ttu-id="6dfe9-120">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="6dfe9-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="6dfe9-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6dfe9-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="6dfe9-122">interface de ligne de commande (CLI)</span><span class="sxs-lookup"><span data-stu-id="6dfe9-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="6dfe9-123">API REST Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="6dfe9-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="6dfe9-124">Pour plus d’informations, vous pouvez toujours taper ```Get-Help``` et puis hello commande PowerShell que vous voulez de l’aide.</span><span class="sxs-lookup"><span data-stu-id="6dfe9-124">For additional information, you can always type ```Get-Help``` and then hello PowerShell command you want help on.</span></span>

## <a name="create-alert-rules-in-powershell"></a><span data-ttu-id="6dfe9-125">Créer des règles d’alerte dans PowerShell</span><span class="sxs-lookup"><span data-stu-id="6dfe9-125">Create alert rules in PowerShell</span></span>
1. <span data-ttu-id="6dfe9-126">Ouvrez une session dans tooAzure.</span><span class="sxs-lookup"><span data-stu-id="6dfe9-126">Log in tooAzure.</span></span>   

    ```PowerShell
    Login-AzureRmAccount

    ```
2. <span data-ttu-id="6dfe9-127">Obtenir la liste des abonnements de hello vous disposez.</span><span class="sxs-lookup"><span data-stu-id="6dfe9-127">Get a list of hello subscriptions you have available.</span></span> <span data-ttu-id="6dfe9-128">Vérifiez que vous travaillez avec abonnement hello.</span><span class="sxs-lookup"><span data-stu-id="6dfe9-128">Verify that you are working with hello right subscription.</span></span> <span data-ttu-id="6dfe9-129">Dans le cas contraire, définissez-le toohello droite à l’aide de la sortie de hello de `Get-AzureRmSubscription`.</span><span class="sxs-lookup"><span data-stu-id="6dfe9-129">If not, set it toohello right one using hello output from `Get-AzureRmSubscription`.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    Get-AzureRmContext
    Set-AzureRmContext -SubscriptionId <subscriptionid>
    ```
3. <span data-ttu-id="6dfe9-130">les règles existantes toolist sur un groupe de ressources, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6dfe9-130">toolist existing rules on a resource group, use hello following command:</span></span>

   ```PowerShell
   Get-AzureRmAlertRule -ResourceGroup <myresourcegroup> -DetailedOutput
   ```
4. <span data-ttu-id="6dfe9-131">toocreate une règle, vous avez besoin de toohave plusieurs informations importantes tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="6dfe9-131">toocreate a rule, you need toohave several important pieces of information first.</span></span>

  * <span data-ttu-id="6dfe9-132">Hello **ID de ressource** pour la ressource de hello souhaité tooset une alerte pour</span><span class="sxs-lookup"><span data-stu-id="6dfe9-132">hello **Resource ID** for hello resource you want tooset an alert for</span></span>
  * <span data-ttu-id="6dfe9-133">Hello **définitions de métrique** disponibles pour cette ressource</span><span class="sxs-lookup"><span data-stu-id="6dfe9-133">hello **metric definitions** available for that resource</span></span>

     <span data-ttu-id="6dfe9-134">Une façon tooget hello ID de ressource est toouse hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6dfe9-134">One way tooget hello Resource ID is toouse hello Azure portal.</span></span> <span data-ttu-id="6dfe9-135">En supposant que la ressource de hello a déjà été créé, sélectionnez-le dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="6dfe9-135">Assuming hello resource is already created, select it in hello portal.</span></span> <span data-ttu-id="6dfe9-136">Puis, dans le panneau suivant de hello, sélectionnez *propriétés* sous hello *paramètres* section.</span><span class="sxs-lookup"><span data-stu-id="6dfe9-136">Then in hello next blade, select *Properties* under hello *Settings* section.</span></span> <span data-ttu-id="6dfe9-137">**ID de ressource** est un champ dans le panneau suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="6dfe9-137">**RESOURCE ID** is a field in hello next blade.</span></span> <span data-ttu-id="6dfe9-138">Une autre méthode consiste à toouse hello [Explorateur de ressources Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6dfe9-138">Another way is toouse hello [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="6dfe9-139">Voici un exemple d’ID de ressource d’une application web</span><span class="sxs-lookup"><span data-stu-id="6dfe9-139">An example Resource ID for a web app is</span></span>

     ```
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="6dfe9-140">Vous pouvez utiliser `Get-AzureRmMetricDefinition` liste de hello tooview de toutes les définitions de métrique pour une ressource spécifique.</span><span class="sxs-lookup"><span data-stu-id="6dfe9-140">You can use `Get-AzureRmMetricDefinition` tooview hello list of all metric definitions for a specific resource.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id>
     ```

     <span data-ttu-id="6dfe9-141">Hello exemple suivant génère une table avec mesure de hello nom et le hello unité pour cette métrique.</span><span class="sxs-lookup"><span data-stu-id="6dfe9-141">hello following example generates a table with hello metric Name and hello Unit for that metric.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit

     ```
     <span data-ttu-id="6dfe9-142">La liste complète des options disponibles pour Get-AzureRmMetricDefinition s’obtient en exécutant la commande Get-MetricDefinitions.</span><span class="sxs-lookup"><span data-stu-id="6dfe9-142">A full list of available options for Get-AzureRmMetricDefinition is available by running Get-MetricDefinitions.</span></span>
5. <span data-ttu-id="6dfe9-143">Hello suivant exemple configure une alerte sur une ressource de site web.</span><span class="sxs-lookup"><span data-stu-id="6dfe9-143">hello following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="6dfe9-144">Hello alerte se déclenche chaque fois qu’il reçoit toujours tout le trafic de 5 minutes, et à nouveau lorsqu’elle ne reçoit aucun trafic pendant 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="6dfe9-144">hello alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```PowerShell
    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Description "alert on any website activity"

    ```
6. <span data-ttu-id="6dfe9-145">toocreate webhook ou envoyer par courrier électronique lorsqu’une alerte se déclenche, créez d’abord par courrier électronique hello et/ou le webhooks.</span><span class="sxs-lookup"><span data-stu-id="6dfe9-145">toocreate webhook or send email when an alert triggers, first create hello email and/or webhooks.</span></span> <span data-ttu-id="6dfe9-146">Créer immédiatement les règle hello par la suite avec hello - balise Actions et comme indiqué dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="6dfe9-146">Then immediately create hello rule afterwards with hello -Actions tag and as shown in hello following example.</span></span> <span data-ttu-id="6dfe9-147">Vous ne pouvez pas associer un webhook ou des messages électroniques à des règles déjà créées à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6dfe9-147">You cannot associate webhook or emails with already created rules via PowerShell.</span></span>

    ```PowerShell
    $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
    $actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://www.contoso.com?token=mytoken

    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Actions $actionEmail, $actionWebhook -Description "alert on any website activity"
    ```

7. <span data-ttu-id="6dfe9-148">tooverify que vos alertes ont été créés correctement en examinant les règles individuelles hello.</span><span class="sxs-lookup"><span data-stu-id="6dfe9-148">tooverify that your alerts have been created properly by looking at hello individual rules.</span></span>

    ```PowerShell
    Get-AzureRmAlertRule -Name myMetricRuleWithWebhookAndEmail -ResourceGroup myresourcegroup -DetailedOutput

    Get-AzureRmAlertRule -Name myLogAlertRule -ResourceGroup myresourcegroup -DetailedOutput
    ```
8. <span data-ttu-id="6dfe9-149">Supprimez vos alertes.</span><span class="sxs-lookup"><span data-stu-id="6dfe9-149">Delete your alerts.</span></span> <span data-ttu-id="6dfe9-150">Ces commandes suppriment les règles hello créés précédemment dans cet article.</span><span class="sxs-lookup"><span data-stu-id="6dfe9-150">These commands delete hello rules created previously in this article.</span></span>

    ```PowerShell
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myrule
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myMetricRuleWithWebhookAndEmail
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myLogAlertRule
    ```

## <a name="next-steps"></a><span data-ttu-id="6dfe9-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6dfe9-151">Next steps</span></span>
* <span data-ttu-id="6dfe9-152">[Obtenir une vue d’ensemble de la surveillance Azure](monitoring-overview.md) y compris les types d’informations, vous pouvez collecter et analyser hello.</span><span class="sxs-lookup"><span data-stu-id="6dfe9-152">[Get an overview of Azure monitoring](monitoring-overview.md) including hello types of information you can collect and monitor.</span></span>
* <span data-ttu-id="6dfe9-153">Découvrez plus en détail la [configuration des webhooks dans les alertes](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="6dfe9-153">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="6dfe9-154">Découvrez plus d’informations sur la [configuration des alertes sur les événements de journal d’activité](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="6dfe9-154">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="6dfe9-155">Découvrez plus en détails les [runbooks Azure Automation](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="6dfe9-155">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="6dfe9-156">Obtenir un [vue d’ensemble de la collecte des journaux de diagnostic](monitoring-overview-of-diagnostic-logs.md) toocollect détaillée des métriques de haute fréquence sur votre service.</span><span class="sxs-lookup"><span data-stu-id="6dfe9-156">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) toocollect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="6dfe9-157">Obtenir un [vue d’ensemble de la collecte de métriques](insights-how-to-customize-monitoring.md) toomake que votre service est disponible et réactive.</span><span class="sxs-lookup"><span data-stu-id="6dfe9-157">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
