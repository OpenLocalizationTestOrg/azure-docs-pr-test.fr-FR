---
title: aaaMonitoring les fonctions Azure | Documents Microsoft
description: "Découvrez comment toomonitor vos fonctions de Azure."
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
ms.openlocfilehash: 254348d1cefce925654bd9532715b6def571e0ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-functions"></a><span data-ttu-id="9e663-104">Surveillance d’Azure Functions</span><span class="sxs-lookup"><span data-stu-id="9e663-104">Monitoring Azure Functions</span></span>

## <a name="overview"></a><span data-ttu-id="9e663-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="9e663-105">Overview</span></span> 


<span data-ttu-id="9e663-106">Hello **moniteur** onglet pour chaque fonction vous permet de tooreview chaque exécution d’une fonction.</span><span class="sxs-lookup"><span data-stu-id="9e663-106">hello **Monitor** tab for each function allows you tooreview each execution of a function.</span></span>

![Onglet Surveiller d’Azure Functions](./media/functions-monitoring/monitor-tab.png) 

<span data-ttu-id="9e663-108">Une exécution permet de durée hello tooreview, les données d’entrée, les erreurs et les fichiers journaux associés.</span><span class="sxs-lookup"><span data-stu-id="9e663-108">Clicking an execution allows you tooreview hello duration, input data, errors, and associated log files.</span></span> <span data-ttu-id="9e663-109">Cela est utile pour le débogage et l’optimisation de vos fonctions.</span><span class="sxs-lookup"><span data-stu-id="9e663-109">This is useful debugging and performance tuning your functions.</span></span>


> [!IMPORTANT]
> <span data-ttu-id="9e663-110">Lorsque vous utilisez hello [consommation plan d’hébergement](functions-overview.md#pricing) pour les fonctions d’Azure, hello **analyse** vignette dans le panneau de vue d’ensemble des applications de la fonction hello n’affiche pas les données.</span><span class="sxs-lookup"><span data-stu-id="9e663-110">When using hello [Consumption hosting plan](functions-overview.md#pricing) for Azure Functions, hello **Monitoring** tile in hello Function App overview blade will not show any data.</span></span> <span data-ttu-id="9e663-111">Il s’agit, car la plate-forme de hello s’adapter dynamiquement et gère les instances de calcul pour vous, ces mesures ne sont pas significatives sur un plan de la consommation.</span><span class="sxs-lookup"><span data-stu-id="9e663-111">This is because hello platform dynamically scales and manages compute instances for you, so these metrics are not meaningful on a Consumption plan.</span></span> <span data-ttu-id="9e663-112">toomonitor hello l’utilisation de vos applications de fonction, vous devez utiliser à la place des conseils de hello dans cet article.</span><span class="sxs-lookup"><span data-stu-id="9e663-112">toomonitor hello usage of your Function Apps, you should instead use hello guidance in this article.</span></span>
> 
> <span data-ttu-id="9e663-113">Hello suivant capture d’écran montre un exemple :</span><span class="sxs-lookup"><span data-stu-id="9e663-113">hello following screen-shot shows an example:</span></span>
> 
> ![La surveillance sur le panneau de ressources principal hello](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a><span data-ttu-id="9e663-115">Surveillance en temps réel</span><span class="sxs-lookup"><span data-stu-id="9e663-115">Real-time monitoring</span></span>

<span data-ttu-id="9e663-116">L’analyse en temps réel est disponible en cliquant sur **flux d’événements en direct**, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="9e663-116">Real-time monitoring is available by clicking **live event stream** as shown below.</span></span> 

![Option de flux d’événements pour l’onglet de surveillance hello de Live](./media/functions-monitoring/monitor-tab-live-event-stream.png)

<span data-ttu-id="9e663-118">flux d’événements en direct de Hello est représentés graphiquement dans un nouvel onglet de navigateur, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="9e663-118">hello live event stream will be graphed in a new browser tab as shown below.</span></span> 

![Exemple de flux de données d’événement en direct](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> <span data-ttu-id="9e663-120">Il existe un problème connu qui peut provoquer votre toobe toofail de données remplie.</span><span class="sxs-lookup"><span data-stu-id="9e663-120">There is a known issue that may cause your data toofail toobe populated.</span></span> <span data-ttu-id="9e663-121">Si vous rencontrez cela, vous devrez peut-être les flux d’événements live tooclose hello navigateur onglet contenant hello, puis cliquez sur **flux d’événements live** tooallow nouveau il tooproperly remplir vos données de flux de données d’événement.</span><span class="sxs-lookup"><span data-stu-id="9e663-121">If you experience this, you may need tooclose hello browser tab containing hello live event stream and then click **live event stream** again tooallow it tooproperly populate your event stream data.</span></span> 

<span data-ttu-id="9e663-122">flux d’événements en direct de Hello sera graphique hello suit les statistiques de votre fonction :</span><span class="sxs-lookup"><span data-stu-id="9e663-122">hello live event stream will graph hello following statistics for your function:</span></span>

* <span data-ttu-id="9e663-123">Exécutions démarrées par seconde</span><span class="sxs-lookup"><span data-stu-id="9e663-123">Executions started per second</span></span>
* <span data-ttu-id="9e663-124">Exécutions réussies par seconde</span><span class="sxs-lookup"><span data-stu-id="9e663-124">Executions completed per second</span></span>
* <span data-ttu-id="9e663-125">Exécutions ayant échoué par seconde</span><span class="sxs-lookup"><span data-stu-id="9e663-125">Executions failed per second</span></span>
* <span data-ttu-id="9e663-126">Temps d’exécution moyen en millisecondes.</span><span class="sxs-lookup"><span data-stu-id="9e663-126">Average execution time in milliseconds.</span></span>

<span data-ttu-id="9e663-127">Ces statistiques sont en temps réel, mais hello réel de graphiques de données de l’exécution de hello peut avoir environ dix secondes de latence.</span><span class="sxs-lookup"><span data-stu-id="9e663-127">These statistics are real-time but hello actual graphing of hello execution data may have around 10 seconds of latency.</span></span>






## <a name="monitoring-log-files-from-a-command-line"></a><span data-ttu-id="9e663-128">Analyse des fichiers journaux à partir d’une ligne de commande</span><span class="sxs-lookup"><span data-stu-id="9e663-128">Monitoring log files from a command line</span></span>


<span data-ttu-id="9e663-129">Vous pouvez diffuser la session de ligne de commande de tooa de fichiers journaux sur une station de travail à l’aide de hello Azure Interface de ligne de commande (CLI) ou PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9e663-129">You can stream log files tooa command line session on a local workstation using hello Azure Command Line Interface (CLI) or PowerShell.</span></span>

### <a name="monitoring-function-app-log-files-with-hello-azure-cli"></a><span data-ttu-id="9e663-130">Analyse des fichiers du journal application fonction hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="9e663-130">Monitoring function app log files with hello Azure CLI</span></span>

<span data-ttu-id="9e663-131">tooget démarré, [installer hello CLI d’Azure](../cli-install-nodejs.md)</span><span class="sxs-lookup"><span data-stu-id="9e663-131">tooget started, [install hello Azure CLI](../cli-install-nodejs.md)</span></span>

<span data-ttu-id="9e663-132">Connectez-vous à votre compte Azure utilisant hello commande ou l’un des hello autres options traitées, [connecter tooAzure de hello CLI d’Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="9e663-132">Log into your Azure account using hello following command, or any of hello other options covered in, [Log in tooAzure from hello Azure CLI](../xplat-cli-connect.md).</span></span>

    azure login

<span data-ttu-id="9e663-133">Mode de gestion de Service Azure CLI (ASM) tooenable de commande de suivante de hello utilisation :.</span><span class="sxs-lookup"><span data-stu-id="9e663-133">Use hello following command tooenable Azure CLI Service Management (ASM) mode:.</span></span>

    azure config mode asm

<span data-ttu-id="9e663-134">Si vous avez plusieurs abonnements, utilisez hello suivant toolist de commandes vos abonnements et le jeu hello abonnement toohello abonnement actuel qui contient votre application de la fonction.</span><span class="sxs-lookup"><span data-stu-id="9e663-134">If you have multiple subscriptions, use hello following commands toolist your subscriptions and set hello current subscription toohello subscription that contains your function app.</span></span>

    azure account list
    azure account set <subscriptionNameOrId>

<span data-ttu-id="9e663-135">Hello commande suivante est diffusés journaux hello de votre ligne de commande toohello fonction application :</span><span class="sxs-lookup"><span data-stu-id="9e663-135">hello following command will stream hello log files of your function app toohello command line:</span></span>

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a><span data-ttu-id="9e663-136">Analyse des fichiers journaux Function App avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e663-136">Monitoring function app log files with PowerShell</span></span>

<span data-ttu-id="9e663-137">tooget démarré, [installer et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9e663-137">tooget started, [install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="9e663-138">Ajoutez votre compte Azure en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9e663-138">Add your Azure account by running hello following command:</span></span>

    PS C:\> Add-AzureAccount

<span data-ttu-id="9e663-139">Si vous avez plusieurs abonnements, vous pouvez les répertorier par nom avec hello suivant commande toosee si hello correct de l’abonnement est hello actuellement sélectionné en fonction de `IsCurrent` propriété :</span><span class="sxs-lookup"><span data-stu-id="9e663-139">If you have multiple subscriptions, you can list them by name with hello following command toosee if hello correct subscription is hello currently selected based on `IsCurrent` property:</span></span>

    PS C:\> Get-AzureSubscription

<span data-ttu-id="9e663-140">Si vous devez tooset hello abonnement actif toohello un contenant votre application de la fonction, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9e663-140">If you need tooset hello active subscription toohello one containing your function app, use hello following command:</span></span>

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

<span data-ttu-id="9e663-141">Session PowerShell flux hello journaux tooyour avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9e663-141">Stream hello logs tooyour PowerShell session with hello following command:</span></span>

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

<span data-ttu-id="9e663-142">Pour plus d’informations, consultez trop[Comment : diffuser des journaux pour les applications web](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span><span class="sxs-lookup"><span data-stu-id="9e663-142">For more information refer too[How to: Stream logs for web apps](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9e663-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9e663-143">Next steps</span></span>
<span data-ttu-id="9e663-144">Pour plus d’informations, consultez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="9e663-144">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="9e663-145">Test d’une fonction</span><span class="sxs-lookup"><span data-stu-id="9e663-145">Testing a function</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="9e663-146">Mettre à l’échelle une fonction</span><span class="sxs-lookup"><span data-stu-id="9e663-146">Scale a function</span></span>](functions-scale.md)

