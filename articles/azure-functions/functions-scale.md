---
title: "Plans Consommation et App Service d’Azure Functions | Microsoft Docs"
description: "Découvrez comment Azure Functions se met à l’échelle pour répondre aux besoins de vos charges de travail liées aux événements."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, webhooks, calcul dynamique, architecture sans serveur"
ms.assetid: 5b63649c-ec7f-4564-b168-e0a74cb7e0f3
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/12/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70e77e09b2e2116153159167af61776398904a3c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-consumption-and-app-service-plans"></a><span data-ttu-id="8984b-104">Plans Consommation et App Service d’Azure Functions</span><span class="sxs-lookup"><span data-stu-id="8984b-104">Azure Functions Consumption and App Service plans</span></span> 

## <a name="introduction"></a><span data-ttu-id="8984b-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="8984b-105">Introduction</span></span>

<span data-ttu-id="8984b-106">Vous pouvez exécuter la solution Azure Functions dans deux modes : le plan Consommation et le plan Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="8984b-106">You can run Azure Functions in two different modes: Consumption plan and Azure App Service plan.</span></span> <span data-ttu-id="8984b-107">Le plan Consommation alloue automatiquement la puissance de calcul pendant l’exécution du code, augmente la taille des instances quand c’est nécessaire pour gérer la charge, puis descend en puissance quand le code n’est pas en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="8984b-107">The Consumption plan automatically allocates compute power when your code is running, scales out as necessary to handle load, and then scales down when code is not running.</span></span> <span data-ttu-id="8984b-108">Vous n’avez donc pas à payer pour des machines virtuelles inactives ni à disposer d’une capacité de réserve à l’avance.</span><span class="sxs-lookup"><span data-stu-id="8984b-108">So, you don't have to pay for idle VMs and don't have to reserve capacity in advance.</span></span> <span data-ttu-id="8984b-109">Cet article est consacré au plan Consommation.</span><span class="sxs-lookup"><span data-stu-id="8984b-109">This article focuses on the Consumption plan.</span></span> <span data-ttu-id="8984b-110">Pour plus d’informations sur le fonctionnement du plan App Service, consultez l’article [Présentation détaillée des plans d’Azure App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8984b-110">For details about how the App Service plan works, see the [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

<span data-ttu-id="8984b-111">Si vous n’êtes pas familiarisé avec Azure Functions, consultez [Vue d’ensemble d’Azure Functions](functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8984b-111">If you aren't familiar with Azure Functions, see the [Azure Functions overview](functions-overview.md).</span></span>

<span data-ttu-id="8984b-112">Quand vous créez une application de fonction, vous devez configurer un plan d’hébergement pour les fonctions que l’application contient.</span><span class="sxs-lookup"><span data-stu-id="8984b-112">When you create a function app, you must configure a hosting plan for functions that the app contains.</span></span> <span data-ttu-id="8984b-113">Dans ces deux modes, une instance de *l’hôte Azure Functions* exécute les fonctions.</span><span class="sxs-lookup"><span data-stu-id="8984b-113">In either mode, an instance of the *Azure Functions host* executes the functions.</span></span> <span data-ttu-id="8984b-114">Le type de plan contrôle :</span><span class="sxs-lookup"><span data-stu-id="8984b-114">The type of plan controls:</span></span>

* <span data-ttu-id="8984b-115">la façon dont les instances d’hôte font l’objet d’une augmentation de taille ;</span><span class="sxs-lookup"><span data-stu-id="8984b-115">How host instances are scaled out.</span></span>
* <span data-ttu-id="8984b-116">les ressources disponibles pour chaque hôte.</span><span class="sxs-lookup"><span data-stu-id="8984b-116">The resources that are available to each host.</span></span>

<span data-ttu-id="8984b-117">Vous devez choisir le type de plan durant la création de l’application de fonction.</span><span class="sxs-lookup"><span data-stu-id="8984b-117">Currently, you must choose the plan type during the creation of the function app.</span></span> <span data-ttu-id="8984b-118">Vous ne pouvez pas en changer ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="8984b-118">You can't change it afterward.</span></span> 

<span data-ttu-id="8984b-119">Vous pouvez faire évoluer le plan App Service entre les différents niveaux.</span><span class="sxs-lookup"><span data-stu-id="8984b-119">You can scale between tiers on the App Service plan.</span></span> <span data-ttu-id="8984b-120">Dans le plan Consommation, Azure Functions gère automatiquement l’allocation de toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="8984b-120">On the Consumption plan, Azure Functions automatically handles all resource allocation.</span></span>

## <a name="consumption-plan"></a><span data-ttu-id="8984b-121">Plan de consommation</span><span class="sxs-lookup"><span data-stu-id="8984b-121">Consumption plan</span></span>

<span data-ttu-id="8984b-122">Quand vous utilisez un plan Consommation, les instances de l’hôte Azure Functions sont ajoutées et supprimées de façon dynamique en fonction du nombre d’événements entrants.</span><span class="sxs-lookup"><span data-stu-id="8984b-122">When you're using a Consumption plan, instances of the Azure Functions host are dynamically added and removed based on the number of incoming events.</span></span> <span data-ttu-id="8984b-123">Ce plan est mis à l’échelle automatiquement, et vous êtes facturé pour les ressources de calcul uniquement quand vos fonctions sont exécutées.</span><span class="sxs-lookup"><span data-stu-id="8984b-123">This plan scales automatically, and you are charged for compute resources only when your functions are running.</span></span> <span data-ttu-id="8984b-124">Dans un plan Consommation, une fonction peut s’exécuter pendant 10 minutes au plus.</span><span class="sxs-lookup"><span data-stu-id="8984b-124">On a Consumption plan, a function can run for a maximum of 10 minutes.</span></span> 

> [!NOTE]
> <span data-ttu-id="8984b-125">Le délai d’expiration par défaut pour les fonctions dans un plan Consommation est de 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="8984b-125">The default timeout for functions on a Consumption plan is 5 minutes.</span></span> <span data-ttu-id="8984b-126">Vous pouvez augmenter la valeur à 10 minutes pour l’application de fonction en modifiant la propriété `functionTimeout` dans [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="8984b-126">The value can be increased to 10 minutes for the Function App by changing the property `functionTimeout` in [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>

<span data-ttu-id="8984b-127">La facturation est basée sur la durée d’exécution et la mémoire utilisée. Elle est agrégée dans toutes les fonctions d’une application de fonction.</span><span class="sxs-lookup"><span data-stu-id="8984b-127">Billing is based on execution time and memory used, and it's aggregated across all functions within a function app.</span></span> <span data-ttu-id="8984b-128">Pour plus d’informations, consultez la page [Tarification d’Azure Functions].</span><span class="sxs-lookup"><span data-stu-id="8984b-128">For more information, see the [Azure Functions pricing page].</span></span>

<span data-ttu-id="8984b-129">Le plan par défaut, le plan Consommation, présente les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="8984b-129">The Consumption plan is the default and offers the following benefits:</span></span>
- <span data-ttu-id="8984b-130">Paiement uniquement à l’exécution de vos fonctions</span><span class="sxs-lookup"><span data-stu-id="8984b-130">Pay only when your functions are running.</span></span>
- <span data-ttu-id="8984b-131">Augmentation automatique de la taille des instances même pendant les périodes de charge élevée</span><span class="sxs-lookup"><span data-stu-id="8984b-131">Scale out automatically, even during periods of high load.</span></span>

## <a name="app-service-plan"></a><span data-ttu-id="8984b-132">Plan App Service</span><span class="sxs-lookup"><span data-stu-id="8984b-132">App Service plan</span></span>

<span data-ttu-id="8984b-133">Dans le plan App Service, vos applications de fonction sont exécutées sur des machines virtuelles dédiées sur des références de base, Standard et Premium, à l’instar de Web Apps.</span><span class="sxs-lookup"><span data-stu-id="8984b-133">In the App Service plan, your function apps run on dedicated VMs on Basic, Standard, and Premium SKUs, similar to Web Apps.</span></span> <span data-ttu-id="8984b-134">Les machines virtuelles dédiées sont allouées à vos applications App Service, ce qui signifie que l’hôte des fonctions est toujours en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="8984b-134">Dedicated VMs are allocated to your App Service apps, which means the functions host is always running.</span></span>

<span data-ttu-id="8984b-135">Pensez à un plan App Service dans les cas suivants :</span><span class="sxs-lookup"><span data-stu-id="8984b-135">Consider an App Service plan in the following cases:</span></span>
- <span data-ttu-id="8984b-136">Vous disposez de machines virtuelles existantes, sous-utilisées qui exécutent déjà d’autres instances App Service.</span><span class="sxs-lookup"><span data-stu-id="8984b-136">You have existing, underutilized VMs that are already running other App Service instances.</span></span>
- <span data-ttu-id="8984b-137">Vous souhaitez que vos applications de fonction s’exécutent en continu ou presque.</span><span class="sxs-lookup"><span data-stu-id="8984b-137">You expect your function apps to run continuously, or nearly continuously.</span></span>
- <span data-ttu-id="8984b-138">Vous avez besoin de plus d’options de mémoire ou de processeur que celles qui sont proposées dans le plan Consommation.</span><span class="sxs-lookup"><span data-stu-id="8984b-138">You need more CPU or memory options than what is provided on the Consumption plan.</span></span>
- <span data-ttu-id="8984b-139">Vous avez besoin d’une durée d’exécution supérieure à celle qui est autorisée dans le plan Consommation.</span><span class="sxs-lookup"><span data-stu-id="8984b-139">You need to run longer than the maximum execution time allowed on the Consumption plan.</span></span>

<span data-ttu-id="8984b-140">L’utilisation d’une machine virtuelle dissocie le coût de l’exécution et de la taille de mémoire.</span><span class="sxs-lookup"><span data-stu-id="8984b-140">A VM decouples cost from both runtime and memory size.</span></span> <span data-ttu-id="8984b-141">Vous ne payez donc pas plus que le coût de l’instance de machine virtuelle que vous allouez.</span><span class="sxs-lookup"><span data-stu-id="8984b-141">As a result, you won't pay more than the cost of the VM instance that you allocate.</span></span> <span data-ttu-id="8984b-142">Pour plus d’informations sur le fonctionnement du plan App Service, consultez l’article [Présentation détaillée des plans d’Azure App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8984b-142">For details about how the App Service plan works, see the [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

<span data-ttu-id="8984b-143">Avec un plan App Service, vous pouvez augmenter manuellement la taille des instances en ajoutant des instances de machine virtuelle, ou vous pouvez activer la mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="8984b-143">With an App Service plan, you can manually scale out by adding more VM instances, or you can enable autoscale.</span></span> <span data-ttu-id="8984b-144">Pour plus d’informations, consultez [Mettre à l’échelle le nombre d’instances manuellement ou automatiquement](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8984b-144">For more information, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span></span> <span data-ttu-id="8984b-145">Vous pouvez également effectuer une montée en puissance en choisissant un autre plan App Service.</span><span class="sxs-lookup"><span data-stu-id="8984b-145">You can also scale up by choosing a different App Service plan.</span></span> <span data-ttu-id="8984b-146">Pour plus d’informations, consultez [Faire monter en puissance une application web dans Azure](../app-service-web/web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="8984b-146">For more information, see [Scale up an app in Azure](../app-service-web/web-sites-scale.md).</span></span> <span data-ttu-id="8984b-147">Si vous prévoyez d’exécuter des fonctions JavaScript dans un plan App Service, vous devez choisir un plan qui comporte moins de cœurs.</span><span class="sxs-lookup"><span data-stu-id="8984b-147">If you are planning to run JavaScript functions on an App Service plan, you should choose a plan that has fewer cores.</span></span> <span data-ttu-id="8984b-148">Pour plus d’informations, consultez les [informations de référence sur JavaScript pour Functions](functions-reference-node.md#choose-single-core-app-service-plans).</span><span class="sxs-lookup"><span data-stu-id="8984b-148">For more information, see the [JavaScript reference for Functions](functions-reference-node.md#choose-single-core-app-service-plans).</span></span>  

<span data-ttu-id="8984b-149"><!-- Note: the portal links to this section via fwlink https://go.microsoft.com/fwlink/?linkid=830855 --> 
<a name="always-on"></a>
### Toujours actif</span><span class="sxs-lookup"><span data-stu-id="8984b-149"><!-- Note: the portal links to this section via fwlink https://go.microsoft.com/fwlink/?linkid=830855 --> 
<a name="always-on"></a>
### Always On</span></span>

<span data-ttu-id="8984b-150">Si vous utilisez un plan App Service, vous devez activer le paramètre **Toujours actif** afin que l’application de fonction s’exécute correctement.</span><span class="sxs-lookup"><span data-stu-id="8984b-150">If you run on an App Service plan, you should enable the **Always On** setting so that your function app  runs correctly.</span></span> <span data-ttu-id="8984b-151">Dans un plan App Service, comme le runtime des fonctions devient inactif après quelques minutes d’inactivité, seuls des déclencheurs HTTP « relancent » vos fonctions.</span><span class="sxs-lookup"><span data-stu-id="8984b-151">On an App Service plan, the functions runtime will go idle after a few minutes of inactivity, so only HTTP triggers will "wake up" your functions.</span></span> <span data-ttu-id="8984b-152">Ce fonctionnement est semblable à celui du service WebJobs pour lequel le paramètre Toujours actif doit toujours être activé.</span><span class="sxs-lookup"><span data-stu-id="8984b-152">This is similar to how WebJobs must have Always On enabled.</span></span> 

<span data-ttu-id="8984b-153">Le paramètre Toujours actif est disponible uniquement dans un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="8984b-153">Always On is available only on an App Service plan.</span></span> <span data-ttu-id="8984b-154">Dans un plan Consommation, la plateforme active automatiquement les applications de fonction.</span><span class="sxs-lookup"><span data-stu-id="8984b-154">On a Consumption plan, the platform activates function apps automatically.</span></span>

## <a name="storage-account-requirements"></a><span data-ttu-id="8984b-155">Conditions requises pour le compte de stockage</span><span class="sxs-lookup"><span data-stu-id="8984b-155">Storage account requirements</span></span>

<span data-ttu-id="8984b-156">Dans un plan Consommation ou un plan App Service, une application de fonction nécessite un compte de stockage Azure qui prend en charge les stockages Azure Blob, File d’attente et Table.</span><span class="sxs-lookup"><span data-stu-id="8984b-156">On either a Consumption plan or an App Service plan, a function app requires an Azure Storage account that supports Azure Blob, Queue, and Table storage.</span></span> <span data-ttu-id="8984b-157">En interne, Azure Functions utilise le stockage Azure pour les opérations telles que la gestion des déclencheurs et la journalisation des exécutions de fonctions.</span><span class="sxs-lookup"><span data-stu-id="8984b-157">Internally, Azure Functions uses Azure Storage for operations such as managing triggers and logging function executions.</span></span> <span data-ttu-id="8984b-158">Certains comptes de stockage ne prennent pas en charge les files d’attente et les tables, comme les comptes de stockage Blob uniquement (notamment le stockage Premium) et les comptes de stockage à usage général avec la réplication ZRS.</span><span class="sxs-lookup"><span data-stu-id="8984b-158">Some storage accounts do not support queues and tables, such as blob-only storage accounts (including premium storage) and general-purpose storage accounts with zone-redundant storage replication.</span></span> <span data-ttu-id="8984b-159">Ces comptes sont filtrés à partir du panneau **Compte de stockage** quand vous créez une application de fonction.</span><span class="sxs-lookup"><span data-stu-id="8984b-159">These accounts are filtered from the **Storage Account** blade when you're creating a function app.</span></span>

<span data-ttu-id="8984b-160">Pour en savoir plus sur les types de compte de stockage, consultez [Présentation des services Stockage Azure](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span><span class="sxs-lookup"><span data-stu-id="8984b-160">To learn more about storage account types, see [Introducing the Azure Storage services](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).</span></span>

## <a name="how-the-consumption-plan-works"></a><span data-ttu-id="8984b-161">Fonctionnement du plan de consommation</span><span class="sxs-lookup"><span data-stu-id="8984b-161">How the Consumption plan works</span></span>

<span data-ttu-id="8984b-162">Le plan Consommation met automatiquement à l’échelle les ressources processeur et mémoire en ajoutant des instances de l’hôte Functions en fonction du nombre d’événements en fonction desquels ses fonctions sont déclenchées.</span><span class="sxs-lookup"><span data-stu-id="8984b-162">The Consumption plan automatically scales CPU and memory resources by adding additional instances of the Functions host, based on the number of events that its functions are triggered on.</span></span> <span data-ttu-id="8984b-163">Chaque instance de l’hôte Functions est limitée à 1,5 Go de mémoire.</span><span class="sxs-lookup"><span data-stu-id="8984b-163">Each instance of the Functions host is limited to 1.5 GB of memory.</span></span>

<span data-ttu-id="8984b-164">Quand vous utilisez le plan d’hébergement Consommation, les fichiers de code de fonction sont stockés dans des partages de fichiers Azure du compte de stockage principal.</span><span class="sxs-lookup"><span data-stu-id="8984b-164">When you use the Consumption hosting plan, function code files are stored on Azure Files shares on the main storage account.</span></span> <span data-ttu-id="8984b-165">Lorsque vous supprimez le compte de stockage principal, ce contenu est supprimé et ne peut pas être récupéré.</span><span class="sxs-lookup"><span data-stu-id="8984b-165">When you delete the main storage account, this content is deleted and cannot be recovered.</span></span>

> [!NOTE]
> <span data-ttu-id="8984b-166">Quand vous utilisez un déclencheur d’objet blob dans un plan Consommation, il peut y avoir jusqu’à 10 minutes de délai dans le traitement des nouveaux objets blob si une application de fonction est devenue inactive.</span><span class="sxs-lookup"><span data-stu-id="8984b-166">When you're using a blob trigger on a Consumption plan, there can be up to a 10-minute delay in processing new blobs if a function app has gone idle.</span></span> <span data-ttu-id="8984b-167">Une fois l’application de fonction en cours d’exécution, les blobs sont traités immédiatement.</span><span class="sxs-lookup"><span data-stu-id="8984b-167">After the function app is running, blobs are processed immediately.</span></span> <span data-ttu-id="8984b-168">Pour éviter ce délai initial, pensez à l’une des options suivantes :</span><span class="sxs-lookup"><span data-stu-id="8984b-168">To avoid this initial delay, consider one of the following options:</span></span>
> - <span data-ttu-id="8984b-169">Utilisez un plan App Service avec le paramètre Toujours actif activé.</span><span class="sxs-lookup"><span data-stu-id="8984b-169">Use an App Service plan with Always On enabled.</span></span>
> - <span data-ttu-id="8984b-170">Utilisez un autre mécanisme pour déclencher le traitement de l’objet blob, comme un message de file d’attente qui contient le nom de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="8984b-170">Use another mechanism to trigger the blob processing, such as a queue message that contains the blob name.</span></span> <span data-ttu-id="8984b-171">Pour en obtenir un exemple, consultez [Déclencheur de file d’attente avec liaison d’entrée d’objet blob](functions-bindings-storage-blob.md#input-sample).</span><span class="sxs-lookup"><span data-stu-id="8984b-171">For an example, see [Queue trigger with blob input binding](functions-bindings-storage-blob.md#input-sample).</span></span>

### <a name="runtime-scaling"></a><span data-ttu-id="8984b-172">Mise à l’échelle du runtime</span><span class="sxs-lookup"><span data-stu-id="8984b-172">Runtime scaling</span></span>

<span data-ttu-id="8984b-173">Azure Functions utilise un composant appelé *contrôleur de mise à l’échelle* pour surveiller la fréquence des événements et déterminer s’il convient de monter ou de descendre en puissance.</span><span class="sxs-lookup"><span data-stu-id="8984b-173">Azure Functions uses a component called the *scale controller* to monitor the rate of events and determine whether to scale out or scale down.</span></span> <span data-ttu-id="8984b-174">Le contrôleur de mise à l’échelle utilise une méthode heuristique pour chaque type de déclencheur.</span><span class="sxs-lookup"><span data-stu-id="8984b-174">The scale controller uses heuristics for each trigger type.</span></span> <span data-ttu-id="8984b-175">Par exemple, si vous utilisez un déclencheur de stockage File d’attente Azure, il est mis à l’échelle en fonction de la longueur de la file d’attente et de l’âge du plus ancien message en file d’attente.</span><span class="sxs-lookup"><span data-stu-id="8984b-175">For example, when you're using an Azure Queue storage trigger, it scales based on the queue length and the age of the oldest queue message.</span></span>

<span data-ttu-id="8984b-176">L’unité de mise à l’échelle est l’application de fonction.</span><span class="sxs-lookup"><span data-stu-id="8984b-176">The unit of scale is the function app.</span></span> <span data-ttu-id="8984b-177">Quand les instances de l’application de fonction font l’objet d’une augmentation de taille, d’autres ressources sont allouées pour exécuter plusieurs instances de l’hôte Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="8984b-177">When the function app is scaled out, more resources are allocated to run multiple instances of the Azure Functions host.</span></span> <span data-ttu-id="8984b-178">À l’inverse, quand la demande de calcul est réduite, le contrôleur de mise à l’échelle supprime des instances de l’hôte de fonction.</span><span class="sxs-lookup"><span data-stu-id="8984b-178">Conversely, as compute demand is reduced, the scale controller removes function host instances.</span></span> <span data-ttu-id="8984b-179">Le nombre d’instances est finalement réduit à zéro si aucune fonction n’est exécutée dans une application de fonction.</span><span class="sxs-lookup"><span data-stu-id="8984b-179">The number of instances is eventually scaled down to zero when no functions are running within a function app.</span></span>

![Contrôleur de mise à l’échelle surveillant les événements et créant des instances](./media/functions-scale/central-listener.png)

### <a name="billing-model"></a><span data-ttu-id="8984b-181">Modèle de facturation</span><span class="sxs-lookup"><span data-stu-id="8984b-181">Billing model</span></span>

<span data-ttu-id="8984b-182">La facturation du plan de consommation est décrite en détail dans la page [Tarification d’Azure Functions].</span><span class="sxs-lookup"><span data-stu-id="8984b-182">Billing for the Consumption plan is described in detail on the [Azure Functions pricing page].</span></span> <span data-ttu-id="8984b-183">L’utilisation est agrégée au niveau de l’application de fonction et compte uniquement la durée d’exécution du code de fonction.</span><span class="sxs-lookup"><span data-stu-id="8984b-183">Usage is aggregated at the function app level and counts only the time that function code is running.</span></span> <span data-ttu-id="8984b-184">Les unités de facturation sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="8984b-184">The following are units for billing:</span></span> 
* <span data-ttu-id="8984b-185">**Consommation des ressources en gigaoctet/seconde (Go/s)**.</span><span class="sxs-lookup"><span data-stu-id="8984b-185">**Resource consumption in gigabyte-seconds (GB-s)**.</span></span> <span data-ttu-id="8984b-186">Calcul effectué d’après une combinaison de la taille de la mémoire et de la durée d’exécution pour toutes les fonctions d’une application de fonction.</span><span class="sxs-lookup"><span data-stu-id="8984b-186">Computed as a combination of memory size and execution time for all functions within a function app.</span></span> 
* <span data-ttu-id="8984b-187">**Exécutions**.</span><span class="sxs-lookup"><span data-stu-id="8984b-187">**Executions**.</span></span> <span data-ttu-id="8984b-188">Comptées chaque fois qu’une fonction est exécutée en réponse à un événement déclenché par une liaison.</span><span class="sxs-lookup"><span data-stu-id="8984b-188">Counted each time a function is executed in response to an event, triggered by a binding.</span></span>

[Tarification d’Azure Functions]: https://azure.microsoft.com/pricing/details/functions