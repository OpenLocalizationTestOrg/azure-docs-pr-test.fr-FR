---
title: "Notez de retrait de 1 aaaGuest du système d’exploitation famille | Documents Microsoft"
description: "Fournit des informations sur lors de la mise hors service hello Azure invité famille 1 s’est produite et comment toodetermine si vous êtes concerné"
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
ms.openlocfilehash: fa8b904c6560dbbe4982c301f818c7a5cbc4eacb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="guest-os-family-1-retirement-notice"></a><span data-ttu-id="7d714-103">Informations relatives à la suppression de la famille 1 des systèmes d’exploitation invités</span><span class="sxs-lookup"><span data-stu-id="7d714-103">Guest OS Family 1 retirement notice</span></span>
<span data-ttu-id="7d714-104">retrait de Hello de la famille 1 a été annoncé le 1er juin 2013.</span><span class="sxs-lookup"><span data-stu-id="7d714-104">hello retirement of OS Family 1 was first announced on June 1, 2013.</span></span>

<span data-ttu-id="7d714-105">**2 septembre 2014** hello système de d’exploitation invité Azure (s’invité) famille 1.x, qui est basé sur le système d’exploitation de hello Windows Server 2008, a été officiellement supprimé.</span><span class="sxs-lookup"><span data-stu-id="7d714-105">**Sept 2, 2014** hello Azure Guest operating system (Guest OS) Family 1.x, which is based on hello Windows Server 2008 operating system, was officially retired.</span></span> <span data-ttu-id="7d714-106">Tous les services de nouvelles tentatives toodeploy ou mise à niveau des services existants à l’aide de la famille 1 échoue avec un message d’erreur vous informant que hello du système d’exploitation invités de famille 1 a été retirée.</span><span class="sxs-lookup"><span data-stu-id="7d714-106">All attempts toodeploy new services or upgrade existing services using Family 1 will fail with an error message informing you that hello Guest OS Family 1 has been retired.</span></span>

<span data-ttu-id="7d714-107">**3 novembre 2014** La prise en charge étendue de la famille 1 des SE invités a pris fin et a été complètement supprimée.</span><span class="sxs-lookup"><span data-stu-id="7d714-107">**November 3, 2014** Extended support for Guest OS Family 1 ended and it is fully retired.</span></span> <span data-ttu-id="7d714-108">Tous les services toujours liés à la famille 1 seront affectés.</span><span class="sxs-lookup"><span data-stu-id="7d714-108">All services still on Family 1 will be impacted.</span></span> <span data-ttu-id="7d714-109">Nous pouvons arrêter ces services à tout moment.</span><span class="sxs-lookup"><span data-stu-id="7d714-109">We may stop those services at any time.</span></span> <span data-ttu-id="7d714-110">Il n’existe aucune garantie que vos services continueront toorun, sauf si vous mettre à niveau manuellement les vous-même.</span><span class="sxs-lookup"><span data-stu-id="7d714-110">There is no guarantee your services will continue toorun unless you manually upgrade them yourself.</span></span>

<span data-ttu-id="7d714-111">Si vous avez des questions supplémentaires, visitez hello [Forums des Services Cloud](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) ou [contactez le support Azure](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="7d714-111">If you have additional questions, visit hello [Cloud Services Forums](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) or [contact Azure support](https://azure.microsoft.com/support/options/).</span></span>

## <a name="are-you-affected"></a><span data-ttu-id="7d714-112">Êtes-vous concerné ?</span><span class="sxs-lookup"><span data-stu-id="7d714-112">Are you affected?</span></span>
<span data-ttu-id="7d714-113">Vos Services Cloud sont affectées si l’un des éléments suivants de hello s’applique :</span><span class="sxs-lookup"><span data-stu-id="7d714-113">Your Cloud Services are affected if any one of hello following applies:</span></span>

1. <span data-ttu-id="7d714-114">Vous avez une valeur de « osFamily = « 1 » explicitement spécifiée dans le fichier ServiceConfiguration.cscfg de hello pour votre Service Cloud.</span><span class="sxs-lookup"><span data-stu-id="7d714-114">You have a value of "osFamily = "1" explicitly specified in hello ServiceConfiguration.cscfg file for your Cloud Service.</span></span>
2. <span data-ttu-id="7d714-115">Il est inutile de valeur pour osFamily spécifié explicitement dans le fichier ServiceConfiguration.cscfg de hello pour votre Service Cloud.</span><span class="sxs-lookup"><span data-stu-id="7d714-115">You do not have a value for osFamily explicitly specified in hello ServiceConfiguration.cscfg file for your Cloud Service.</span></span> <span data-ttu-id="7d714-116">Actuellement, hello hello par défaut valeur par « 1 » dans ce cas.</span><span class="sxs-lookup"><span data-stu-id="7d714-116">Currently, hello system uses hello default value of "1" in this case.</span></span>
3. <span data-ttu-id="7d714-117">Hello portail Azure répertorie la valeur de votre famille de système d’exploitation invité en tant que « Windows Server 2008 ».</span><span class="sxs-lookup"><span data-stu-id="7d714-117">hello Azure portal lists your Guest Operating System family value as "Windows Server 2008".</span></span>

<span data-ttu-id="7d714-118">toofind qui sont en cours d’exécution quelle famille du système d’exploitation de vos services cloud, vous pouvez exécuter hello suivant le script dans Azure PowerShell, toutefois vous devez [configurer Azure PowerShell](/powershell/azureps-cmdlets-docs) première.</span><span class="sxs-lookup"><span data-stu-id="7d714-118">toofind which of your cloud services are running which OS Family, you can run hello following script in Azure PowerShell, though you must [set up Azure PowerShell](/powershell/azureps-cmdlets-docs) first.</span></span> <span data-ttu-id="7d714-119">Pour plus d’informations sur le script de hello, consultez [Azure invité du système d’exploitation famille 1 fin de vie : juin 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).</span><span class="sxs-lookup"><span data-stu-id="7d714-119">For more information on hello script, see [Azure Guest OS Family 1 End of Life: June 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).</span></span>

```Powershell
foreach($subscription in Get-AzureSubscription) {
    Select-AzureSubscription -SubscriptionName $subscription.SubscriptionName

    $deployments=get-azureService | get-azureDeployment -ErrorAction Ignore | where {$_.SdkVersion -NE ""}

    $deployments | ft @{Name="SubscriptionName";Expression={$subscription.SubscriptionName}}, ServiceName, SdkVersion, Slot, @{Name="osFamily";Expression={(select-xml -content $_.configuration -xpath "/ns:ServiceConfiguration/@osFamily" -namespace $namespace).node.value }}, osVersion, Status, URL
}
```

<span data-ttu-id="7d714-120">Vos services cloud seront affectées par la mise hors service de la famille 1 si la colonne osFamily de hello dans la sortie du script hello est vide ou contient des « 1 ».</span><span class="sxs-lookup"><span data-stu-id="7d714-120">Your cloud services will be impacted by OS Family 1 retirement if hello osFamily column in hello script output is empty or contains a "1".</span></span>

## <a name="recommendations-if-you-are-affected"></a><span data-ttu-id="7d714-121">Recommandations si vous êtes concerné</span><span class="sxs-lookup"><span data-stu-id="7d714-121">Recommendations if you are affected</span></span>
<span data-ttu-id="7d714-122">Nous vous conseillons de que migrer votre tooone de rôles de Service de cloud computing de familles de système d’exploitation invité hello pris en charge :</span><span class="sxs-lookup"><span data-stu-id="7d714-122">We recommend you migrate your Cloud Service roles tooone of hello supported Guest OS Families:</span></span>

<span data-ttu-id="7d714-123">**Famille 4.x du SE invité** - Windows Server 2012 R2 *(recommandé)*</span><span class="sxs-lookup"><span data-stu-id="7d714-123">**Guest OS family 4.x** - Windows Server 2012 R2 *(recommended)*</span></span>

1. <span data-ttu-id="7d714-124">Assurez-vous que votre application utilise SDK 2.1 ou une version ultérieure avec .NET framework 4.0, 4.5 ou 4.5.1.</span><span class="sxs-lookup"><span data-stu-id="7d714-124">Ensure that your application is using SDK 2.1 or later with .NET framework 4.0, 4.5 or 4.5.1.</span></span>
2. <span data-ttu-id="7d714-125">Définir le fichier ServiceConfiguration.cscfg de hello osFamily attribut hello en trop « 4 » et redéployez votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="7d714-125">Set hello osFamily attribute too“4” in hello ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="7d714-126">**Famille 3.x du SE invité** - Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="7d714-126">**Guest OS family 3.x** - Windows Server 2012</span></span>

1. <span data-ttu-id="7d714-127">Assurez-vous que votre application utilise SDK 1.8 ou une version ultérieure avec .NET framework 4.0 ou 4.5.</span><span class="sxs-lookup"><span data-stu-id="7d714-127">Ensure that your application is using SDK 1.8 or later with .NET framework 4.0 or 4.5.</span></span>
2. <span data-ttu-id="7d714-128">Définir le fichier ServiceConfiguration.cscfg trop « 3 » hello en hello osFamily attribut et redéployez votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="7d714-128">Set hello osFamily attribute too“3” in hello ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="7d714-129">**Famille 2.x du SE invité** - Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="7d714-129">**Guest OS family 2.x** - Windows Server 2008 R2</span></span>

1. <span data-ttu-id="7d714-130">Assurez-vous que votre application utilise SDK 1.3 ou une version ultérieure avec .NET framework 3.5 ou 4.0.</span><span class="sxs-lookup"><span data-stu-id="7d714-130">Ensure that your application is using SDK 1.3 and above with .NET framework 3.5 or 4.0.</span></span>
2. <span data-ttu-id="7d714-131">Définir le fichier ServiceConfiguration.cscfg de hello osFamily attribut hello en trop « 2 » et redéployez votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="7d714-131">Set hello osFamily attribute too"2" in hello ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

## <a name="extended-support-for-guest-os-family-1-ended-nov-3-2014"></a><span data-ttu-id="7d714-132">Fin de la prise en charge étendue pour la famille 1 des SE invités depuis le 3 novembre 2014</span><span class="sxs-lookup"><span data-stu-id="7d714-132">Extended Support for Guest OS Family 1 ended Nov 3, 2014</span></span>
<span data-ttu-id="7d714-133">Les services cloud de la famille 1 des SE invités ne sont plus pris en charge.</span><span class="sxs-lookup"><span data-stu-id="7d714-133">Cloud services on Guest OS family 1 are no longer supported.</span></span> <span data-ttu-id="7d714-134">Migrer la famille 1 dès que possible tooavoid toute interruption de service.</span><span class="sxs-lookup"><span data-stu-id="7d714-134">Migrate off family 1 as soon as possible tooavoid service disruption.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="7d714-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7d714-135">Next steps</span></span>
<span data-ttu-id="7d714-136">Hello révision dernières [mises à jour de système d’exploitation invité](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="7d714-136">Review hello latest [Guest OS releases](cloud-services-guestos-update-matrix.md).</span></span>
