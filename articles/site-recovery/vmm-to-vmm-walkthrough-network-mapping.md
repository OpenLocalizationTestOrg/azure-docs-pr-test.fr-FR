---
title: "réseaux aaaMap pour le site secondaire de la tooa de réplication d’ordinateur virtuel Hyper-V avec Azure Site Recovery | Documents Microsoft"
description: "Décrit comment les réseaux toomap lors de la réplication des ordinateurs virtuels Hyper-V tooa site VMM secondaire avec Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 461b7c1c-ef61-4005-aeec-2324e727a3d0
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: d4f621df4ce08ae055bc6809daea0b71b76754ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-map-networks-for-hyper-v-vm-replication-tooa-secondary-site"></a><span data-ttu-id="7c833-103">Étape 7 : Mapper les réseaux pour le site secondaire de machine virtuelle Hyper-V réplication tooa</span><span class="sxs-lookup"><span data-stu-id="7c833-103">Step 7: Map networks for Hyper-V VM replication tooa secondary site</span></span>


<span data-ttu-id="7c833-104">Après avoir configuré [paramètres source et cible](vmm-to-vmm-walkthrough-source-target.md) pour répliquer le site de System Center Virtual Machine Manager (VMM) secondaire Hyper-V machines virtuelles (VM) tooa, utiliser ce mappage article tooconfigure réseau virtuel Hyper-V tooa de réplication de machine (VM) secondaire du site, à l’aide de [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7c833-104">After setting up [source and target settings](vmm-to-vmm-walkthrough-source-target.md) for replicating Hyper-V virtual machines (VMs) tooa secondary System Center Virtual Machine Manager (VMM) site, use this article tooconfigure network mapping for Hyper-V virtual machine (VM) replication tooa secondary site, using  [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="7c833-105">Après avoir lu cet article, validez les commentaires au bas de hello, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="7c833-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="7c833-106">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="7c833-106">Before you start</span></span>

- <span data-ttu-id="7c833-107">En savoir plus sur le [mappage réseau](vmm-to-vmm-walkthrough-network.md#network-mapping-overview) avant de démarrer.</span><span class="sxs-lookup"><span data-stu-id="7c833-107">Learn about [network mapping](vmm-to-vmm-walkthrough-network.md#network-mapping-overview) before you start.</span></span>
- <span data-ttu-id="7c833-108">Vérifiez que les ordinateurs virtuels sur les serveurs VMM sont connectés tooa réseau d’ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="7c833-108">Verify that virtual machines on VMM servers are connected tooa VM network.</span></span>

## <a name="configure-network-mapping"></a><span data-ttu-id="7c833-109">Configurer le mappage réseau</span><span class="sxs-lookup"><span data-stu-id="7c833-109">Configure network mapping</span></span>

1. <span data-ttu-id="7c833-110">Dans **Mappage réseau** > **Mappages réseau**, cliquez sur **+Mappage réseau**.</span><span class="sxs-lookup"><span data-stu-id="7c833-110">In **Network Mapping** > **Network mappings**, click **+Network Mapping**.</span></span>
2. <span data-ttu-id="7c833-111">Dans **ajouter le mappage réseau** , sélectionnez la source de hello et serveurs VMM cible.</span><span class="sxs-lookup"><span data-stu-id="7c833-111">In **Add network mapping** tab, select hello source and target VMM servers.</span></span> <span data-ttu-id="7c833-112">réseaux d’ordinateurs virtuels Hello associés aux serveurs VMM de hello sont récupérés.</span><span class="sxs-lookup"><span data-stu-id="7c833-112">hello VM networks associated with hello VMM servers are retrieved.</span></span>
3. <span data-ttu-id="7c833-113">Dans **réseau Source**, sélectionnez réseau hello toouse à partir de la liste de hello des réseaux d’ordinateurs virtuels associé avec le serveur VMM principal de hello.</span><span class="sxs-lookup"><span data-stu-id="7c833-113">In **Source network**, select hello network you want toouse from hello list of VM networks associated with hello primary VMM server.</span></span>
4. <span data-ttu-id="7c833-114">Dans **réseau cible**, sélectionnez réseau hello toouse sur le serveur VMM secondaire de hello.</span><span class="sxs-lookup"><span data-stu-id="7c833-114">In **Target network**, select hello network you want toouse on hello secondary VMM server.</span></span> <span data-ttu-id="7c833-115">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7c833-115">Then click **OK**.</span></span>

    ![Mappage réseau](./media/vmm-to-vmm-walkthrough-network-mapping/network-mapping2.png)

<span data-ttu-id="7c833-117">Voici le processus exécuté lorsque le mappage réseau démarre :</span><span class="sxs-lookup"><span data-stu-id="7c833-117">Here's what happens when network mapping begins:</span></span>

* <span data-ttu-id="7c833-118">Les ordinateurs virtuels réplica existants qui correspondent le réseau d’ordinateurs virtuels toohello source sera réseau d’ordinateurs virtuels connectés toohello cible.</span><span class="sxs-lookup"><span data-stu-id="7c833-118">Any existing replica virtual machines that correspond toohello source VM network will be connected toohello target VM network.</span></span>
* <span data-ttu-id="7c833-119">Nouveaux ordinateurs virtuels qui sont le réseau d’ordinateurs virtuels connectés toohello source sera connecté toohello réseau cible après la réplication.</span><span class="sxs-lookup"><span data-stu-id="7c833-119">New virtual machines that are connected toohello source VM network will be connected toohello target mapped network after replication.</span></span>
* <span data-ttu-id="7c833-120">Si vous modifiez un mappage existant avec un nouveau réseau, les machines virtuelles de réplication sera connectées à l’aide de nouveaux paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="7c833-120">If you modify an existing mapping with a new network, replica virtual machines will be connected using hello new settings.</span></span>
* <span data-ttu-id="7c833-121">Si le réseau cible de hello possède plusieurs sous-réseaux et d’un de ces sous-réseaux a hello trouve du même nom que le sous-réseau sur lequel hello source virtual machine, puis hello ordinateur virtuel sera connecté toothat cible sous-réseau après le basculement.</span><span class="sxs-lookup"><span data-stu-id="7c833-121">If hello target network has multiple subnets and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after failover.</span></span> <span data-ttu-id="7c833-122">S’il n’existe aucun sous-réseau cible avec un nom correspondant, ordinateur virtuel de hello sera connecté toohello premier sous-réseau de réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="7c833-122">If there’s no target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>



## <a name="next-steps"></a><span data-ttu-id="7c833-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7c833-123">Next steps</span></span>

<span data-ttu-id="7c833-124">Accédez trop[étape 8 : configurer une stratégie de réplication](vmm-to-vmm-walkthrough-replication.md).</span><span class="sxs-lookup"><span data-stu-id="7c833-124">Go too[Step 8: Configure a replication policy](vmm-to-vmm-walkthrough-replication.md).</span></span>
