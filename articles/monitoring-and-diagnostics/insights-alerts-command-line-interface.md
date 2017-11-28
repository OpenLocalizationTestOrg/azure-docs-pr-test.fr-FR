---
title: "Créer des alertes pour les services Azure - Interface de ligne de commande multiplateforme | Microsoft Docs"
description: "Déclenchez des e-mails et des notifications, appelez des URL de sites web (webhooks) ou déclenchez une automatisation lorsque les conditions spécifiées sont remplies."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 5c6a2d27-7dcc-4f89-8752-9bb31b05ff35
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: robb
ms.openlocfilehash: 92246a8da73a244a1c9a924bed55711d71a20fd8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---cross-platform-cli"></a><span data-ttu-id="1786a-103">Créer des alertes de métrique dans Azure Monitor pour les services Azure - Interface CLI multiplateforme</span><span class="sxs-lookup"><span data-stu-id="1786a-103">Create metric alerts in Azure Monitor for Azure services - Cross-platform CLI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1786a-104">Portail</span><span class="sxs-lookup"><span data-stu-id="1786a-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="1786a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1786a-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="1786a-106">INTERFACE DE LIGNE DE COMMANDE</span><span class="sxs-lookup"><span data-stu-id="1786a-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="1786a-107">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="1786a-107">Overview</span></span>
<span data-ttu-id="1786a-108">Cet article montre comment configurer des alertes de métrique Azure avec l’interface de ligne de commande (CLI) multiplateforme.</span><span class="sxs-lookup"><span data-stu-id="1786a-108">This article shows you how to set up Azure metric alerts using the cross-platform Command Line Interface (CLI).</span></span>

> [!NOTE]
> <span data-ttu-id="1786a-109">Azure Monitor est le nouveau nom de ce qui était appelé « Azure Insights » jusqu’au 25 septembre 2016.</span><span class="sxs-lookup"><span data-stu-id="1786a-109">Azure Monitor is the new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="1786a-110">Toutefois, les espaces de noms et, par conséquent, les commandes ci-dessous contiennent toujours « insights ».</span><span class="sxs-lookup"><span data-stu-id="1786a-110">However, the namespaces and thus the commands below still contain the "insights".</span></span>
>
>

<span data-ttu-id="1786a-111">Vous pouvez recevoir une alerte en fonction de métriques de surveillance pour vos services Azure ou d'événements sur ces derniers.</span><span class="sxs-lookup"><span data-stu-id="1786a-111">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="1786a-112">**Valeurs de métriques** : l’alerte se déclenche lorsque la valeur d’une métrique spécifiée dépasse un seuil que vous affectez dans un des deux sens.</span><span class="sxs-lookup"><span data-stu-id="1786a-112">**Metric values** - The alert triggers when the value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="1786a-113">C’est-à-dire que le déclenchement se fait à la fois lorsque la condition est remplie et par la suite une fois que la condition n’est plus remplie.</span><span class="sxs-lookup"><span data-stu-id="1786a-113">That is, it triggers both when the condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="1786a-114">**Événements du journal d’activité** : une alerte peut se déclencher sur *chaque* événement ou seulement quand un certain événement se produit.</span><span class="sxs-lookup"><span data-stu-id="1786a-114">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="1786a-115">Pour plus d’informations sur les alertes du journal d’activité, [cliquez ici](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="1786a-115">To learn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="1786a-116">Vous pouvez configurer une alerte de métrique pour effectuer les opérations suivantes lors de son déclenchement :</span><span class="sxs-lookup"><span data-stu-id="1786a-116">You can configure a metric alert to do the following when it triggers:</span></span>

* <span data-ttu-id="1786a-117">envoyer des notifications par courrier électronique à l’administrateur du service et aux coadministrateurs</span><span class="sxs-lookup"><span data-stu-id="1786a-117">send email notifications to the service administrator and co-administrators</span></span>
* <span data-ttu-id="1786a-118">envoyer un courrier électronique à d’autres adresses que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="1786a-118">send email to additional emails that you specify.</span></span>
* <span data-ttu-id="1786a-119">appeler un webhook</span><span class="sxs-lookup"><span data-stu-id="1786a-119">call a webhook</span></span>
* <span data-ttu-id="1786a-120">démarrer l’exécution d’un runbook Azure (uniquement à partir du Portail Azure pour l’instant)</span><span class="sxs-lookup"><span data-stu-id="1786a-120">start execution of an Azure runbook (only from the Azure portal at this time)</span></span>

<span data-ttu-id="1786a-121">Vous pouvez configurer et obtenir des informations sur les règles d’alerte de métrique via</span><span class="sxs-lookup"><span data-stu-id="1786a-121">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="1786a-122">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="1786a-122">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="1786a-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1786a-123">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="1786a-124">interface de ligne de commande (CLI)</span><span class="sxs-lookup"><span data-stu-id="1786a-124">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="1786a-125">API REST Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="1786a-125">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="1786a-126">Vous pouvez toujours obtenir une aide sur les commandes en tapant une commande et en ajoutant -help à la fin.</span><span class="sxs-lookup"><span data-stu-id="1786a-126">You can always receive help for commands by typing a command and putting -help at the end.</span></span> <span data-ttu-id="1786a-127">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="1786a-127">For example:</span></span>

    ```console
    azure insights alerts -help
    azure insights alerts actions email create -help
    ```

## <a name="create-alert-rules-using-the-cli"></a><span data-ttu-id="1786a-128">Créer des règles d’alerte à l’aide de l’interface CLI</span><span class="sxs-lookup"><span data-stu-id="1786a-128">Create alert rules using the CLI</span></span>
1. <span data-ttu-id="1786a-129">Suivez les conditions préalables et connectez-vous à Azure.</span><span class="sxs-lookup"><span data-stu-id="1786a-129">Perform the Prerequisites and login to Azure.</span></span> <span data-ttu-id="1786a-130">Consultez les [exemples d’interface de ligne de commande Azure Monitor](insights-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1786a-130">See [Azure Monitor CLI samples](insights-cli-samples.md).</span></span> <span data-ttu-id="1786a-131">En bref, installez l’interface CLI et exécutez ces commandes.</span><span class="sxs-lookup"><span data-stu-id="1786a-131">In short, install the CLI and run these commands.</span></span> <span data-ttu-id="1786a-132">Elles vous connectent, indiquent quel abonnement que vous utilisez et préparent l’exécution des commandes Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="1786a-132">They get you logged in, show what subscription you are using, and prepare you to run Azure Monitor commands.</span></span>

    ```console
    azure login
    azure account show
    azure config mode arm

    ```

2. <span data-ttu-id="1786a-133">Pour répertorier les règles existantes dans un groupe de ressources, utilisez le format suivant **azure insights alerts rule list** *[options] &lt;resourceGroup&gt;*</span><span class="sxs-lookup"><span data-stu-id="1786a-133">To list existing rules on a resource group, use the following form **azure insights alerts rule list** *[options] &lt;resourceGroup&gt;*</span></span>

   ```console
   azure insights alerts rule list myresourcegroupname

   ```
3. <span data-ttu-id="1786a-134">Pour créer une règle, vous avez d’abord besoin de différentes informations importantes.</span><span class="sxs-lookup"><span data-stu-id="1786a-134">To create a rule, you need to have several important pieces of information first.</span></span>
  * <span data-ttu-id="1786a-135">**L’ID de la ressource** pour laquelle vous souhaitez définir une alerte</span><span class="sxs-lookup"><span data-stu-id="1786a-135">The **Resource ID** for the resource you want to set an alert for</span></span>
  * <span data-ttu-id="1786a-136">Les **définitions de métriques** disponibles pour cette ressource</span><span class="sxs-lookup"><span data-stu-id="1786a-136">The **metric definitions** available for that resource</span></span>

     <span data-ttu-id="1786a-137">Pour obtenir l’ID de la ressource, vous pouvez utiliser le Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1786a-137">One way to get the Resource ID is to use the Azure portal.</span></span> <span data-ttu-id="1786a-138">À supposer que la ressource soit déjà créée, sélectionnez-la dans le portail.</span><span class="sxs-lookup"><span data-stu-id="1786a-138">Assuming the resource is already created, select it in the portal.</span></span> <span data-ttu-id="1786a-139">Puis, dans le panneau suivant, sélectionnez *Propriétés* sous la section *Paramètres*.</span><span class="sxs-lookup"><span data-stu-id="1786a-139">Then in the next blade, select *Properties* under the *Settings* section.</span></span> <span data-ttu-id="1786a-140">*L’ID DE RESSOURCE* est un champ du panneau suivant.</span><span class="sxs-lookup"><span data-stu-id="1786a-140">The *RESOURCE ID* is a field in the next blade.</span></span> <span data-ttu-id="1786a-141">Une autre méthode consiste à utiliser [l’Explorateur de ressources Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1786a-141">Another way is to use the [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="1786a-142">Voici un exemple d’ID de ressource d’une application web</span><span class="sxs-lookup"><span data-stu-id="1786a-142">An example resource id for a web app is</span></span>

     ```console
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="1786a-143">Pour obtenir la liste des métriques disponibles et de leurs unités pour l’exemple de ressource précédent, utilisez la commande CLI suivante :</span><span class="sxs-lookup"><span data-stu-id="1786a-143">To get a list of the available metrics and units for those metrics for the previous resource example, use the following CLI command:</span></span>  

     ```console
     azure insights metrics list /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename PT1M
     ```

     <span data-ttu-id="1786a-144">*PT1M* est la précision de la mesure disponible (intervalles d’une minute).</span><span class="sxs-lookup"><span data-stu-id="1786a-144">*PT1M* is the granularity of the available measurement (1-minute intervals).</span></span> <span data-ttu-id="1786a-145">L’utilisation de différentes précisions vous offre différentes options de métriques.</span><span class="sxs-lookup"><span data-stu-id="1786a-145">Using different granularities gives you different metric options.</span></span>
4. <span data-ttu-id="1786a-146">Pour créer une règle d’alerte basée sur une métrique, utilisez une commande de la forme suivante :</span><span class="sxs-lookup"><span data-stu-id="1786a-146">To create a metric-based alert rule, use a command of the following form:</span></span>

    <span data-ttu-id="1786a-147">**azure insights alerts rule metric set** *[options] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span><span class="sxs-lookup"><span data-stu-id="1786a-147">**azure insights alerts rule metric set** *[options] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span></span>

    <span data-ttu-id="1786a-148">L’exemple suivant configure une alerte sur une ressource de site web.</span><span class="sxs-lookup"><span data-stu-id="1786a-148">The following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="1786a-149">L’alerte se déclenche chaque fois qu’il reçoit constamment du trafic pendant cinq minutes, et à nouveau lorsqu’il ne reçoit aucun trafic pendant cinq minutes.</span><span class="sxs-lookup"><span data-stu-id="1786a-149">The alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```console
    azure insights alerts rule metric set myrule eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total

    ```
5. <span data-ttu-id="1786a-150">Pour créer un webhook ou envoyer un e-mail quand une alerte se déclenche, commencez par créer l’e-mail et/ou les webhooks.</span><span class="sxs-lookup"><span data-stu-id="1786a-150">To create webhook or send email when a metric alert fires, first create the email and/or webhooks.</span></span> <span data-ttu-id="1786a-151">Puis créez la règle immédiatement après.</span><span class="sxs-lookup"><span data-stu-id="1786a-151">Then create the rule immediately afterwards.</span></span> <span data-ttu-id="1786a-152">Vous ne pouvez pas associer un webhook ou des messages électroniques à des règles déjà créées à l’aide de l’interface CLI.</span><span class="sxs-lookup"><span data-stu-id="1786a-152">You cannot associate webhook or emails with already created rules using the CLI.</span></span>

    ```console
    azure insights alerts actions email create --customEmails myemail@contoso.com

    azure insights alerts actions webhook create https://www.contoso.com

    azure insights alerts rule metric set myrulewithwebhookandemail eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total
    ```

6. <span data-ttu-id="1786a-153">Vous pouvez vérifier que vos alertes ont été correctement créées en examinant une règle en particulier.</span><span class="sxs-lookup"><span data-stu-id="1786a-153">You can verify that your alerts have been created properly by looking at an individual rule.</span></span>

    ```console
    azure insights alerts rule list myresourcegroup --ruleName myrule
    ```
7. <span data-ttu-id="1786a-154">Pour supprimer des règles, utilisez une commande de la forme :</span><span class="sxs-lookup"><span data-stu-id="1786a-154">To delete rules, use a command of the form:</span></span>

    <span data-ttu-id="1786a-155">**insights alerts rule delete** [options] &lt;resourceGroup&gt; &lt;ruleName&gt;</span><span class="sxs-lookup"><span data-stu-id="1786a-155">**insights alerts rule delete** [options] &lt;resourceGroup&gt; &lt;ruleName&gt;</span></span>

    <span data-ttu-id="1786a-156">Ces commandes suppriment les règles créées précédemment dans cet article.</span><span class="sxs-lookup"><span data-stu-id="1786a-156">These commands delete the rules previously created in this article.</span></span>

    ```console
    azure insights alerts rule delete myresourcegroup myrule
    azure insights alerts rule delete myresourcegroup myrulewithwebhookandemail
    azure insights alerts rule delete myresourcegroup myActivityLogRule
    ```

## <a name="next-steps"></a><span data-ttu-id="1786a-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1786a-157">Next steps</span></span>
* <span data-ttu-id="1786a-158">[Consultez une vue d’ensemble de la surveillance Azure](monitoring-overview.md) , notamment les types d’informations que vous pouvez collecter et surveiller.</span><span class="sxs-lookup"><span data-stu-id="1786a-158">[Get an overview of Azure monitoring](monitoring-overview.md) including the types of information you can collect and monitor.</span></span>
* <span data-ttu-id="1786a-159">Découvrez plus en détail la [configuration des webhooks dans les alertes](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="1786a-159">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="1786a-160">Découvrez plus d’informations sur la [configuration des alertes sur les événements de journal d’activité](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="1786a-160">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="1786a-161">Découvrez plus en détails les [runbooks Azure Automation](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="1786a-161">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="1786a-162">Consultez une [vue d’ensemble de la collecte des journaux de diagnostic](monitoring-overview-of-diagnostic-logs.md) pour collecter des métriques détaillées à fréquence élevée sur votre service.</span><span class="sxs-lookup"><span data-stu-id="1786a-162">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) to collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="1786a-163">Consultez une [vue d’ensemble de la collecte des métriques](insights-how-to-customize-monitoring.md) pour vous assurer que votre service est disponible et réactif.</span><span class="sxs-lookup"><span data-stu-id="1786a-163">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
