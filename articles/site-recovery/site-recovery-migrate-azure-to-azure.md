---
title: "machines virtuelles Azure IaaS d’aaaMigrate entre les régions Azure | Documents Microsoft"
description: "Utilisez Azure IaaS Azure Site Recovery toomigrate virtuels à partir d’une région Azure tooanother."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8a29e0d9-0010-4739-972f-02b8bdf360f6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: c84dc77716b8d19969eab60707ed1332ca39b893
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-iaas-virtual-machines-between-azure-regions-with-azure-site-recovery"></a><span data-ttu-id="26765-103">Migrer des machines virtuelles IaaS Azure entre différentes régions Azure avec Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="26765-103">Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery</span></span>
## <a name="overview"></a><span data-ttu-id="26765-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="26765-104">Overview</span></span>
<span data-ttu-id="26765-105">Récupération de Site de tooAzure Bienvenue !</span><span class="sxs-lookup"><span data-stu-id="26765-105">Welcome tooAzure Site Recovery!</span></span> <span data-ttu-id="26765-106">Utilisez cet article si vous souhaitez que les machines virtuelles Azure de toomigrate entre les régions Azure.</span><span class="sxs-lookup"><span data-stu-id="26765-106">Use this article if you want toomigrate Azure VMs between Azure regions.</span></span> <span data-ttu-id="26765-107">Avant de commencer, notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="26765-107">Before you start, note that:</span></span>

* <span data-ttu-id="26765-108">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : Azure Resource Manager et classique.</span><span class="sxs-lookup"><span data-stu-id="26765-108">Azure has two different deployment models for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="26765-109">Azure a également deux portails : hello portail classique Azure qui prend en charge le modèle de déploiement classique hello et hello portail Azure avec prise en charge pour les deux modèles de déploiement.</span><span class="sxs-lookup"><span data-stu-id="26765-109">Azure also has two portals – hello Azure classic portal that supports hello classic deployment model, and hello Azure portal with support for both deployment models.</span></span> <span data-ttu-id="26765-110">les étapes de base Hello pour la migration sont hello même si vous configurez la récupération de Site dans le Gestionnaire de ressources ou standard.</span><span class="sxs-lookup"><span data-stu-id="26765-110">hello basic steps for migration are hello same whether you're configuring Site Recovery in Resource Manager or in classic.</span></span> <span data-ttu-id="26765-111">Hello toutefois les instructions de l’interface utilisateur et des captures d’écran dans cet article sont pertinentes pour hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="26765-111">However hello UI instructions and screenshots in this article are relevant for hello Azure portal.</span></span>
* <span data-ttu-id="26765-112">**Actuellement vous pouvez uniquement migrer d’une région tooanother. Vous pouvez basculer des machines virtuelles à partir d’une région Azure tooanother, mais vous ne pouvez pas restaurer les à nouveau.**</span><span class="sxs-lookup"><span data-stu-id="26765-112">**Currently you can only migrate from one region tooanother. You can fail over VMs from one Azure region tooanother, but you can't fail them back again.**</span></span>

<span data-ttu-id="26765-113">Valider des commentaires ou des questions au bas de hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="26765-113">Post any comments or questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26765-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="26765-114">Prerequisites</span></span>
<span data-ttu-id="26765-115">Voici ce dont vous avez besoin pour ce déploiement :</span><span class="sxs-lookup"><span data-stu-id="26765-115">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="26765-116">**Machines virtuelles IaaS**: hello des machines virtuelles que vous souhaitez toomigrate.</span><span class="sxs-lookup"><span data-stu-id="26765-116">**IaaS virtual machines**: hello VMs you want toomigrate.</span></span> <span data-ttu-id="26765-117">Vous migrez ces machines virtuelles en les traitant comme des machines physiques.</span><span class="sxs-lookup"><span data-stu-id="26765-117">You migrate these VMs by treating them as physical machines.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="26765-118">Étapes du déploiement</span><span class="sxs-lookup"><span data-stu-id="26765-118">Deployment steps</span></span>
<span data-ttu-id="26765-119">Cette section décrit les étapes de déploiement hello dans le nouveau portail de Azure hello.</span><span class="sxs-lookup"><span data-stu-id="26765-119">This section describes hello deployment steps in hello new Azure portal.</span></span>

1. <span data-ttu-id="26765-120">[Créer un coffre](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="26765-120">[Create a vault](site-recovery-vmware-to-azure.md).</span></span>
2. <span data-ttu-id="26765-121">[Activer la réplication](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="26765-121">[Enable replication](site-recovery-vmware-to-azure.md).</span></span> <span data-ttu-id="26765-122">Activer la réplication pour hello machines virtuelles, vous souhaitez toomigrate, choisissez Azure en tant que source.</span><span class="sxs-lookup"><span data-stu-id="26765-122">Enable replication for hello VMs you want toomigrate, and choose Azure as source.</span></span> 
3. <span data-ttu-id="26765-123">[ Exécuter un basculement non planifié](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="26765-123">[ Run an unplanned failover](site-recovery-failover.md).</span></span> <span data-ttu-id="26765-124">Une fois la réplication initiale terminée, vous pouvez exécuter un basculement non planifié à partir d’une région Azure tooanother.</span><span class="sxs-lookup"><span data-stu-id="26765-124">After initial replication is complete, you can run an unplanned failover from one Azure region tooanother.</span></span> <span data-ttu-id="26765-125">Si vous le souhaitez, vous pouvez créer un plan de récupération et exécuter un basculement non planifié, toomigrate plusieurs ordinateurs virtuels entre les régions.</span><span class="sxs-lookup"><span data-stu-id="26765-125">Optionally, you can create a recovery plan and run an unplanned failover, toomigrate multiple virtual machines between regions.</span></span> <span data-ttu-id="26765-126">[Découvrez d’autres informations](site-recovery-create-recovery-plans.md) sur les plans de récupération.</span><span class="sxs-lookup"><span data-stu-id="26765-126">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26765-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="26765-127">Next steps</span></span>
<span data-ttu-id="26765-128">Découvrez les autres scénarios de réplication dans [Qu’est-ce que le service Azure Site Recovery ?](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="26765-128">Learn more about other replication scenarios in [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>
