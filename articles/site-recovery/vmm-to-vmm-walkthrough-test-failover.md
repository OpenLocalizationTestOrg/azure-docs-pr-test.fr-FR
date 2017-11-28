---
title: "Exécuter un test de basculement pour la réplication d’une machine virtuelle Hyper-V sur un site secondaire avec Azure Site Recovery | Documents Microsoft"
description: "Décrit comment exécuter un test de basculement pour la réplication de machines virtuelles Hyper-V sur un site secondaire System Center VMM avec Azure Site Recovery."
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
ms.openlocfilehash: 23d235d326273e7ec59feee6588a39f685401e52
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="step-10-run-a-test-failover-for-hyper-v-replication-to-a-secondary-site"></a><span data-ttu-id="4d2cf-103">Étape 10 : exécuter un test de basculement pour la réplication Hyper-V vers un site secondaire</span><span class="sxs-lookup"><span data-stu-id="4d2cf-103">Step 10: Run a test failover for Hyper-V replication to a secondary site</span></span>


<span data-ttu-id="4d2cf-104">Après avoir activé la réplication de machines virtuelles Hyper-V avec [Azure Site Recovery](site-recovery-overview.md), cet article permet d’exécuter un test de basculement.</span><span class="sxs-lookup"><span data-stu-id="4d2cf-104">After you enable replication for Hyper-V virtual machines (VMs) with [Azure Site Recovery](site-recovery-overview.md), use this article to run a test failover.</span></span> <span data-ttu-id="4d2cf-105">Un test de basculement vérifie que la réplication fonctionne, sans affecter votre environnement de production.</span><span class="sxs-lookup"><span data-stu-id="4d2cf-105">A test failover verifies that replication is working, without impacting your production environment.</span></span> 


<span data-ttu-id="4d2cf-106">Après avoir lu cet article, publiez des commentaires au bas de ce dernier ou sur le [Forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="4d2cf-106">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="4d2cf-107">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="4d2cf-107">Before you start</span></span>

- <span data-ttu-id="4d2cf-108">Lors du déclenchement d’un test de basculement, vous pouvez spécifier le réseau auquel les machines virtuelles réplica de test se connectent.</span><span class="sxs-lookup"><span data-stu-id="4d2cf-108">When you're triggering a test failover, you can specify the network to which the test replica VMs will connect.</span></span> <span data-ttu-id="4d2cf-109">[En savoir plus](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) sur les options de réseau.</span><span class="sxs-lookup"><span data-stu-id="4d2cf-109">[Learn more](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) about the network options.</span></span>
- <span data-ttu-id="4d2cf-110">Nous vous recommandons de ne pas choisir un réseau que vous avez sélectionné lors du mappage réseau.</span><span class="sxs-lookup"><span data-stu-id="4d2cf-110">We recommend that you don't choose a network that you selected during network mapping.</span></span>
- <span data-ttu-id="4d2cf-111">Les instructions fournies dans cet article décrivent comment basculer d’une seule machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4d2cf-111">The instructions in this article describe how to fail over a single VM.</span></span> <span data-ttu-id="4d2cf-112">Reportez-vous à la documentation sur la[création de plans de récupération](site-recovery-create-recovery-plans.md) si vous souhaitez basculer ensemble plusieurs machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="4d2cf-112">Read about [creating recovery plans](site-recovery-create-recovery-plans.md) if you want to fail over multiple VMs together.</span></span>
- <span data-ttu-id="4d2cf-113">En savoir plus sur les[limitations des tests de basculement](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).</span><span class="sxs-lookup"><span data-stu-id="4d2cf-113">Read about [limitations for test failovers](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).</span></span>
- <span data-ttu-id="4d2cf-114">L’adresse IP donnée à une machine virtuelle durant un test de basculement est identique à l’adresse IP qu’elle recevrait durant un basculement planifié ou non planifié (à condition que l’adresse IP soit disponible dans le réseau de test de basculement).</span><span class="sxs-lookup"><span data-stu-id="4d2cf-114">The IP address given to a VM during test failover is the same IP address that the VM would receive for a planned or unplanned failover (presuming that the IP address is available in the test failover network).</span></span> <span data-ttu-id="4d2cf-115">Si l’adresse IP n’est pas disponible dans le réseau de test de basculement, la machine virtuelle reçoit une autre adresse IP disponible dans le réseau de test de basculement.</span><span class="sxs-lookup"><span data-stu-id="4d2cf-115">If the IP address isn't available in the test failover network, the VM receives another IP address that is available in the test failover network.</span></span>
- <span data-ttu-id="4d2cf-116">Si vous ne souhaitez pas effectuer un test de basculement dans votre réseau de production, pour une validation complète de l’ordinateur de connectivité réseau de bout en bout, sachez que :</span><span class="sxs-lookup"><span data-stu-id="4d2cf-116">If you do want to do a test failover in your production network, for full validatation of end-to-end network connectivity machine, note that:</span></span>
    - <span data-ttu-id="4d2cf-117">La machine virtuelle principale doit être arrêtée lorsque vous effectuez le test de basculement.</span><span class="sxs-lookup"><span data-stu-id="4d2cf-117">The primary VM should be shut down when you're doing the test failover.</span></span> <span data-ttu-id="4d2cf-118">Si vous ne le faites pas, deux machines virtuelles avec la même identité s’exécuteront sur le même réseau en même temps.</span><span class="sxs-lookup"><span data-stu-id="4d2cf-118">Otherwise, two VMs with the same identity will be running in the same network at the same time.</span></span> 
    - <span data-ttu-id="4d2cf-119">Si vous apportez des modifications aux machines virtuelles de test, ces modifications sont perdues lors du nettoyage du test de basculement.</span><span class="sxs-lookup"><span data-stu-id="4d2cf-119">If you make changes to test VMs, those changes are lost when you clean up the test failover.</span></span> <span data-ttu-id="4d2cf-120">Ces modifications ne sont pas répliquées vers la machine virtuelle principale.</span><span class="sxs-lookup"><span data-stu-id="4d2cf-120">These changes aren't replicated back to the primary VM.</span></span>
    - <span data-ttu-id="4d2cf-121">Tester un réseau de production entraîne une interruption des charges de travail de production.</span><span class="sxs-lookup"><span data-stu-id="4d2cf-121">Testing a a production network leads to downtime for your production workloads.</span></span> <span data-ttu-id="4d2cf-122">Demandez aux utilisateurs de ne pas utiliser l’application lorsque l’extraction de récupération d’urgence est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="4d2cf-122">Ask users not to use the app when the disaster recovery drill is in progress.</span></span>  


## <a name="run-a-test-failover-for-a-vm"></a><span data-ttu-id="4d2cf-123">Exécuter un test de basculement pour une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="4d2cf-123">Run a test failover for a VM</span></span>

1. <span data-ttu-id="4d2cf-124">Pour effectuer le basculement d’une seule machine virtuelle, dans **Éléments répliqués**, cliquez sur la machine virtuelle > **Test de basculement**.</span><span class="sxs-lookup"><span data-stu-id="4d2cf-124">To fail over a single VM, in **Replicated Items**, click the VM > **Test Failover**.</span></span>
2. <span data-ttu-id="4d2cf-125">Dans **Test de basculement**, indiquez le mode de connexion des machines virtuelles aux réseaux après le test de basculement.</span><span class="sxs-lookup"><span data-stu-id="4d2cf-125">In **Test Failover**, specify how test VMs will be connected to networks after the test failover.</span></span> 
3. <span data-ttu-id="4d2cf-126">Cliquez sur **OK** pour commencer le basculement.</span><span class="sxs-lookup"><span data-stu-id="4d2cf-126">Click **OK** to begin the failover.</span></span> <span data-ttu-id="4d2cf-127">Effectuez un suivi de l’opération dans l’onglet **Tâches** .</span><span class="sxs-lookup"><span data-stu-id="4d2cf-127">Track progress on the **Jobs** tab.</span></span>
5. <span data-ttu-id="4d2cf-128">Une fois le basculement terminé, vérifiez que les machines virtuelles démarrent correctement.</span><span class="sxs-lookup"><span data-stu-id="4d2cf-128">After failover is complete, verify that the test VMs start successfully.</span></span>
6. <span data-ttu-id="4d2cf-129">Une fois que vous avez terminé, cliquez sur **Nettoyer le test de basculement** sur le plan de récupération.</span><span class="sxs-lookup"><span data-stu-id="4d2cf-129">When you're done, click **Cleanup test failover** on the recovery plan.</span></span>
7. <span data-ttu-id="4d2cf-130">Cliquez sur **Notes** pour consigner et enregistrer d’éventuelles observations sur le test de basculement.</span><span class="sxs-lookup"><span data-stu-id="4d2cf-130">In **Notes**, record and save any observations associated with the test failover.</span></span> <span data-ttu-id="4d2cf-131">Cette étape supprime les machines et les réseaux virtuels qui ont été créés au cours du test de basculement.</span><span class="sxs-lookup"><span data-stu-id="4d2cf-131">This step deletes the virtual machines and networks that were created during test failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4d2cf-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4d2cf-132">Next steps</span></span>

<span data-ttu-id="4d2cf-133">Une fois que vous avez testé le déploiement, apprenez-en davantage sur les autres types de [basculement](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="4d2cf-133">After you've tested the deployment, learn more about other types of [failover](site-recovery-failover.md).</span></span>
