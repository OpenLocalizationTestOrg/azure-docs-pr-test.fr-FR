---
title: "Créer des alertes pour les services Azure - PowerShell | Microsoft Docs"
description: "Déclenchez des e-mails et des notifications, appelez des URL de sites web (webhooks) ou déclenchez une automatisation lorsque les conditions spécifiées sont remplies."
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
ms.openlocfilehash: 50127242cdf156771d0610e58cf2fc41281adae7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---powershell"></a><span data-ttu-id="7505d-103">Création d’alertes de métrique dans Azure Monitor pour les services Azure - PowerShell</span><span class="sxs-lookup"><span data-stu-id="7505d-103">Create metric alerts in Azure Monitor for Azure services - PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7505d-104">Portail</span><span class="sxs-lookup"><span data-stu-id="7505d-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="7505d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7505d-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="7505d-106">INTERFACE DE LIGNE DE COMMANDE</span><span class="sxs-lookup"><span data-stu-id="7505d-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="7505d-107">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="7505d-107">Overview</span></span>
<span data-ttu-id="7505d-108">Cet article vous montre comment configurer des alertes de métrique Azure avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7505d-108">This article shows you how to set up Azure metric alerts using PowerShell.</span></span>  

<span data-ttu-id="7505d-109">Vous pouvez recevoir une alerte en fonction de métriques de surveillance pour vos services Azure ou d'événements sur ces derniers.</span><span class="sxs-lookup"><span data-stu-id="7505d-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="7505d-110">**Valeurs de métriques** : l’alerte se déclenche lorsque la valeur d’une métrique spécifiée dépasse un seuil que vous affectez dans un des deux sens.</span><span class="sxs-lookup"><span data-stu-id="7505d-110">**Metric values** - The alert triggers when the value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="7505d-111">C’est-à-dire que le déclenchement se fait à la fois lorsque la condition est remplie et par la suite une fois que la condition n’est plus remplie.</span><span class="sxs-lookup"><span data-stu-id="7505d-111">That is, it triggers both when the condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="7505d-112">**Événements du journal d’activité** : une alerte peut se déclencher sur *chaque* événement ou seulement quand un certain événement se produit.</span><span class="sxs-lookup"><span data-stu-id="7505d-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="7505d-113">Pour plus d’informations sur les alertes du journal d’activité, [cliquez ici](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="7505d-113">To learn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="7505d-114">Vous pouvez configurer une alerte de métrique pour effectuer les opérations suivantes lors de son déclenchement :</span><span class="sxs-lookup"><span data-stu-id="7505d-114">You can configure a metric alert to do the following when it triggers:</span></span>

* <span data-ttu-id="7505d-115">envoyer des notifications par courrier électronique à l’administrateur du service et aux coadministrateurs</span><span class="sxs-lookup"><span data-stu-id="7505d-115">send email notifications to the service administrator and co-administrators</span></span>
* <span data-ttu-id="7505d-116">envoyer un courrier électronique à d’autres adresses que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="7505d-116">send email to additional emails that you specify.</span></span>
* <span data-ttu-id="7505d-117">appeler un webhook</span><span class="sxs-lookup"><span data-stu-id="7505d-117">call a webhook</span></span>
* <span data-ttu-id="7505d-118">démarrer l’exécution d’un runbook Azure (uniquement à partir du Portail Azure)</span><span class="sxs-lookup"><span data-stu-id="7505d-118">start execution of an Azure runbook (only from the Azure portal)</span></span>

<span data-ttu-id="7505d-119">Vous pouvez configurer et obtenir des informations sur les règles d’alerte avec</span><span class="sxs-lookup"><span data-stu-id="7505d-119">You can configure and get information about alert rules using</span></span>

* [<span data-ttu-id="7505d-120">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="7505d-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="7505d-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7505d-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="7505d-122">interface de ligne de commande (CLI)</span><span class="sxs-lookup"><span data-stu-id="7505d-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="7505d-123">API REST Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="7505d-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="7505d-124">Pour obtenir des informations complémentaires, vous pouvez à tout moment taper ```Get-Help``` , suivi de la commande PowerShell sur laquelle vous souhaitez de l’aide.</span><span class="sxs-lookup"><span data-stu-id="7505d-124">For additional information, you can always type ```Get-Help``` and then the PowerShell command you want help on.</span></span>

## <a name="create-alert-rules-in-powershell"></a><span data-ttu-id="7505d-125">Créer des règles d’alerte dans PowerShell</span><span class="sxs-lookup"><span data-stu-id="7505d-125">Create alert rules in PowerShell</span></span>
1. <span data-ttu-id="7505d-126">Connectez-vous à Azure.</span><span class="sxs-lookup"><span data-stu-id="7505d-126">Log in to Azure.</span></span>   

    ```PowerShell
    Login-AzureRmAccount

    ```
2. <span data-ttu-id="7505d-127">Récupérez la liste des abonnements dont vous disposez.</span><span class="sxs-lookup"><span data-stu-id="7505d-127">Get a list of the subscriptions you have available.</span></span> <span data-ttu-id="7505d-128">Vérifiez que vous travaillez avec le bon abonnement.</span><span class="sxs-lookup"><span data-stu-id="7505d-128">Verify that you are working with the right subscription.</span></span> <span data-ttu-id="7505d-129">Dans le cas contraire, choisissez le bon à l’aide de la sortie de `Get-AzureRmSubscription`.</span><span class="sxs-lookup"><span data-stu-id="7505d-129">If not, set it to the right one using the output from `Get-AzureRmSubscription`.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    Get-AzureRmContext
    Set-AzureRmContext -SubscriptionId <subscriptionid>
    ```
3. <span data-ttu-id="7505d-130">Pour répertorier les règles existantes sur un groupe de ressources, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7505d-130">To list existing rules on a resource group, use the following command:</span></span>

   ```PowerShell
   Get-AzureRmAlertRule -ResourceGroup <myresourcegroup> -DetailedOutput
   ```
4. <span data-ttu-id="7505d-131">Pour créer une règle, vous avez d’abord besoin de différentes informations importantes.</span><span class="sxs-lookup"><span data-stu-id="7505d-131">To create a rule, you need to have several important pieces of information first.</span></span>

  * <span data-ttu-id="7505d-132">**L’ID de la ressource** pour laquelle vous souhaitez définir une alerte</span><span class="sxs-lookup"><span data-stu-id="7505d-132">The **Resource ID** for the resource you want to set an alert for</span></span>
  * <span data-ttu-id="7505d-133">Les **définitions de métriques** disponibles pour cette ressource</span><span class="sxs-lookup"><span data-stu-id="7505d-133">The **metric definitions** available for that resource</span></span>

     <span data-ttu-id="7505d-134">Pour obtenir l’ID de la ressource, vous pouvez utiliser le Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7505d-134">One way to get the Resource ID is to use the Azure portal.</span></span> <span data-ttu-id="7505d-135">À supposer que la ressource soit déjà créée, sélectionnez-la dans le portail.</span><span class="sxs-lookup"><span data-stu-id="7505d-135">Assuming the resource is already created, select it in the portal.</span></span> <span data-ttu-id="7505d-136">Puis, dans le panneau suivant, sélectionnez *Propriétés* sous la section *Paramètres*.</span><span class="sxs-lookup"><span data-stu-id="7505d-136">Then in the next blade, select *Properties* under the *Settings* section.</span></span> <span data-ttu-id="7505d-137">**ID DE RESSOURCE** est un champ du panneau suivant.</span><span class="sxs-lookup"><span data-stu-id="7505d-137">**RESOURCE ID** is a field in the next blade.</span></span> <span data-ttu-id="7505d-138">Une autre méthode consiste à utiliser [l’Explorateur de ressources Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7505d-138">Another way is to use the [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="7505d-139">Voici un exemple d’ID de ressource d’une application web</span><span class="sxs-lookup"><span data-stu-id="7505d-139">An example Resource ID for a web app is</span></span>

     ```
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="7505d-140">Vous pouvez utiliser `Get-AzureRmMetricDefinition` pour afficher la liste de toutes les définitions de métriques d’une ressource spécifique.</span><span class="sxs-lookup"><span data-stu-id="7505d-140">You can use `Get-AzureRmMetricDefinition` to view the list of all metric definitions for a specific resource.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id>
     ```

     <span data-ttu-id="7505d-141">L’exemple suivant génère une table avec le nom de la métrique et son unité.</span><span class="sxs-lookup"><span data-stu-id="7505d-141">The following example generates a table with the metric Name and the Unit for that metric.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit

     ```
     <span data-ttu-id="7505d-142">La liste complète des options disponibles pour Get-AzureRmMetricDefinition s’obtient en exécutant la commande Get-MetricDefinitions.</span><span class="sxs-lookup"><span data-stu-id="7505d-142">A full list of available options for Get-AzureRmMetricDefinition is available by running Get-MetricDefinitions.</span></span>
5. <span data-ttu-id="7505d-143">L’exemple suivant configure une alerte sur une ressource de site web.</span><span class="sxs-lookup"><span data-stu-id="7505d-143">The following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="7505d-144">L’alerte se déclenche chaque fois qu’il reçoit constamment du trafic pendant cinq minutes, et à nouveau lorsqu’il ne reçoit aucun trafic pendant cinq minutes.</span><span class="sxs-lookup"><span data-stu-id="7505d-144">The alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```PowerShell
    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Description "alert on any website activity"

    ```
6. <span data-ttu-id="7505d-145">Pour créer un webhook ou envoyer un courrier électronique lorsqu’une alerte se déclenche, commencez par créer le message et/ou les webhooks.</span><span class="sxs-lookup"><span data-stu-id="7505d-145">To create webhook or send email when an alert triggers, first create the email and/or webhooks.</span></span> <span data-ttu-id="7505d-146">Puis créez la règle immédiatement après avec la balise -Actions, comme l’indique l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="7505d-146">Then immediately create the rule afterwards with the -Actions tag and as shown in the following example.</span></span> <span data-ttu-id="7505d-147">Vous ne pouvez pas associer un webhook ou des messages électroniques à des règles déjà créées à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7505d-147">You cannot associate webhook or emails with already created rules via PowerShell.</span></span>

    ```PowerShell
    $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
    $actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://www.contoso.com?token=mytoken

    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Actions $actionEmail, $actionWebhook -Description "alert on any website activity"
    ```

7. <span data-ttu-id="7505d-148">Pour vérifier que vos alertes ont été correctement créées en examinant les règles individuelles.</span><span class="sxs-lookup"><span data-stu-id="7505d-148">To verify that your alerts have been created properly by looking at the individual rules.</span></span>

    ```PowerShell
    Get-AzureRmAlertRule -Name myMetricRuleWithWebhookAndEmail -ResourceGroup myresourcegroup -DetailedOutput

    Get-AzureRmAlertRule -Name myLogAlertRule -ResourceGroup myresourcegroup -DetailedOutput
    ```
8. <span data-ttu-id="7505d-149">Supprimez vos alertes.</span><span class="sxs-lookup"><span data-stu-id="7505d-149">Delete your alerts.</span></span> <span data-ttu-id="7505d-150">Ces commandes suppriment les règles créées précédemment dans cet article.</span><span class="sxs-lookup"><span data-stu-id="7505d-150">These commands delete the rules created previously in this article.</span></span>

    ```PowerShell
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myrule
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myMetricRuleWithWebhookAndEmail
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myLogAlertRule
    ```

## <a name="next-steps"></a><span data-ttu-id="7505d-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7505d-151">Next steps</span></span>
* <span data-ttu-id="7505d-152">[Consultez une vue d’ensemble de la surveillance Azure](monitoring-overview.md) , notamment les types d’informations que vous pouvez collecter et surveiller.</span><span class="sxs-lookup"><span data-stu-id="7505d-152">[Get an overview of Azure monitoring](monitoring-overview.md) including the types of information you can collect and monitor.</span></span>
* <span data-ttu-id="7505d-153">Découvrez plus en détail la [configuration des webhooks dans les alertes](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="7505d-153">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="7505d-154">Découvrez plus d’informations sur la [configuration des alertes sur les événements de journal d’activité](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="7505d-154">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="7505d-155">Découvrez plus en détails les [runbooks Azure Automation](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="7505d-155">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="7505d-156">Consultez une [vue d’ensemble de la collecte des journaux de diagnostic](monitoring-overview-of-diagnostic-logs.md) pour collecter des métriques détaillées à fréquence élevée sur votre service.</span><span class="sxs-lookup"><span data-stu-id="7505d-156">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) to collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="7505d-157">Consultez une [vue d’ensemble de la collecte des métriques](insights-how-to-customize-monitoring.md) pour vous assurer que votre service est disponible et réactif.</span><span class="sxs-lookup"><span data-stu-id="7505d-157">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
