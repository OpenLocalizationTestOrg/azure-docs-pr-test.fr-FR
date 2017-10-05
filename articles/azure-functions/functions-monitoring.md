---
title: Test des fonctions Azure | Microsoft Docs
description: "Découvrez comment surveiller vos fonctions Azure."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, webhooks, calcul dynamique, architecture sans serveur"
ms.assetid: 501722c3-f2f7-4224-a220-6d59da08a320
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/03/2016
ms.author: wesmc
ms.openlocfilehash: b70214593b1417265387f42306a633bb0df2920e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="monitoring-azure-functions"></a><span data-ttu-id="6fa0a-104">Surveillance d’Azure Functions</span><span class="sxs-lookup"><span data-stu-id="6fa0a-104">Monitoring Azure Functions</span></span>

## <a name="overview"></a><span data-ttu-id="6fa0a-105">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="6fa0a-105">Overview</span></span> 


<span data-ttu-id="6fa0a-106">L’onglet **Surveiller** pour chaque fonction vous permet de vérifier chaque exécution d’une fonction.</span><span class="sxs-lookup"><span data-stu-id="6fa0a-106">The **Monitor** tab for each function allows you to review each execution of a function.</span></span>

![Onglet Surveiller d’Azure Functions](./media/functions-monitoring/monitor-tab.png) 

<span data-ttu-id="6fa0a-108">Cliquer sur une exécution vous permet de consulter la durée, les données d’entrée, les erreurs et les fichiers journaux associés.</span><span class="sxs-lookup"><span data-stu-id="6fa0a-108">Clicking an execution allows you to review the duration, input data, errors, and associated log files.</span></span> <span data-ttu-id="6fa0a-109">Cela est utile pour le débogage et l’optimisation de vos fonctions.</span><span class="sxs-lookup"><span data-stu-id="6fa0a-109">This is useful debugging and performance tuning your functions.</span></span>


> [!IMPORTANT]
> <span data-ttu-id="6fa0a-110">Lorsque vous utilisez le [plan de consommation d’hébergement](functions-overview.md#pricing) pour Azure Functions, la vignette **Surveillance** dans le panneau de vue d’ensemble de Function App n’affiche pas toutes les données.</span><span class="sxs-lookup"><span data-stu-id="6fa0a-110">When using the [Consumption hosting plan](functions-overview.md#pricing) for Azure Functions, the **Monitoring** tile in the Function App overview blade will not show any data.</span></span> <span data-ttu-id="6fa0a-111">Cela est dû au fait que la plateforme met à l’échelle et gère automatiquement les instances de calcul pour vous. Ces mesures ne sont donc pas pertinentes pour un plan de consommation.</span><span class="sxs-lookup"><span data-stu-id="6fa0a-111">This is because the platform dynamically scales and manages compute instances for you, so these metrics are not meaningful on a Consumption plan.</span></span> <span data-ttu-id="6fa0a-112">Pour surveiller l’utilisation de vos Function Apps, utilisez plutôt les instructions de cet article.</span><span class="sxs-lookup"><span data-stu-id="6fa0a-112">To monitor the usage of your Function Apps, you should instead use the guidance in this article.</span></span>
> 
> <span data-ttu-id="6fa0a-113">La capture d’écran suivante présente un exemple :</span><span class="sxs-lookup"><span data-stu-id="6fa0a-113">The following screen-shot shows an example:</span></span>
> 
> ![Surveillance dans le panneau principal de la ressource](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a><span data-ttu-id="6fa0a-115">Surveillance en temps réel</span><span class="sxs-lookup"><span data-stu-id="6fa0a-115">Real-time monitoring</span></span>

<span data-ttu-id="6fa0a-116">L’analyse en temps réel est disponible en cliquant sur **flux d’événements en direct**, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6fa0a-116">Real-time monitoring is available by clicking **live event stream** as shown below.</span></span> 

![Option de flux d’événement en direct pour l’onglet Surveiller](./media/functions-monitoring/monitor-tab-live-event-stream.png)

<span data-ttu-id="6fa0a-118">Le flux d’événements en direct est représenté graphiquement dans un nouvel onglet de navigateur, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6fa0a-118">The live event stream will be graphed in a new browser tab as shown below.</span></span> 

![Exemple de flux de données d’événement en direct](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> <span data-ttu-id="6fa0a-120">Il existe un problème connu qui peut provoquer l’échec du remplissage de vos données.</span><span class="sxs-lookup"><span data-stu-id="6fa0a-120">There is a known issue that may cause your data to fail to be populated.</span></span> <span data-ttu-id="6fa0a-121">Si c’est le cas, vous devrez peut-être fermer l’onglet du navigateur contenant le flux d’événements en direct, puis cliquer à nouveau sur **flux d’événements en direct** pour lui permettre de remplir correctement vos données de flux de données d’événement.</span><span class="sxs-lookup"><span data-stu-id="6fa0a-121">If you experience this, you may need to close the browser tab containing the live event stream and then click **live event stream** again to allow it to properly populate your event stream data.</span></span> 

<span data-ttu-id="6fa0a-122">Le flux d’événements en direct représentera graphiquement les statistiques suivantes de votre fonction :</span><span class="sxs-lookup"><span data-stu-id="6fa0a-122">The live event stream will graph the following statistics for your function:</span></span>

* <span data-ttu-id="6fa0a-123">Exécutions démarrées par seconde</span><span class="sxs-lookup"><span data-stu-id="6fa0a-123">Executions started per second</span></span>
* <span data-ttu-id="6fa0a-124">Exécutions réussies par seconde</span><span class="sxs-lookup"><span data-stu-id="6fa0a-124">Executions completed per second</span></span>
* <span data-ttu-id="6fa0a-125">Exécutions ayant échoué par seconde</span><span class="sxs-lookup"><span data-stu-id="6fa0a-125">Executions failed per second</span></span>
* <span data-ttu-id="6fa0a-126">Temps d’exécution moyen en millisecondes.</span><span class="sxs-lookup"><span data-stu-id="6fa0a-126">Average execution time in milliseconds.</span></span>

<span data-ttu-id="6fa0a-127">Ces statistiques sont en temps réel, mais les graphiques réels des données d’exécution peuvent avoir une latence d’environ 10 secondes.</span><span class="sxs-lookup"><span data-stu-id="6fa0a-127">These statistics are real-time but the actual graphing of the execution data may have around 10 seconds of latency.</span></span>






## <a name="monitoring-log-files-from-a-command-line"></a><span data-ttu-id="6fa0a-128">Analyse des fichiers journaux à partir d’une ligne de commande</span><span class="sxs-lookup"><span data-stu-id="6fa0a-128">Monitoring log files from a command line</span></span>


<span data-ttu-id="6fa0a-129">Vous pouvez diffuser des fichiers journaux vers une session de ligne de commande sur une station de travail à l’aide de l’Interface de ligne de commande Azure (CLI) ou PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6fa0a-129">You can stream log files to a command line session on a local workstation using the Azure Command Line Interface (CLI) or PowerShell.</span></span>

### <a name="monitoring-function-app-log-files-with-the-azure-cli"></a><span data-ttu-id="6fa0a-130">Analyse des fichiers journaux Function App avec l’interface CLI Azure</span><span class="sxs-lookup"><span data-stu-id="6fa0a-130">Monitoring function app log files with the Azure CLI</span></span>

<span data-ttu-id="6fa0a-131">Pour commencer, [installez l’interface de ligne de commande Azure](../cli-install-nodejs.md)</span><span class="sxs-lookup"><span data-stu-id="6fa0a-131">To get started, [install the Azure CLI](../cli-install-nodejs.md)</span></span>

<span data-ttu-id="6fa0a-132">Connectez-vous à votre compte Azure à l’aide de la commande suivante, ou n’importe quelle autre des options couvertes dans [Connexion à Azure à partir de l’interface de ligne de commande (CLI) Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="6fa0a-132">Log into your Azure account using the following command, or any of the other options covered in, [Log in to Azure from the Azure CLI](../xplat-cli-connect.md).</span></span>

    azure login

<span data-ttu-id="6fa0a-133">Utilisez la commande suivante pour activer les commandes Azure CLI en mode Service Management (ASM) :.</span><span class="sxs-lookup"><span data-stu-id="6fa0a-133">Use the following command to enable Azure CLI Service Management (ASM) mode:.</span></span>

    azure config mode asm

<span data-ttu-id="6fa0a-134">Si vous avez plusieurs abonnements, utilisez les commandes suivantes pour les répertorier et définir l’abonnement qui contient votre Function App comme abonnement actif.</span><span class="sxs-lookup"><span data-stu-id="6fa0a-134">If you have multiple subscriptions, use the following commands to list your subscriptions and set the current subscription to the subscription that contains your function app.</span></span>

    azure account list
    azure account set <subscriptionNameOrId>

<span data-ttu-id="6fa0a-135">La commande suivante diffusera les fichiers journaux de votre Function App vers la ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="6fa0a-135">The following command will stream the log files of your function app to the command line:</span></span>

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a><span data-ttu-id="6fa0a-136">Analyse des fichiers journaux Function App avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="6fa0a-136">Monitoring function app log files with PowerShell</span></span>

<span data-ttu-id="6fa0a-137">Pour commencer, [installez et configurez Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6fa0a-137">To get started, [install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="6fa0a-138">Ajoutez votre compte Azure en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6fa0a-138">Add your Azure account by running the following command:</span></span>

    PS C:\> Add-AzureAccount

<span data-ttu-id="6fa0a-139">Si vous avez plusieurs abonnements, vous pouvez les répertorier par nom avec la commande suivante pour voir si l’abonnement approprié est sélectionné selon la propriété `IsCurrent` :</span><span class="sxs-lookup"><span data-stu-id="6fa0a-139">If you have multiple subscriptions, you can list them by name with the following command to see if the correct subscription is the currently selected based on `IsCurrent` property:</span></span>

    PS C:\> Get-AzureSubscription

<span data-ttu-id="6fa0a-140">Si vous avez besoin de définir l’abonnement actif sur celui qui contient votre Function App, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6fa0a-140">If you need to set the active subscription to the one containing your function app, use the following command:</span></span>

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

<span data-ttu-id="6fa0a-141">Diffusez les journaux vers votre session PowerShell avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6fa0a-141">Stream the logs to your PowerShell session with the following command:</span></span>

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

<span data-ttu-id="6fa0a-142">Pour plus d’informations, reportez-vous à [Procédure : diffusion de journaux pour les applications web](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span><span class="sxs-lookup"><span data-stu-id="6fa0a-142">For more information refer to [How to: Stream logs for web apps](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6fa0a-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6fa0a-143">Next steps</span></span>
<span data-ttu-id="6fa0a-144">Pour plus d’informations, consultez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="6fa0a-144">For more information, see the following resources:</span></span>

* [<span data-ttu-id="6fa0a-145">Test d’une fonction</span><span class="sxs-lookup"><span data-stu-id="6fa0a-145">Testing a function</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="6fa0a-146">Mettre à l’échelle une fonction</span><span class="sxs-lookup"><span data-stu-id="6fa0a-146">Scale a function</span></span>](functions-scale.md)

