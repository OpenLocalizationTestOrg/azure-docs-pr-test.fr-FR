---
title: "outils d’aaaCommunity - déplacer les ressources classiques tooAzure Gestionnaire de ressources | Documents Microsoft"
description: "Cet outils hello de catalogues article qui ont été fournis par hello Communauté toohelp migrer les ressources IaaS à partir du modèle de déploiement d’Azure Resource Manager toohello classique."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 228b697b-3950-49f5-84bb-283bb56621b1
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 67d5624a14d12a2d9eb46eb12aef461b706d4589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="community-tools-toomigrate-iaas-resources-from-classic-tooazure-resource-manager"></a><span data-ttu-id="4d0b0-103">Communauté Outils ressources IaaS toomigrate classique tooAzure Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="4d0b0-103">Community tools toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>
<span data-ttu-id="4d0b0-104">Cet article catalogues hello les outils qui ont été fournis par hello Communauté tooassist avec la migration des ressources IaaS à partir du modèle de déploiement d’Azure Resource Manager toohello classique.</span><span class="sxs-lookup"><span data-stu-id="4d0b0-104">This article catalogs hello tools that have been provided by hello community tooassist with migration of IaaS resources from classic toohello Azure Resource Manager deployment model.</span></span>

> [!NOTE]
> <span data-ttu-id="4d0b0-105">Ces outils ne sont pas pris en charge officiellement par le Support Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4d0b0-105">These tools are not officially supported by Microsoft Support.</span></span> <span data-ttu-id="4d0b0-106">Par conséquent, ils sont open source sur GitHub et nous sommes réservations persistantes de tooaccept heureux de correctifs ou des scénarios supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="4d0b0-106">Therefore they are open sourced on GitHub and we're happy tooaccept PRs for fixes or additional scenarios.</span></span> <span data-ttu-id="4d0b0-107">tooreport un problème, utilisez hello GitHub problèmes de fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="4d0b0-107">tooreport an issue, use hello GitHub issues feature.</span></span>
> 
> <span data-ttu-id="4d0b0-108">Une migration avec ces outils entraînera un temps d’arrêt pour votre machine virtuelle Classic.</span><span class="sxs-lookup"><span data-stu-id="4d0b0-108">Migrating with these tools will cause downtime for your classic Virtual Machine.</span></span> <span data-ttu-id="4d0b0-109">Si vous souhaitez effectuer une migration prise en charge par la plateforme, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="4d0b0-109">If you're looking for platform supported migration, visit</span></span> 
> 
>   * [<span data-ttu-id="4d0b0-110">Plateforme prise en charge la migration des ressources IaaS à partir de la pile de Resource Manager tooAzure classique</span><span class="sxs-lookup"><span data-stu-id="4d0b0-110">Platform supported migration of IaaS resources from Classic tooAzure Resource Manager stack</span></span>](migration-classic-resource-manager-overview.md)
>   * [<span data-ttu-id="4d0b0-111">Techniques détaillées sur la plateforme prise en charge la migration à partir de classique tooAzure Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="4d0b0-111">Technical Deep Dive on Platform supported migration from Classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md)
>   * [<span data-ttu-id="4d0b0-112">Migrer les ressources IaaS classique tooAzure Gestionnaire de ressources à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4d0b0-112">Migrate IaaS resources from Classic tooAzure Resource Manager using Azure PowerShell</span></span>](migration-classic-resource-manager-ps.md)
> 
> 

## <a name="asmmetadataparser"></a><span data-ttu-id="4d0b0-113">AsmMetadataParser</span><span class="sxs-lookup"><span data-stu-id="4d0b0-113">AsmMetadataParser</span></span>
<span data-ttu-id="4d0b0-114">Il s’agit d’un ensemble d’outils d’assistance créé dans le cadre de migrations d’entreprise à partir de la gestion des services Azure tooAzure Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="4d0b0-114">This is a collection of helper tools created as part of enterprise migrations from Azure Service Management tooAzure Resource Manager.</span></span> <span data-ttu-id="4d0b0-115">Cet outil vous permet de tooreplicate votre infrastructure dans un autre abonnement qui peut être utilisé pour vérifier la migration et tous les points de fer avant d’exécuter la migration hello sur votre abonnement de Production.</span><span class="sxs-lookup"><span data-stu-id="4d0b0-115">This tool allows you tooreplicate your infrastructure into another subscription which can be used for testing migration and iron out any issues before running hello migration on your Production subscription.</span></span>

[<span data-ttu-id="4d0b0-116">Documentation de l’outil lien toohello</span><span class="sxs-lookup"><span data-stu-id="4d0b0-116">Link toohello tool documentation</span></span>](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/AsmToArmMigrationApiToolset)

## <a name="migaz"></a><span data-ttu-id="4d0b0-117">migAz</span><span class="sxs-lookup"><span data-stu-id="4d0b0-117">migAz</span></span>
<span data-ttu-id="4d0b0-118">migAz est une option supplémentaire de toomigrate un ensemble complet de ressources de Resource Manager IaaS tooAzure de ressources IaaS classiques.</span><span class="sxs-lookup"><span data-stu-id="4d0b0-118">migAz is an additional option toomigrate a complete set of classic IaaS resources tooAzure Resource Manager IaaS resources.</span></span> <span data-ttu-id="4d0b0-119">Hello migration peut se produire dans hello même abonnement ou entre différents abonnements et les types d’abonnements (ex : les abonnements CSP).</span><span class="sxs-lookup"><span data-stu-id="4d0b0-119">hello migration can occur within hello same subscription or between different subscriptions and subscription types (ex: CSP subscriptions).</span></span>

[<span data-ttu-id="4d0b0-120">Documentation de l’outil lien toohello</span><span class="sxs-lookup"><span data-stu-id="4d0b0-120">Link toohello tool documentation</span></span>](https://github.com/Azure/migAz)

## <a name="next-steps"></a><span data-ttu-id="4d0b0-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4d0b0-121">Next Steps</span></span>

* [<span data-ttu-id="4d0b0-122">Vue d’ensemble de la plateforme prise en charge la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="4d0b0-122">Overview of platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="4d0b0-123">Techniques détaillées sur la plateforme prise en charge la migration à partir de tooAzure classique Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="4d0b0-123">Technical deep dive on platform-supported migration from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="4d0b0-124">Planification de la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="4d0b0-124">Planning for migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="4d0b0-125">Utiliser les ressources IaaS PowerShell toomigrate classique tooAzure Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="4d0b0-125">Use PowerShell toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="4d0b0-126">Utiliser les ressources IaaS CLI toomigrate classique tooAzure Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="4d0b0-126">Use CLI toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="4d0b0-127">Passer en revue les erreurs courantes de migration</span><span class="sxs-lookup"><span data-stu-id="4d0b0-127">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="4d0b0-128">Hello de révision plus Forum aux questions sur la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="4d0b0-128">Review hello most frequently asked questions about migrating IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

