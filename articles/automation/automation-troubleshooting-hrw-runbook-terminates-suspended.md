---
title: "Runbook Worker hybride : une tâche de runbook se termine avec l’état suspendu | Microsoft Docs"
description: "Causes des problèmes et résolutions en cas d’erreur provoquant la fin de la tâche Runbook Worker hybride."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 02c6606e-8924-4328-a196-45630c2255e9
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/17/2016
ms.author: magoedte
ms.openlocfilehash: 7c6365b729d73f1c5b9bc57952b1723255d9e9f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="hybrid-runbook-worker-a-runbook-job-terminates-with-a-status-of-suspended"></a><span data-ttu-id="42500-103">Runbook Worker hybride : une tâche de runbook se termine avec l’état suspendu</span><span class="sxs-lookup"><span data-stu-id="42500-103">Hybrid Runbook Worker: A runbook job terminates with a status of Suspended</span></span>
## <a name="summary"></a><span data-ttu-id="42500-104">Résumé</span><span class="sxs-lookup"><span data-stu-id="42500-104">Summary</span></span>
<span data-ttu-id="42500-105">Le runbook est interrompu peu après la tentative de l’exécuter trois fois.</span><span class="sxs-lookup"><span data-stu-id="42500-105">Your runbook is suspended shortly after attempting to execute it three times.</span></span> <span data-ttu-id="42500-106">Il existe des conditions susceptibles d’interrompre l’exécution correcte du runbook et le message d’erreur lié n’inclut pas d’informations supplémentaires indiquant pourquoi.</span><span class="sxs-lookup"><span data-stu-id="42500-106">There are conditions which may interrupt the runbook from completing successfully and the related error message does not include any additional information indicating why.</span></span> <span data-ttu-id="42500-107">Cet article fournit des étapes de dépannage pour des problèmes concernant les échecs d’exécution du runbook worker hybride.</span><span class="sxs-lookup"><span data-stu-id="42500-107">This article provides troubleshooting steps for issues related to the Hybrid Runbook Worker runbook execution failures.</span></span>

<span data-ttu-id="42500-108">Si le problème lié à Azure n’est pas traité dans cet article, parcourez les forums Azure sur [MSDN et Stack Overflow](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="42500-108">If your Azure issue is not addressed in this article, visit the Azure forums on [MSDN and the Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="42500-109">Vous pouvez publier votre problème sur ces forums ou dans [@AzureSupport sur Twitter](https://twitter.com/AzureSupport).</span><span class="sxs-lookup"><span data-stu-id="42500-109">You can post your issue on these forums or to [@AzureSupport on Twitter](https://twitter.com/AzureSupport).</span></span> <span data-ttu-id="42500-110">Vous pouvez également créer une demande de support Azure en sélectionnant **Obtenir de l’aide** sur le site du [support Azure](https://azure.microsoft.com/support/options/) .</span><span class="sxs-lookup"><span data-stu-id="42500-110">Also, you can file an Azure support request by selecting **Get support** on the [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptom"></a><span data-ttu-id="42500-111">Symptôme</span><span class="sxs-lookup"><span data-stu-id="42500-111">Symptom</span></span>
<span data-ttu-id="42500-112">L’exécution du runbook échoue et l’erreur est retournée est « L’action de la tâche ’Activate’ ne peut pas être exécutée, car le processus s’est arrêté inopinément.</span><span class="sxs-lookup"><span data-stu-id="42500-112">Runbook execution fails and the error returned is, "The job action 'Activate' cannot be run, because the process stopped unexpectedly.</span></span> <span data-ttu-id="42500-113">L’action de la tâche a été tentée 3 fois. »</span><span class="sxs-lookup"><span data-stu-id="42500-113">The job action was attempted 3 times."</span></span>

## <a name="cause"></a><span data-ttu-id="42500-114">Cause :</span><span class="sxs-lookup"><span data-stu-id="42500-114">Cause</span></span>
<span data-ttu-id="42500-115">Il existe plusieurs causes possibles pour cette erreur :</span><span class="sxs-lookup"><span data-stu-id="42500-115">There are several possible causes for the error:</span></span> 

1. <span data-ttu-id="42500-116">Le worker hybride est derrière un pare-feu ou un proxy</span><span class="sxs-lookup"><span data-stu-id="42500-116">The hybrid worker is behind a proxy or firewall</span></span>
2. <span data-ttu-id="42500-117">L’ordinateur sur lequel le worker hybride s’exécute ne respecte pas les [exigences](automation-hybrid-runbook-worker.md#hybrid-runbook-worker-requirements)</span><span class="sxs-lookup"><span data-stu-id="42500-117">The computer the hybrid worker is running on has less than the minimum hardware [requirements](automation-hybrid-runbook-worker.md#hybrid-runbook-worker-requirements)</span></span> 
3. <span data-ttu-id="42500-118">Les runbooks ne peuvent pas s’authentifier auprès des ressources locales</span><span class="sxs-lookup"><span data-stu-id="42500-118">The runbooks cannot authenticate with local resources</span></span>

## <a name="cause-1-hybrid-runbook-worker-is-behind-proxy-or-firewall"></a><span data-ttu-id="42500-119">Cause 1 : Le runbook worker hybride est derrière un proxy ou un pare-feu</span><span class="sxs-lookup"><span data-stu-id="42500-119">Cause 1: Hybrid Runbook Worker is behind proxy or firewall</span></span>
<span data-ttu-id="42500-120">L’ordinateur sur lequel s’exécute le runbook worker hybride est derrière un pare-feu ou un serveur proxy, et un accès réseau sortant peut ne pas être autorisé ou configuré correctement.</span><span class="sxs-lookup"><span data-stu-id="42500-120">The computer the Hybrid Runbook Worker is running on is behind a firewall or proxy server and outbound network access may not be permitted or configured correctly.</span></span>

### <a name="solution"></a><span data-ttu-id="42500-121">Solution</span><span class="sxs-lookup"><span data-stu-id="42500-121">Solution</span></span>
<span data-ttu-id="42500-122">Vérifiez que l’ordinateur dispose d’un accès sortant à *.cloudapp.net sur les ports 443, 9354 et de 30000 à 30199.</span><span class="sxs-lookup"><span data-stu-id="42500-122">Verify the computer has outbound access to *.cloudapp.net on ports 443, 9354, and 30000-30199.</span></span> 

## <a name="cause-2-computer-has-less-than-minimum-hardware-requirements"></a><span data-ttu-id="42500-123">Cause 2 : L’ordinateur ne dispose pas de la configuration minimale requise</span><span class="sxs-lookup"><span data-stu-id="42500-123">Cause 2: Computer has less than minimum hardware requirements</span></span>
<span data-ttu-id="42500-124">Les ordinateurs qui exécutent les workers hybrides doivent respecter la configuration matérielle minimale requise avant de pouvoir héberger cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="42500-124">Computers running the Hybrid Runbook Worker should meet the minimum hardware requirements before designating it to host this feature.</span></span> <span data-ttu-id="42500-125">Sinon, en fonction de l’utilisation des ressources d’autres processus d’arrière-plan et de la contention due aux runbooks lors de l’exécution, l’ordinateur sera surchargé, entraînant des retards ou des délais d’attente pour la tâche du runbook.</span><span class="sxs-lookup"><span data-stu-id="42500-125">Otherwise, depending on the resource utilization of other background processes and contention caused by runbooks during execution, the computer will become over utilized and cause runbook job delays or timeouts.</span></span> 

### <a name="solution"></a><span data-ttu-id="42500-126">Solution</span><span class="sxs-lookup"><span data-stu-id="42500-126">Solution</span></span>
<span data-ttu-id="42500-127">Vérifiez tout d’abord que l’ordinateur désigné pour exécuter la fonctionnalité Runbook Worker hybride répond à la configuration matérielle minimale requise.</span><span class="sxs-lookup"><span data-stu-id="42500-127">First confirm the computer designated to run the Hybrid Runbook Worker feature meets the minimum hardware requirements.</span></span>  <span data-ttu-id="42500-128">Si c’est le cas, surveillez l’utilisation du processeur et de la mémoire pour déterminer toute corrélation entre les performances des processus Runbook Worker hybride et de Windows.</span><span class="sxs-lookup"><span data-stu-id="42500-128">If it does, monitor CPU and memory utilization to determine any correlation between the performance of Hybrid Runbook Worker processes and Windows.</span></span>  <span data-ttu-id="42500-129">S’il existe une surcharge de la mémoire ou du processeur, cela peut indiquer la nécessité de mettre à niveau ou d’ajouter des processeurs supplémentaires, ou d’augmenter la mémoire pour résoudre le goulot d’étranglement des ressources et résoudre l’erreur.</span><span class="sxs-lookup"><span data-stu-id="42500-129">If there is memory or CPU pressure, this may indicate the need to upgrade or add additional processors, or increase memory to address the resource bottleneck and resolve the error.</span></span> <span data-ttu-id="42500-130">Vous pouvez également sélectionner une ressource de calcul différente qui peut prendre en charge la configuration minimale requise et évoluer lorsque les demandes en matière de charge de travail indiquent qu’une augmentation est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="42500-130">Alternatively, select a different compute resource that can support the minimum requirements and scale when workload demands indicate an increase is necessary.</span></span>         

## <a name="cause-3-runbooks-cannot-authenticate-with-local-resources"></a><span data-ttu-id="42500-131">Cause 3 : Les runbooks ne peuvent pas s’authentifier auprès des ressources locales</span><span class="sxs-lookup"><span data-stu-id="42500-131">Cause 3: Runbooks cannot authenticate with local resources</span></span>
### <a name="solution"></a><span data-ttu-id="42500-132">Solution</span><span class="sxs-lookup"><span data-stu-id="42500-132">Solution</span></span>
<span data-ttu-id="42500-133">Vérifiez dans le journal des événements **Microsoft-SMA** la présence d’un événement correspondant avec la description *Le processus Win32 s’est terminé avec le code [4294967295]*.</span><span class="sxs-lookup"><span data-stu-id="42500-133">Check the **Microsoft-SMA** event log for a corresponding event with description *Win32 Process Exited with code [4294967295]*.</span></span>  <span data-ttu-id="42500-134">La cause de cette erreur est que vous n’avez pas configuré l’authentification dans vos runbooks ou que vous n’avez pas spécifié les informations d’identification Exécuter en tant que pour le groupe Worker hybride.</span><span class="sxs-lookup"><span data-stu-id="42500-134">The cause of this error is you haven't configured authentication in your runbooks or specified the Run As credentials for the Hybrid worker group.</span></span>  <span data-ttu-id="42500-135">Veuillez consulter les [autorisations du Runbook](automation-hybrid-runbook-worker.md#runbook-permissions) pour confirmer que l’authentification a été correctement configurée pour vos Runbooks.</span><span class="sxs-lookup"><span data-stu-id="42500-135">Please review [Runbook permissions](automation-hybrid-runbook-worker.md#runbook-permissions) to confirm you have correctly configured authentication for your runbooks.</span></span>  
