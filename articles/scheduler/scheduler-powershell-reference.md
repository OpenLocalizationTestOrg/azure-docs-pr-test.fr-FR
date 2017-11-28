---
title: "aaaScheduler référence des applets de commande PowerShell"
description: "Informations de référence sur les applets de commande PowerShell de Scheduler"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 9a26c457-d7a1-4e4a-bc79-f26592155218
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: a2b23bcd3e4493ffba1dbf21fbb87818be7c01e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-powershell-cmdlets-reference"></a><span data-ttu-id="7090e-103">Informations de référence sur les applets de commande PowerShell de Scheduler</span><span class="sxs-lookup"><span data-stu-id="7090e-103">Scheduler PowerShell Cmdlets Reference</span></span>
<span data-ttu-id="7090e-104">Hello tableau suivant décrit et des liens de page de référence toohello de chacune des applets de commande principales hello dans Azure Scheduler.</span><span class="sxs-lookup"><span data-stu-id="7090e-104">hello following table describes and links toohello reference page of each of hello major cmdlets in Azure Scheduler.</span></span>

<span data-ttu-id="7090e-105">tooinstall Azure PowerShell et associez-le à votre abonnement Azure, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7090e-105">tooinstall Azure PowerShell and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> 

<span data-ttu-id="7090e-106">Pour plus d’informations sur les [applets de commande Azure Resource Manager](/powershell/azure/overview), consultez [Utilisation d’Azure PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="7090e-106">For more information about [Azure Resource Manager cmdlets](/powershell/azure/overview), see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

| <span data-ttu-id="7090e-107">Applet de commande</span><span class="sxs-lookup"><span data-stu-id="7090e-107">Cmdlet</span></span> | <span data-ttu-id="7090e-108">Description de l'applet de commande</span><span class="sxs-lookup"><span data-stu-id="7090e-108">Cmdlet Description</span></span> |
| --- | --- |
| [<span data-ttu-id="7090e-109">Disable-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="7090e-109">Disable-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/disable-azurermschedulerjobcollection) |<span data-ttu-id="7090e-110">Désactive une collection de travaux.</span><span class="sxs-lookup"><span data-stu-id="7090e-110">Disables a job collection.</span></span> |
| [<span data-ttu-id="7090e-111">Enable-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="7090e-111">Enable-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/enable-azurermschedulerjobcollection) |<span data-ttu-id="7090e-112">Active une collection de travaux.</span><span class="sxs-lookup"><span data-stu-id="7090e-112">Enables a job collection.</span></span> |
| [<span data-ttu-id="7090e-113">Get-AzureRmSchedulerJob</span><span class="sxs-lookup"><span data-stu-id="7090e-113">Get-AzureRmSchedulerJob</span></span>](/powershell/module/azurerm.scheduler/get-azurermschedulerjob) |<span data-ttu-id="7090e-114">Récupère les travaux du Planificateur.</span><span class="sxs-lookup"><span data-stu-id="7090e-114">Gets Scheduler jobs.</span></span> |
| [<span data-ttu-id="7090e-115">Get-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="7090e-115">Get-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/get-azurermschedulerjobcollection) |<span data-ttu-id="7090e-116">Récupère les collections de travaux.</span><span class="sxs-lookup"><span data-stu-id="7090e-116">Gets job collections.</span></span> |
| [<span data-ttu-id="7090e-117">Get-AzureRmSchedulerJobHistory</span><span class="sxs-lookup"><span data-stu-id="7090e-117">Get-AzureRmSchedulerJobHistory</span></span>](/powershell/module/azurerm.scheduler/get-azurermschedulerjobhistory) |<span data-ttu-id="7090e-118">Affiche l’historique des travaux.</span><span class="sxs-lookup"><span data-stu-id="7090e-118">Gets job history.</span></span> |
| [<span data-ttu-id="7090e-119">New-AzureRmSchedulerHttpJob</span><span class="sxs-lookup"><span data-stu-id="7090e-119">New-AzureRmSchedulerHttpJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerhttpjob) |<span data-ttu-id="7090e-120">Crée un travail HTTP.</span><span class="sxs-lookup"><span data-stu-id="7090e-120">Creates an HTTP job.</span></span> |
| [<span data-ttu-id="7090e-121">New-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="7090e-121">New-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerjobcollection) |<span data-ttu-id="7090e-122">Crée une collection de travaux.</span><span class="sxs-lookup"><span data-stu-id="7090e-122">Creates a job collection.</span></span> |
| [<span data-ttu-id="7090e-123">New-AzureRmSchedulerServiceBusQueueJob</span><span class="sxs-lookup"><span data-stu-id="7090e-123">New-AzureRmSchedulerServiceBusQueueJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerservicebusqueuejob) |<span data-ttu-id="7090e-124">Crée un travail de file d’attente Service Bus.</span><span class="sxs-lookup"><span data-stu-id="7090e-124">Creates a service bus queue job.</span></span> |
| [<span data-ttu-id="7090e-125">New-AzureRmSchedulerServiceBusTopicJob</span><span class="sxs-lookup"><span data-stu-id="7090e-125">New-AzureRmSchedulerServiceBusTopicJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerservicebustopicjob) |<span data-ttu-id="7090e-126">Crée un travail de rubrique Service Bus.</span><span class="sxs-lookup"><span data-stu-id="7090e-126">Creates a service bus topic job.</span></span> |
| [<span data-ttu-id="7090e-127">New-AzureRmSchedulerStorageQueueJob</span><span class="sxs-lookup"><span data-stu-id="7090e-127">New-AzureRmSchedulerStorageQueueJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerstoragequeuejob) |<span data-ttu-id="7090e-128">Crée un travail de file d’attente de stockage.</span><span class="sxs-lookup"><span data-stu-id="7090e-128">Creates a storage queue job.</span></span> |
| [<span data-ttu-id="7090e-129">Remove-AzureRmSchedulerJob</span><span class="sxs-lookup"><span data-stu-id="7090e-129">Remove-AzureRmSchedulerJob</span></span>](/powershell/module/azurerm.scheduler/remove-azurermschedulerjob) |<span data-ttu-id="7090e-130">Supprime un travail du Planificateur.</span><span class="sxs-lookup"><span data-stu-id="7090e-130">Removes a Scheduler job.</span></span> |
| [<span data-ttu-id="7090e-131">Remove-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="7090e-131">Remove-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/remove-azurermschedulerjobcollection) |<span data-ttu-id="7090e-132">Supprime une collection de travaux.</span><span class="sxs-lookup"><span data-stu-id="7090e-132">Removes a job collection.</span></span> |
| [<span data-ttu-id="7090e-133">Set-AzureRmSchedulerHttpJob</span><span class="sxs-lookup"><span data-stu-id="7090e-133">Set-AzureRmSchedulerHttpJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerhttpjob) |<span data-ttu-id="7090e-134">Modifie un travail HTTP du Planificateur.</span><span class="sxs-lookup"><span data-stu-id="7090e-134">Modifies a Scheduler HTTP job.</span></span> |
| [<span data-ttu-id="7090e-135">Set-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="7090e-135">Set-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerjobcollection) |<span data-ttu-id="7090e-136">Modifie une collection de travaux.</span><span class="sxs-lookup"><span data-stu-id="7090e-136">Modifies a job collection.</span></span> |
| [<span data-ttu-id="7090e-137">Set-AzureRmSchedulerServiceBusQueueJob</span><span class="sxs-lookup"><span data-stu-id="7090e-137">Set-AzureRmSchedulerServiceBusQueueJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerservicebusqueuejob) |<span data-ttu-id="7090e-138">Modifie un travail de file d’attente Service Bus.</span><span class="sxs-lookup"><span data-stu-id="7090e-138">Modifies a service bus queue job.</span></span> |
| [<span data-ttu-id="7090e-139">Set-AzureRmSchedulerServiceBusTopicJob</span><span class="sxs-lookup"><span data-stu-id="7090e-139">Set-AzureRmSchedulerServiceBusTopicJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerservicebustopicjob) |<span data-ttu-id="7090e-140">Modifie un travail de rubrique Service Bus.</span><span class="sxs-lookup"><span data-stu-id="7090e-140">Modifies a service bus topic job.</span></span> |
| [<span data-ttu-id="7090e-141">Set-AzureRmSchedulerStorageQueueJob</span><span class="sxs-lookup"><span data-stu-id="7090e-141">Set-AzureRmSchedulerStorageQueueJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerstoragequeuejob) |<span data-ttu-id="7090e-142">Modifie un travail de file d’attente de stockage.</span><span class="sxs-lookup"><span data-stu-id="7090e-142">Modifies a storage queue job.</span></span> |

<span data-ttu-id="7090e-143">Pour plus d’informations, vous pouvez exécuter des hello suivant d’applets de commande :</span><span class="sxs-lookup"><span data-stu-id="7090e-143">For more detailed information, you can run any of hello following cmdlets:</span></span> 

```
Get-Help <cmdlet name> -Detailed
```
```
Get-Help <cmdlet name> -Examples
```
```
Get-Help <cmdlet name> -Full
```

## <a name="see-also"></a><span data-ttu-id="7090e-144">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="7090e-144">See Also</span></span>
 [<span data-ttu-id="7090e-145">Présentation d'Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="7090e-145">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="7090e-146">Concepts, terminologie et hiérarchie d’entités d’Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="7090e-146">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="7090e-147">Prise en main du planificateur Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="7090e-147">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="7090e-148">Plans et facturation dans Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="7090e-148">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="7090e-149">Informations de référence sur l’API REST d’Azure Scheluler</span><span class="sxs-lookup"><span data-stu-id="7090e-149">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="7090e-150">Haute disponibilité et fiabilité d’Azure Scheluler</span><span class="sxs-lookup"><span data-stu-id="7090e-150">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="7090e-151">Limites, valeurs par défaut et codes d’erreur d’Azure Scheluler</span><span class="sxs-lookup"><span data-stu-id="7090e-151">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="7090e-152">Authentification sortante d’Azure Scheluler</span><span class="sxs-lookup"><span data-stu-id="7090e-152">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

