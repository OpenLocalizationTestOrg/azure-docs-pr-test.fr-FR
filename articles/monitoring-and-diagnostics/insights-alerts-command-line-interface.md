---
title: les alertes pour les services Azure - inter-plateformes CLI aaaCreate | Documents Microsoft
description: "Déclencher des messages électroniques, les notifications, les URL de sites Web d’appel (webhooks) ou automation lorsque les conditions hello spécifiées sont remplies."
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
ms.openlocfilehash: e53701e5377a415038a69fbd32f1e5fc5fe99be9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---cross-platform-cli"></a><span data-ttu-id="f698d-103">Créer des alertes de métrique dans Azure Monitor pour les services Azure - Interface CLI multiplateforme</span><span class="sxs-lookup"><span data-stu-id="f698d-103">Create metric alerts in Azure Monitor for Azure services - Cross-platform CLI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f698d-104">Portail</span><span class="sxs-lookup"><span data-stu-id="f698d-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="f698d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f698d-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="f698d-106">INTERFACE DE LIGNE DE COMMANDE</span><span class="sxs-lookup"><span data-stu-id="f698d-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="f698d-107">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="f698d-107">Overview</span></span>
<span data-ttu-id="f698d-108">Cet article vous explique comment tooset des alertes de métrique Azure à l’aide de hello inter-plateformes Interface de ligne de commande (CLI).</span><span class="sxs-lookup"><span data-stu-id="f698d-108">This article shows you how tooset up Azure metric alerts using hello cross-platform Command Line Interface (CLI).</span></span>

> [!NOTE]
> <span data-ttu-id="f698d-109">Moniteur de Azure est hello nouveau nom pour ce qui a été appelé « Azure Insights » jusqu'à 25 septembre 2016.</span><span class="sxs-lookup"><span data-stu-id="f698d-109">Azure Monitor is hello new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="f698d-110">Toutefois, les espaces de noms hello et, par conséquent, les commandes hello ci-dessous encore contient insights » l’hello ».</span><span class="sxs-lookup"><span data-stu-id="f698d-110">However, hello namespaces and thus hello commands below still contain hello "insights".</span></span>
>
>

<span data-ttu-id="f698d-111">Vous pouvez recevoir une alerte en fonction de métriques de surveillance pour vos services Azure ou d'événements sur ces derniers.</span><span class="sxs-lookup"><span data-stu-id="f698d-111">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="f698d-112">**Valeurs de mesure** - hello déclencheurs d’alerte lorsque la valeur de hello d’une métrique spécifique dépasse un seuil que vous affectez dans les deux sens.</span><span class="sxs-lookup"><span data-stu-id="f698d-112">**Metric values** - hello alert triggers when hello value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="f698d-113">Autrement dit, elle déclenche à la fois lorsque hello condition est tout d’abord remplie et puis par la suite que lorsque la condition est n’est plus remplie.</span><span class="sxs-lookup"><span data-stu-id="f698d-113">That is, it triggers both when hello condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="f698d-114">**Événements du journal d’activité** : une alerte peut se déclencher sur *chaque* événement ou seulement quand un certain événement se produit.</span><span class="sxs-lookup"><span data-stu-id="f698d-114">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="f698d-115">toolearn plus d’informations sur les alertes de journal d’activité [cliquez ici](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="f698d-115">toolearn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="f698d-116">Vous pouvez configurer un hello métrique toodo alerte suivant lorsqu’il déclenche :</span><span class="sxs-lookup"><span data-stu-id="f698d-116">You can configure a metric alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="f698d-117">envoyer l’administrateur de service de messagerie des notifications toohello et coadministrateurs</span><span class="sxs-lookup"><span data-stu-id="f698d-117">send email notifications toohello service administrator and co-administrators</span></span>
* <span data-ttu-id="f698d-118">envoyer des e-mails tooadditional que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="f698d-118">send email tooadditional emails that you specify.</span></span>
* <span data-ttu-id="f698d-119">appeler un webhook</span><span class="sxs-lookup"><span data-stu-id="f698d-119">call a webhook</span></span>
* <span data-ttu-id="f698d-120">Démarrer l’exécution d’un runbook Azure (uniquement à partir de hello portail Azure pour l’instant)</span><span class="sxs-lookup"><span data-stu-id="f698d-120">start execution of an Azure runbook (only from hello Azure portal at this time)</span></span>

<span data-ttu-id="f698d-121">Vous pouvez configurer et obtenir des informations sur les règles d’alerte de métrique via</span><span class="sxs-lookup"><span data-stu-id="f698d-121">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="f698d-122">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="f698d-122">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="f698d-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f698d-123">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="f698d-124">interface de ligne de commande (CLI)</span><span class="sxs-lookup"><span data-stu-id="f698d-124">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="f698d-125">API REST Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="f698d-125">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="f698d-126">Vous pouvez toujours recevoir aide pour les commandes en tapant une commande et la mise - aide à la fin de hello.</span><span class="sxs-lookup"><span data-stu-id="f698d-126">You can always receive help for commands by typing a command and putting -help at hello end.</span></span> <span data-ttu-id="f698d-127">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="f698d-127">For example:</span></span>

    ```console
    azure insights alerts -help
    azure insights alerts actions email create -help
    ```

## <a name="create-alert-rules-using-hello-cli"></a><span data-ttu-id="f698d-128">Créer des règles d’alerte à l’aide de hello CLI</span><span class="sxs-lookup"><span data-stu-id="f698d-128">Create alert rules using hello CLI</span></span>
1. <span data-ttu-id="f698d-129">Effectuer des conditions préalables de hello et tooAzure de connexion.</span><span class="sxs-lookup"><span data-stu-id="f698d-129">Perform hello Prerequisites and login tooAzure.</span></span> <span data-ttu-id="f698d-130">Consultez les [exemples d’interface de ligne de commande Azure Monitor](insights-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f698d-130">See [Azure Monitor CLI samples](insights-cli-samples.md).</span></span> <span data-ttu-id="f698d-131">En bref, installez hello CLI et exécutez les commandes.</span><span class="sxs-lookup"><span data-stu-id="f698d-131">In short, install hello CLI and run these commands.</span></span> <span data-ttu-id="f698d-132">Ils vous aider à connecté, afficher les abonnements que vous utilisez et vous toorun Azure analyse les commandes prepare.</span><span class="sxs-lookup"><span data-stu-id="f698d-132">They get you logged in, show what subscription you are using, and prepare you toorun Azure Monitor commands.</span></span>

    ```console
    azure login
    azure account show
    azure config mode arm

    ```

2. <span data-ttu-id="f698d-133">les règles existantes toolist sur un groupe de ressources, utiliser hello suivant du formulaire **azure insights alertes règle liste** *[options] &lt;le groupe de ressources&gt;*</span><span class="sxs-lookup"><span data-stu-id="f698d-133">toolist existing rules on a resource group, use hello following form **azure insights alerts rule list** *[options] &lt;resourceGroup&gt;*</span></span>

   ```console
   azure insights alerts rule list myresourcegroupname

   ```
3. <span data-ttu-id="f698d-134">toocreate une règle, vous avez besoin de toohave plusieurs informations importantes tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="f698d-134">toocreate a rule, you need toohave several important pieces of information first.</span></span>
  * <span data-ttu-id="f698d-135">Hello **ID de ressource** pour la ressource de hello souhaité tooset une alerte pour</span><span class="sxs-lookup"><span data-stu-id="f698d-135">hello **Resource ID** for hello resource you want tooset an alert for</span></span>
  * <span data-ttu-id="f698d-136">Hello **définitions de métrique** disponibles pour cette ressource</span><span class="sxs-lookup"><span data-stu-id="f698d-136">hello **metric definitions** available for that resource</span></span>

     <span data-ttu-id="f698d-137">Une façon tooget hello ID de ressource est toouse hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f698d-137">One way tooget hello Resource ID is toouse hello Azure portal.</span></span> <span data-ttu-id="f698d-138">En supposant que la ressource de hello a déjà été créé, sélectionnez-le dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="f698d-138">Assuming hello resource is already created, select it in hello portal.</span></span> <span data-ttu-id="f698d-139">Puis, dans le panneau suivant de hello, sélectionnez *propriétés* sous hello *paramètres* section.</span><span class="sxs-lookup"><span data-stu-id="f698d-139">Then in hello next blade, select *Properties* under hello *Settings* section.</span></span> <span data-ttu-id="f698d-140">Hello *ID de ressource* est un champ dans le panneau suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="f698d-140">hello *RESOURCE ID* is a field in hello next blade.</span></span> <span data-ttu-id="f698d-141">Une autre méthode consiste à toouse hello [Explorateur de ressources Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f698d-141">Another way is toouse hello [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="f698d-142">Voici un exemple d’ID de ressource d’une application web</span><span class="sxs-lookup"><span data-stu-id="f698d-142">An example resource id for a web app is</span></span>

     ```console
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="f698d-143">tooget une liste de métriques disponibles de hello et les unités de ces métriques pour le précédent exemple de ressource hello, hello utilisez CLI commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f698d-143">tooget a list of hello available metrics and units for those metrics for hello previous resource example, use hello following CLI command:</span></span>  

     ```console
     azure insights metrics list /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename PT1M
     ```

     <span data-ttu-id="f698d-144">*PT1M* est granularité hello de mesure de hello disponible (intervalles de 1 minute).</span><span class="sxs-lookup"><span data-stu-id="f698d-144">*PT1M* is hello granularity of hello available measurement (1-minute intervals).</span></span> <span data-ttu-id="f698d-145">L’utilisation de différentes précisions vous offre différentes options de métriques.</span><span class="sxs-lookup"><span data-stu-id="f698d-145">Using different granularities gives you different metric options.</span></span>
4. <span data-ttu-id="f698d-146">toocreate une règle d’alerte basée sur une mesure, utilisez une commande de hello suivant du formulaire :</span><span class="sxs-lookup"><span data-stu-id="f698d-146">toocreate a metric-based alert rule, use a command of hello following form:</span></span>

    <span data-ttu-id="f698d-147">**azure insights alerts rule metric set***[options] &lt;ruleName&gt;&lt;location&gt;&lt;resourceGroup&gt;&lt;windowSize&gt;&lt;operator&gt;&lt;threshold&gt;&lt;targetResourceId&gt;&lt;metricName&gt;&lt;timeAggregationOperator&gt;*</span><span class="sxs-lookup"><span data-stu-id="f698d-147">**azure insights alerts rule metric set** *[options] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span></span>

    <span data-ttu-id="f698d-148">Hello suivant exemple configure une alerte sur une ressource de site web.</span><span class="sxs-lookup"><span data-stu-id="f698d-148">hello following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="f698d-149">Hello alerte se déclenche chaque fois qu’il reçoit toujours tout le trafic de 5 minutes, et à nouveau lorsqu’elle ne reçoit aucun trafic pendant 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="f698d-149">hello alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```console
    azure insights alerts rule metric set myrule eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total

    ```
5. <span data-ttu-id="f698d-150">toocreate webhook ou envoyer par courrier électronique lors du déclenche d’une alerte de métriques, créez d’abord par courrier électronique hello et/ou le webhooks.</span><span class="sxs-lookup"><span data-stu-id="f698d-150">toocreate webhook or send email when a metric alert fires, first create hello email and/or webhooks.</span></span> <span data-ttu-id="f698d-151">Puis créer règle de hello immédiatement par la suite.</span><span class="sxs-lookup"><span data-stu-id="f698d-151">Then create hello rule immediately afterwards.</span></span> <span data-ttu-id="f698d-152">Vous ne pouvez pas associer webhook ou des messages électroniques avec déjà créé des règles à l’aide de hello CLI.</span><span class="sxs-lookup"><span data-stu-id="f698d-152">You cannot associate webhook or emails with already created rules using hello CLI.</span></span>

    ```console
    azure insights alerts actions email create --customEmails myemail@contoso.com

    azure insights alerts actions webhook create https://www.contoso.com

    azure insights alerts rule metric set myrulewithwebhookandemail eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total
    ```

6. <span data-ttu-id="f698d-153">Vous pouvez vérifier que vos alertes ont été correctement créées en examinant une règle en particulier.</span><span class="sxs-lookup"><span data-stu-id="f698d-153">You can verify that your alerts have been created properly by looking at an individual rule.</span></span>

    ```console
    azure insights alerts rule list myresourcegroup --ruleName myrule
    ```
7. <span data-ttu-id="f698d-154">règles de toodelete, utilisez une commande sous forme de hello :</span><span class="sxs-lookup"><span data-stu-id="f698d-154">toodelete rules, use a command of hello form:</span></span>

    <span data-ttu-id="f698d-155">**insights alerts rule delete** [options] &lt;resourceGroup&gt;&lt;ruleName&gt;</span><span class="sxs-lookup"><span data-stu-id="f698d-155">**insights alerts rule delete** [options] &lt;resourceGroup&gt; &lt;ruleName&gt;</span></span>

    <span data-ttu-id="f698d-156">Ces commandes suppriment les règles hello créés précédemment dans cet article.</span><span class="sxs-lookup"><span data-stu-id="f698d-156">These commands delete hello rules previously created in this article.</span></span>

    ```console
    azure insights alerts rule delete myresourcegroup myrule
    azure insights alerts rule delete myresourcegroup myrulewithwebhookandemail
    azure insights alerts rule delete myresourcegroup myActivityLogRule
    ```

## <a name="next-steps"></a><span data-ttu-id="f698d-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f698d-157">Next steps</span></span>
* <span data-ttu-id="f698d-158">[Obtenir une vue d’ensemble de la surveillance Azure](monitoring-overview.md) y compris les types d’informations, vous pouvez collecter et analyser hello.</span><span class="sxs-lookup"><span data-stu-id="f698d-158">[Get an overview of Azure monitoring](monitoring-overview.md) including hello types of information you can collect and monitor.</span></span>
* <span data-ttu-id="f698d-159">Découvrez plus en détail la [configuration des webhooks dans les alertes](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="f698d-159">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="f698d-160">Découvrez plus d’informations sur la [configuration des alertes sur les événements de journal d’activité](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="f698d-160">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="f698d-161">Découvrez plus en détails les [runbooks Azure Automation](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="f698d-161">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="f698d-162">Obtenir un [vue d’ensemble de la collecte des journaux de diagnostic](monitoring-overview-of-diagnostic-logs.md) toocollect détaillée des métriques de haute fréquence sur votre service.</span><span class="sxs-lookup"><span data-stu-id="f698d-162">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) toocollect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="f698d-163">Obtenir un [vue d’ensemble de la collecte de métriques](insights-how-to-customize-monitoring.md) toomake que votre service est disponible et réactive.</span><span class="sxs-lookup"><span data-stu-id="f698d-163">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
