---
title: "aaaRun un test de basculement pour le site secondaire de la tooa de réplication d’ordinateur virtuel Hyper-V avec Azure Site Recovery | Documents Microsoft"
description: "Décrit comment toorun un test de basculement pour un ordinateur virtuel Hyper-V réplication tooa System Center VMM secondaire du site avec Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a3fd11ce-65a1-4308-8435-45cf954353ef
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: a60411541c2db001c573735bcb0d651f6618f295
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-run-a-test-failover-for-hyper-v-replication-tooa-secondary-site"></a><span data-ttu-id="6acbf-103">Étape 10 : Exécuter un test de basculement pour le site secondaire de tooa de réplication Hyper-V</span><span class="sxs-lookup"><span data-stu-id="6acbf-103">Step 10: Run a test failover for Hyper-V replication tooa secondary site</span></span>


<span data-ttu-id="6acbf-104">Après avoir activé la réplication pour Hyper-V virtual machines virtuelles avec [Azure Site Recovery](site-recovery-overview.md), utilisez cette toorun article un test de basculement.</span><span class="sxs-lookup"><span data-stu-id="6acbf-104">After you enable replication for Hyper-V virtual machines (VMs) with [Azure Site Recovery](site-recovery-overview.md), use this article toorun a test failover.</span></span> <span data-ttu-id="6acbf-105">Un test de basculement vérifie que la réplication fonctionne, sans affecter votre environnement de production.</span><span class="sxs-lookup"><span data-stu-id="6acbf-105">A test failover verifies that replication is working, without impacting your production environment.</span></span> 


<span data-ttu-id="6acbf-106">Après avoir lu cet article, validez les commentaires au bas de hello, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="6acbf-106">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="6acbf-107">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="6acbf-107">Before you start</span></span>

- <span data-ttu-id="6acbf-108">Lorsque vous êtes déclenchement d’un test de basculement, vous pouvez spécifier le réplica hello réseau toowhich hello test que machines virtuelles se connectera.</span><span class="sxs-lookup"><span data-stu-id="6acbf-108">When you're triggering a test failover, you can specify hello network toowhich hello test replica VMs will connect.</span></span> <span data-ttu-id="6acbf-109">[En savoir plus](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) sur les options de réseau hello.</span><span class="sxs-lookup"><span data-stu-id="6acbf-109">[Learn more](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) about hello network options.</span></span>
- <span data-ttu-id="6acbf-110">Nous vous recommandons de ne pas choisir un réseau que vous avez sélectionné lors du mappage réseau.</span><span class="sxs-lookup"><span data-stu-id="6acbf-110">We recommend that you don't choose a network that you selected during network mapping.</span></span>
- <span data-ttu-id="6acbf-111">instructions Hello dans cet article décrivent comment toofail sur une seule machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6acbf-111">hello instructions in this article describe how toofail over a single VM.</span></span> <span data-ttu-id="6acbf-112">En savoir plus sur [création de plans de récupération](site-recovery-create-recovery-plans.md) si vous souhaitez toofail sur plusieurs machines virtuelles ensemble.</span><span class="sxs-lookup"><span data-stu-id="6acbf-112">Read about [creating recovery plans](site-recovery-create-recovery-plans.md) if you want toofail over multiple VMs together.</span></span>
- <span data-ttu-id="6acbf-113">En savoir plus sur les[limitations des tests de basculement](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).</span><span class="sxs-lookup"><span data-stu-id="6acbf-113">Read about [limitations for test failovers](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).</span></span>
- <span data-ttu-id="6acbf-114">adresse IP donnée tooa machine virtuelle pendant le test de basculement Hello est hello recevrait la même adresse IP que hello de machine virtuelle pour un basculement planifié ou non planifié (en supposant qu’adresse hello est disponible dans le réseau de basculement de test hello).</span><span class="sxs-lookup"><span data-stu-id="6acbf-114">hello IP address given tooa VM during test failover is hello same IP address that hello VM would receive for a planned or unplanned failover (presuming that hello IP address is available in hello test failover network).</span></span> <span data-ttu-id="6acbf-115">Si l’adresse IP de hello n’est pas disponible dans le réseau de basculement de test hello, hello machine virtuelle reçoit une autre adresse IP qui est disponible dans le réseau de basculement de test hello.</span><span class="sxs-lookup"><span data-stu-id="6acbf-115">If hello IP address isn't available in hello test failover network, hello VM receives another IP address that is available in hello test failover network.</span></span>
- <span data-ttu-id="6acbf-116">Si vous voulez toodo un test de basculement dans votre réseau de production, pour une validation complète de l’ordinateur de connectivité réseau de bout en bout, sachez que :</span><span class="sxs-lookup"><span data-stu-id="6acbf-116">If you do want toodo a test failover in your production network, for full validatation of end-to-end network connectivity machine, note that:</span></span>
    - <span data-ttu-id="6acbf-117">Hello de qu'ordinateur virtuel principal doit être arrêté lorsque vous effectuez un test de basculement hello.</span><span class="sxs-lookup"><span data-stu-id="6acbf-117">hello primary VM should be shut down when you're doing hello test failover.</span></span> <span data-ttu-id="6acbf-118">Sinon, deux machines virtuelles avec hello même identité sera exécuté dans hello même réseau à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="6acbf-118">Otherwise, two VMs with hello same identity will be running in hello same network at hello same time.</span></span> 
    - <span data-ttu-id="6acbf-119">Si vous apportez des modifications tootest VM, ces modifications sont perdues lors du nettoyage hello test de basculement.</span><span class="sxs-lookup"><span data-stu-id="6acbf-119">If you make changes tootest VMs, those changes are lost when you clean up hello test failover.</span></span> <span data-ttu-id="6acbf-120">Ces modifications ne sont pas répliquée toohello arrière d’ordinateurs virtuels principal.</span><span class="sxs-lookup"><span data-stu-id="6acbf-120">These changes aren't replicated back toohello primary VM.</span></span>
    - <span data-ttu-id="6acbf-121">Tester un un réseau de production prospects toodowntime pour vos charges de travail de production.</span><span class="sxs-lookup"><span data-stu-id="6acbf-121">Testing a a production network leads toodowntime for your production workloads.</span></span> <span data-ttu-id="6acbf-122">Demander aux utilisateurs pas toouse application hello lors de l’extraction de récupération d’urgence hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="6acbf-122">Ask users not toouse hello app when hello disaster recovery drill is in progress.</span></span>  


## <a name="run-a-test-failover-for-a-vm"></a><span data-ttu-id="6acbf-123">Exécuter un test de basculement pour une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="6acbf-123">Run a test failover for a VM</span></span>

1. <span data-ttu-id="6acbf-124">toofail sur une seule machine virtuelle, dans **répliquées des éléments**, cliquez sur la machine virtuelle de hello > **Test de basculement**.</span><span class="sxs-lookup"><span data-stu-id="6acbf-124">toofail over a single VM, in **Replicated Items**, click hello VM > **Test Failover**.</span></span>
2. <span data-ttu-id="6acbf-125">Dans **le Test de basculement**, spécifiez comment machines virtuelles de test sera connecté toonetworks après le basculement de test hello.</span><span class="sxs-lookup"><span data-stu-id="6acbf-125">In **Test Failover**, specify how test VMs will be connected toonetworks after hello test failover.</span></span> 
3. <span data-ttu-id="6acbf-126">Cliquez sur **OK** toobegin hello basculement.</span><span class="sxs-lookup"><span data-stu-id="6acbf-126">Click **OK** toobegin hello failover.</span></span> <span data-ttu-id="6acbf-127">Suivre la progression sur hello **travaux** onglet.</span><span class="sxs-lookup"><span data-stu-id="6acbf-127">Track progress on hello **Jobs** tab.</span></span>
5. <span data-ttu-id="6acbf-128">Une fois le basculement terminé, vérifiez que le test hello démarrage des machines virtuelles avec succès.</span><span class="sxs-lookup"><span data-stu-id="6acbf-128">After failover is complete, verify that hello test VMs start successfully.</span></span>
6. <span data-ttu-id="6acbf-129">Lorsque vous avez terminé, cliquez sur **basculement de test de nettoyage** sur le plan de récupération hello.</span><span class="sxs-lookup"><span data-stu-id="6acbf-129">When you're done, click **Cleanup test failover** on hello recovery plan.</span></span>
7. <span data-ttu-id="6acbf-130">Dans **Notes**, enregistrer et enregistrer toutes les observations associées au basculement de test hello.</span><span class="sxs-lookup"><span data-stu-id="6acbf-130">In **Notes**, record and save any observations associated with hello test failover.</span></span> <span data-ttu-id="6acbf-131">Cette étape supprime hello ordinateurs virtuels et des réseaux qui ont été créés pendant le test de basculement.</span><span class="sxs-lookup"><span data-stu-id="6acbf-131">This step deletes hello virtual machines and networks that were created during test failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6acbf-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6acbf-132">Next steps</span></span>

<span data-ttu-id="6acbf-133">Une fois que vous avez testé le déploiement de hello, en savoir plus sur les autres types de [basculement](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="6acbf-133">After you've tested hello deployment, learn more about other types of [failover](site-recovery-failover.md).</span></span>
