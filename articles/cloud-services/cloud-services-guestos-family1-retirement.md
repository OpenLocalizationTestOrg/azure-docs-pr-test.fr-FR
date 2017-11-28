---
title: "Informations relatives à la suppression de la famille 1 des systèmes d’exploitation invités | Microsoft Docs"
description: "Fournit des informations sur la suppression de la famille 1 des SE invités d'Azure et sur la façon de déterminer si vous êtes concerné"
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 37b422e9-0713-4a81-a942-f553ef478064
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 5/21/2017
ms.author: raiye
ms.openlocfilehash: 3178a09dab1cb972a3460d54dc9908fb95cce68b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="guest-os-family-1-retirement-notice"></a><span data-ttu-id="03315-103">Informations relatives à la suppression de la famille 1 des systèmes d’exploitation invités</span><span class="sxs-lookup"><span data-stu-id="03315-103">Guest OS Family 1 retirement notice</span></span>
<span data-ttu-id="03315-104">La suppression de la famille 1 des systèmes d'exploitation a été annoncée le 1er juin 2013.</span><span class="sxs-lookup"><span data-stu-id="03315-104">The retirement of OS Family 1 was first announced on June 1, 2013.</span></span>

<span data-ttu-id="03315-105">**2 septembre 2014** La famille 1.x des systèmes d'exploitation invités (SE invités) d'Azure, qui est basée sur le système d'exploitation Windows Server 2008, a été officiellement supprimée.</span><span class="sxs-lookup"><span data-stu-id="03315-105">**Sept 2, 2014** The Azure Guest operating system (Guest OS) Family 1.x, which is based on the Windows Server 2008 operating system, was officially retired.</span></span> <span data-ttu-id="03315-106">Toutes les tentatives de déploiement de nouveaux services ou de mise à niveau des services existants à l'aide de la famille 1 échoueront, et un message d'erreur vous informera que la famille 1 des systèmes d'exploitation invités a été supprimée.</span><span class="sxs-lookup"><span data-stu-id="03315-106">All attempts to deploy new services or upgrade existing services using Family 1 will fail with an error message informing you that the Guest OS Family 1 has been retired.</span></span>

<span data-ttu-id="03315-107">**3 novembre 2014** La prise en charge étendue de la famille 1 des SE invités a pris fin et a été complètement supprimée.</span><span class="sxs-lookup"><span data-stu-id="03315-107">**November 3, 2014** Extended support for Guest OS Family 1 ended and it is fully retired.</span></span> <span data-ttu-id="03315-108">Tous les services toujours liés à la famille 1 seront affectés.</span><span class="sxs-lookup"><span data-stu-id="03315-108">All services still on Family 1 will be impacted.</span></span> <span data-ttu-id="03315-109">Nous pouvons arrêter ces services à tout moment.</span><span class="sxs-lookup"><span data-stu-id="03315-109">We may stop those services at any time.</span></span> <span data-ttu-id="03315-110">Il n'existe aucune garantie que vos services continueront de s'exécuter, sauf si vous les mettez à niveau manuellement vous-même.</span><span class="sxs-lookup"><span data-stu-id="03315-110">There is no guarantee your services will continue to run unless you manually upgrade them yourself.</span></span>

<span data-ttu-id="03315-111">Si vous avez d’autres questions, consultez les [Forums de services cloud](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) ou [contactez le support Azure](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="03315-111">If you have additional questions, visit the [Cloud Services Forums](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) or [contact Azure support](https://azure.microsoft.com/support/options/).</span></span>

## <a name="are-you-affected"></a><span data-ttu-id="03315-112">Êtes-vous concerné ?</span><span class="sxs-lookup"><span data-stu-id="03315-112">Are you affected?</span></span>
<span data-ttu-id="03315-113">Vos services cloud sont concernés si l'une des conditions suivantes s'applique :</span><span class="sxs-lookup"><span data-stu-id="03315-113">Your Cloud Services are affected if any one of the following applies:</span></span>

1. <span data-ttu-id="03315-114">Vous avez une valeur de « osFamily = "1" » explicitement spécifiée dans le fichier ServiceConfiguration.cscfg pour votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="03315-114">You have a value of "osFamily = "1" explicitly specified in the ServiceConfiguration.cscfg file for your Cloud Service.</span></span>
2. <span data-ttu-id="03315-115">Vous n'avez pas de valeur pour osFamily explicitement spécifiée dans le fichier ServiceConfiguration.cscfg pour votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="03315-115">You do not have a value for osFamily explicitly specified in the ServiceConfiguration.cscfg file for your Cloud Service.</span></span> <span data-ttu-id="03315-116">Actuellement, le système utilise la valeur par défaut « 1 » dans ce cas.</span><span class="sxs-lookup"><span data-stu-id="03315-116">Currently, the system uses the default value of "1" in this case.</span></span>
3. <span data-ttu-id="03315-117">Le portail Azure répertorie votre valeur de famille des systèmes d’exploitation invités en tant que « Windows Server 2008 ».</span><span class="sxs-lookup"><span data-stu-id="03315-117">The Azure portal lists your Guest Operating System family value as "Windows Server 2008".</span></span>

<span data-ttu-id="03315-118">Pour connaître la famille de systèmes d’exploitation exécutée par les services cloud, vous pouvez exécuter le script suivant dans Azure PowerShell. Vous devrez toutefois commencer par [configurer Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="03315-118">To find which of your cloud services are running which OS Family, you can run the following script in Azure PowerShell, though you must [set up Azure PowerShell](/powershell/azureps-cmdlets-docs) first.</span></span> <span data-ttu-id="03315-119">Pour plus d’informations sur le script, consultez [Fin de vie de la famille 1 des SE invités d'Azure : juin 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).</span><span class="sxs-lookup"><span data-stu-id="03315-119">For more information on the script, see [Azure Guest OS Family 1 End of Life: June 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).</span></span>

```Powershell
foreach($subscription in Get-AzureSubscription) {
    Select-AzureSubscription -SubscriptionName $subscription.SubscriptionName

    $deployments=get-azureService | get-azureDeployment -ErrorAction Ignore | where {$_.SdkVersion -NE ""}

    $deployments | ft @{Name="SubscriptionName";Expression={$subscription.SubscriptionName}}, ServiceName, SdkVersion, Slot, @{Name="osFamily";Expression={(select-xml -content $_.configuration -xpath "/ns:ServiceConfiguration/@osFamily" -namespace $namespace).node.value }}, osVersion, Status, URL
}
```

<span data-ttu-id="03315-120">Vos services cloud seront affectés par la suppression de la famille 1 si la colonne osFamily de la sortie du script est vide ou contient « 1 ».</span><span class="sxs-lookup"><span data-stu-id="03315-120">Your cloud services will be impacted by OS Family 1 retirement if the osFamily column in the script output is empty or contains a "1".</span></span>

## <a name="recommendations-if-you-are-affected"></a><span data-ttu-id="03315-121">Recommandations si vous êtes concerné</span><span class="sxs-lookup"><span data-stu-id="03315-121">Recommendations if you are affected</span></span>
<span data-ttu-id="03315-122">Nous vous recommandons de migrer vos rôles de service cloud vers l'une des familles de SE invités prises en charge :</span><span class="sxs-lookup"><span data-stu-id="03315-122">We recommend you migrate your Cloud Service roles to one of the supported Guest OS Families:</span></span>

<span data-ttu-id="03315-123">**Famille 4.x du SE invité** - Windows Server 2012 R2 *(recommandé)*</span><span class="sxs-lookup"><span data-stu-id="03315-123">**Guest OS family 4.x** - Windows Server 2012 R2 *(recommended)*</span></span>

1. <span data-ttu-id="03315-124">Assurez-vous que votre application utilise SDK 2.1 ou une version ultérieure avec .NET framework 4.0, 4.5 ou 4.5.1.</span><span class="sxs-lookup"><span data-stu-id="03315-124">Ensure that your application is using SDK 2.1 or later with .NET framework 4.0, 4.5 or 4.5.1.</span></span>
2. <span data-ttu-id="03315-125">Définissez l'attribut osFamily sur « 4 » dans le fichier ServiceConfiguration.cscfg et redéployez votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="03315-125">Set the osFamily attribute to “4” in the ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="03315-126">**Famille 3.x du SE invité** - Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="03315-126">**Guest OS family 3.x** - Windows Server 2012</span></span>

1. <span data-ttu-id="03315-127">Assurez-vous que votre application utilise SDK 1.8 ou une version ultérieure avec .NET framework 4.0 ou 4.5.</span><span class="sxs-lookup"><span data-stu-id="03315-127">Ensure that your application is using SDK 1.8 or later with .NET framework 4.0 or 4.5.</span></span>
2. <span data-ttu-id="03315-128">Définissez l'attribut osFamily sur « 3 » dans le fichier ServiceConfiguration.cscfg et redéployez votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="03315-128">Set the osFamily attribute to “3” in the ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="03315-129">**Famille 2.x du SE invité** - Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="03315-129">**Guest OS family 2.x** - Windows Server 2008 R2</span></span>

1. <span data-ttu-id="03315-130">Assurez-vous que votre application utilise SDK 1.3 ou une version ultérieure avec .NET framework 3.5 ou 4.0.</span><span class="sxs-lookup"><span data-stu-id="03315-130">Ensure that your application is using SDK 1.3 and above with .NET framework 3.5 or 4.0.</span></span>
2. <span data-ttu-id="03315-131">Définissez l'attribut osFamily sur « 2 » dans le fichier ServiceConfiguration.cscfg et redéployez votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="03315-131">Set the osFamily attribute to "2" in the ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

## <a name="extended-support-for-guest-os-family-1-ended-nov-3-2014"></a><span data-ttu-id="03315-132">Fin de la prise en charge étendue pour la famille 1 des SE invités depuis le 3 novembre 2014</span><span class="sxs-lookup"><span data-stu-id="03315-132">Extended Support for Guest OS Family 1 ended Nov 3, 2014</span></span>
<span data-ttu-id="03315-133">Les services cloud de la famille 1 des SE invités ne sont plus pris en charge.</span><span class="sxs-lookup"><span data-stu-id="03315-133">Cloud services on Guest OS family 1 are no longer supported.</span></span> <span data-ttu-id="03315-134">Quittez la famille 1 dès que possible pour éviter toute interruption de service.</span><span class="sxs-lookup"><span data-stu-id="03315-134">Migrate off family 1 as soon as possible to avoid service disruption.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="03315-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="03315-135">Next steps</span></span>
<span data-ttu-id="03315-136">Consultez les dernières [versions du système d’exploitation invité](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="03315-136">Review the latest [Guest OS releases](cloud-services-guestos-update-matrix.md).</span></span>
