---
title: "site secondaire tooa réplication aaaEnable Hyper-V avec Azure Site Recovery | Documents Microsoft"
description: "Décrit comment la réplication pour les ordinateurs virtuels Hyper-V en répliquant tooa tooenable System Center VMM secondaire du site avec Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d8782d14-9fef-4396-8912-ff945efc851b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: b4484e0118cb23f343187fe867d9795d30926baf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-enable-replication-tooa-secondary-site-for-hyper-v-vms"></a><span data-ttu-id="b401c-103">Étape 9 : Activer le site secondaire tooa de réplication pour les ordinateurs virtuels Hyper-V</span><span class="sxs-lookup"><span data-stu-id="b401c-103">Step 9: Enable replication tooa secondary site for Hyper-V VMs</span></span>


<span data-ttu-id="b401c-104">Après avoir configuré une stratégie de réplication, utiliser ce site secondaire System Center Virtual Machine Manager (VMM) article tooenable réplication tooa pour local Hyper-V virtuels (VM), à l’aide de [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b401c-104">After setting up a replication policy, use this article tooenable replication tooa secondary System Center Virtual Machine Manager (VMM) site for on-premises Hyper-V virtual machines (VM), using [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="b401c-105">Après avoir lu cet article, validez les commentaires au bas de hello, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="b401c-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="select-vms-tooreplicate"></a><span data-ttu-id="b401c-106">Sélectionnez tooreplicate de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="b401c-106">Select VMs tooreplicate</span></span>

1. <span data-ttu-id="b401c-107">Cliquez sur **Étape 2 : Répliquer l’application** > **Source**.</span><span class="sxs-lookup"><span data-stu-id="b401c-107">Click **Step 2: Replicate application** > **Source**.</span></span> 

    ![Activer la réplication](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication1.png)

2. <span data-ttu-id="b401c-109">Dans **Source**, sélectionnez le serveur VMM de hello et hello cloud dans quel hello hôtes Hyper-V que vous souhaitez tooreplicate sont situés.</span><span class="sxs-lookup"><span data-stu-id="b401c-109">In **Source**, select hello VMM server, and hello cloud in which hello Hyper-V hosts you want tooreplicate are located.</span></span> <span data-ttu-id="b401c-110">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b401c-110">Then click **OK**.</span></span>

    ![Activer la réplication](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication2.png)
3. <span data-ttu-id="b401c-112">Dans **cible**, vérifiez que le serveur VMM secondaire de hello et cloud.</span><span class="sxs-lookup"><span data-stu-id="b401c-112">In **Target**, verify hello secondary VMM server and cloud.</span></span>
4. <span data-ttu-id="b401c-113">Dans **virtuels**, sélectionnez hello machines virtuelles tooprotect à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="b401c-113">In **Virtual machines**, select hello VMs you want tooprotect from hello list.</span></span>

    ![Activer la protection pour les machines virtuelles](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication5.png)

<span data-ttu-id="b401c-115">Vous pouvez suivre la progression de hello **activer la Protection** action dans **travaux** > **les tâches de récupération de Site**.</span><span class="sxs-lookup"><span data-stu-id="b401c-115">You can track progress of hello **Enable Protection** action in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="b401c-116">Après avoir hello **finaliser la Protection** tâche se termine, hello la réplication initiale est terminée et ordinateur virtuel de hello est prêt pour le basculement.</span><span class="sxs-lookup"><span data-stu-id="b401c-116">After hello **Finalize Protection** job completes, hello initial replication is complete, and hello virtual machine is ready for failover.</span></span>

<span data-ttu-id="b401c-117">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="b401c-117">Note that:</span></span>

- <span data-ttu-id="b401c-118">Vous pouvez également activer la protection des machines virtuelles dans la console VMM hello.</span><span class="sxs-lookup"><span data-stu-id="b401c-118">You can also enable protection for virtual machines in hello VMM console.</span></span> <span data-ttu-id="b401c-119">Cliquez sur **activer la Protection** de barre d’outils hello dans les propriétés d’une machine virtuelle hello > **Azure Site Recovery** onglet.</span><span class="sxs-lookup"><span data-stu-id="b401c-119">Click **Enable Protection** on hello toolbar in hello virtual machine properties > **Azure Site Recovery** tab.</span></span>
- <span data-ttu-id="b401c-120">Une fois que vous avez activé la réplication, vous pouvez afficher les propriétés d’hello VM dans **répliquées des éléments**.</span><span class="sxs-lookup"><span data-stu-id="b401c-120">After you've enabled replication, you can view properties for hello VM in **Replicated Items**.</span></span> <span data-ttu-id="b401c-121">Sur hello **Essentials** tableau de bord, vous pouvez voir des informations sur la stratégie de réplication hello pour hello machine virtuelle et son état.</span><span class="sxs-lookup"><span data-stu-id="b401c-121">On hello **Essentials** dashboard, you can see information about hello replication policy for hello VM and its status.</span></span> <span data-ttu-id="b401c-122">Cliquez sur **Propriétés** pour obtenir plus de détails.</span><span class="sxs-lookup"><span data-stu-id="b401c-122">Click **Properties** for more details.</span></span>

## <a name="onboard-existing-vms"></a><span data-ttu-id="b401c-123">Intégrer des machines virtuelles existantes</span><span class="sxs-lookup"><span data-stu-id="b401c-123">Onboard existing VMs</span></span>

<span data-ttu-id="b401c-124">Si vous avez des machines virtuelles existantes dans VMM qui sont répliquées à l’aide du réplica Hyper-V, vous pouvez les intégrer à la réplication Azure Site Recovery comme suit :</span><span class="sxs-lookup"><span data-stu-id="b401c-124">If you have existing virtual machines in VMM that are replicating with Hyper-V Replica, you can onboard them for Azure Site Recovery replication as follows:</span></span>

1. <span data-ttu-id="b401c-125">Assurez-vous que ce serveur hello Hyper-V héberge hello que machine virtuelle existante se trouve dans un cloud principal hello, et ce serveur d’Hyper-V hello hébergement hello ordinateur virtuel se trouve dans le cloud secondaire de hello.</span><span class="sxs-lookup"><span data-stu-id="b401c-125">Ensure that hello Hyper-V server hosting hello existing VM is located in hello primary cloud, and that hello Hyper-V server hosting hello replica virtual machine is located in hello secondary cloud.</span></span>
2. <span data-ttu-id="b401c-126">Assurez-vous que la stratégie de réplication est configurée pour un cloud VMM principal hello.</span><span class="sxs-lookup"><span data-stu-id="b401c-126">Make sure a replication policy is configured for hello primary VMM cloud.</span></span>
3. <span data-ttu-id="b401c-127">Activer la réplication pour l’ordinateur virtuel principal hello.</span><span class="sxs-lookup"><span data-stu-id="b401c-127">Enable replication for hello primary virtual machine.</span></span> <span data-ttu-id="b401c-128">Azure Site Recovery et VMM s’assurer que hello même hôte de réplica et de la machine virtuelle est détectée et Azure Site Recovery réutilise et spécifié les paramètres de réplication de rétablir la connexion à l’aide de hello.</span><span class="sxs-lookup"><span data-stu-id="b401c-128">Azure Site Recovery and VMM ensure that hello same replica host and virtual machine is detected, and Azure Site Recovery will reuse and reestablish replication using hello specified settings.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b401c-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b401c-129">Next steps</span></span>

<span data-ttu-id="b401c-130">Accédez trop[étape 10 : exécuter un test de basculement](vmm-to-vmm-walkthrough-test-failover.md).</span><span class="sxs-lookup"><span data-stu-id="b401c-130">Go too[Step 10: Run a test failover](vmm-to-vmm-walkthrough-test-failover.md).</span></span>
