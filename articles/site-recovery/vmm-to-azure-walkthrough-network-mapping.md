---
title: "le mappage réseau aaaConfigure pour répliquer des ordinateurs virtuels Hyper-V dans VMM nuages tooAzure avec Azure Site Recovery | Documents Microsoft"
description: "Décrit comment le mappage réseau tooconfigure lors de la réplication des ordinateurs virtuels Hyper-V dans VMM nuages tooAzure avec Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 081a9fdb0ffa4114099e9bcb9c1b1e43ad26ecbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-configure-network-mapping-for-hyper-v-replication-with-vmm-tooazure"></a><span data-ttu-id="c2c19-103">Étape 9 : Configurer le mappage réseau pour tooAzure de réplication (avec VMM) Hyper-V</span><span class="sxs-lookup"><span data-stu-id="c2c19-103">Step 9: Configure network mapping for Hyper-V replication (with VMM) tooAzure</span></span>

<span data-ttu-id="c2c19-104">Après avoir configuré hello [les paramètres de réplication source et cible](vmm-to-azure-walkthrough-source-target.md), utilisez cette toomap de mappage de l’article tooconfigure réseau entre les réseaux d’ordinateurs virtuels VMM local et les réseaux Azure.</span><span class="sxs-lookup"><span data-stu-id="c2c19-104">After you set up hello [source and target replication settings](vmm-to-azure-walkthrough-source-target.md), use this article tooconfigure network mapping toomap between on-premises VMM VM networks, and Azure networks.</span></span>

<span data-ttu-id="c2c19-105">Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="c2c19-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="c2c19-106">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="c2c19-106">Before you start</span></span>

- <span data-ttu-id="c2c19-107">En savoir plus sur le [mappage réseau](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span><span class="sxs-lookup"><span data-stu-id="c2c19-107">Learn about [network mapping](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span></span>
- <span data-ttu-id="c2c19-108">[Préparez VMM pour le mappage réseau](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping).</span><span class="sxs-lookup"><span data-stu-id="c2c19-108">[Prepare VMM for network mapping](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping).</span></span> 
- <span data-ttu-id="c2c19-109">Vérifiez que les ordinateurs virtuels sur le serveur VMM de hello sont connectés tooa réseau d’ordinateurs virtuels et que vous avez créé au moins un réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="c2c19-109">Verify that virtual machines on hello VMM server are connected tooa VM network, and that you've created at least one Azure virtual network.</span></span> <span data-ttu-id="c2c19-110">Plusieurs réseaux d’ordinateurs virtuels peuvent être mappés tooa réseau Azure unique.</span><span class="sxs-lookup"><span data-stu-id="c2c19-110">Multiple VM networks can be mapped tooa single Azure network.</span></span>

## <a name="configure-mapping"></a><span data-ttu-id="c2c19-111">Configuration du mappage</span><span class="sxs-lookup"><span data-stu-id="c2c19-111">Configure mapping</span></span>

<span data-ttu-id="c2c19-112">Configurez le mappage comme suit :</span><span class="sxs-lookup"><span data-stu-id="c2c19-112">Configure mapping as follows:</span></span>

1. <span data-ttu-id="c2c19-113">Dans **Infrastructure Site Recovery** > **réseau mappages** > **mappage réseau**, cliquez sur hello **+ mappage réseau**  icône.</span><span class="sxs-lookup"><span data-stu-id="c2c19-113">In **Site Recovery Infrastructure** > **Network mappings** > **Network Mapping**, click hello **+Network Mapping** icon.</span></span>

    ![Mappage réseau](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping1.png)
2. <span data-ttu-id="c2c19-115">Dans **ajouter le mappage réseau**, sélectionnez serveur VMM source à hello, et **Azure** comme cible de hello.</span><span class="sxs-lookup"><span data-stu-id="c2c19-115">In **Add network mapping**, select hello source VMM server, and **Azure** as hello target.</span></span>
3. <span data-ttu-id="c2c19-116">Vérifiez l’abonnement de hello et le modèle de déploiement hello après le basculement.</span><span class="sxs-lookup"><span data-stu-id="c2c19-116">Verify hello subscription and hello deployment model after failover.</span></span>
4. <span data-ttu-id="c2c19-117">Dans **réseau Source**, sélectionnez le réseau d’ordinateurs virtuels de hello source locale que vous souhaitez toomap à partir de la liste hello associé avec le serveur VMM de hello.</span><span class="sxs-lookup"><span data-stu-id="c2c19-117">In **Source network**, select hello source on-premises VM network you want toomap from hello list associated with hello VMM server.</span></span>
5. <span data-ttu-id="c2c19-118">Dans **réseau cible**, sélectionnez hello réseau Azure dans le réplica de machines virtuelles Azure se trouve lorsqu’elles sont créées.</span><span class="sxs-lookup"><span data-stu-id="c2c19-118">In **Target network**, select hello Azure network in which replica Azure VMs will be located when they're created.</span></span> <span data-ttu-id="c2c19-119">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="c2c19-119">Then click **OK**.</span></span>

    ![Mappage réseau](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping2.png)

<span data-ttu-id="c2c19-121">Voici le processus exécuté lorsque le mappage réseau démarre :</span><span class="sxs-lookup"><span data-stu-id="c2c19-121">Here's what happens when network mapping begins:</span></span>

* <span data-ttu-id="c2c19-122">Machines virtuelles existantes sur le réseau d’ordinateurs virtuels hello source sont réseau cible de toohello connecté au commencement de mappage.</span><span class="sxs-lookup"><span data-stu-id="c2c19-122">Existing VMs on hello source VM network are connected toohello target network when mapping begins.</span></span> <span data-ttu-id="c2c19-123">Réseau d’ordinateurs virtuels source nouvelles machines virtuelles connectés toohello connectés toohello mappé réseau Azure lors de la réplication a lieu.</span><span class="sxs-lookup"><span data-stu-id="c2c19-123">New VMs connected toohello source VM network are connected toohello mapped Azure network when replication occurs.</span></span>
* <span data-ttu-id="c2c19-124">Si vous modifiez un mappage réseau existant, les machines virtuelles de réplication se connecter à l’aide de nouveaux paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="c2c19-124">If you modify an existing network mapping, replica virtual machines connect using hello new settings.</span></span>
* <span data-ttu-id="c2c19-125">Si le réseau cible de hello possède plusieurs sous-réseaux, et un de ces sous-réseaux a hello le même nom que le sous-réseau sur lequel virtual machine de hello source se trouve, puis hello ordinateur virtuel se connecte le sous-réseau de toothat cible après le basculement.</span><span class="sxs-lookup"><span data-stu-id="c2c19-125">If hello target network has multiple subnets, and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine connects toothat target subnet after failover.</span></span>
* <span data-ttu-id="c2c19-126">S’il n’existe aucun sous-réseau cible avec un nom correspondant, ordinateur virtuel de hello se connecte toohello premier sous-réseau de réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="c2c19-126">If there’s no target subnet with a matching name, hello virtual machine connects toohello first subnet in hello network.</span></span>



## <a name="next-steps"></a><span data-ttu-id="c2c19-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c2c19-127">Next steps</span></span>

<span data-ttu-id="c2c19-128">Accédez trop[étape 10 : créer une stratégie de réplication](vmm-to-azure-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="c2c19-128">Go too[Step 10: Create a replication policy](vmm-to-azure-walkthrough-replication.md)</span></span>
