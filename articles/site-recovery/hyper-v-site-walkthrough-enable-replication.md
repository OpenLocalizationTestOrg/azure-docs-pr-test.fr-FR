---
title: "la réplication pour les ordinateurs virtuels Hyper-V en répliquant tooAzure (sans System Center VMM) avec Azure Site Recovery aaaEnable | Documents Microsoft"
description: "Résume les étapes hello vous devez tooenable réplication tooAzure pour des ordinateurs virtuels Hyper-V à l’aide du service d’Azure Site Recovery hello"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: bd31ef01-69f1-4591-a519-e42510a6e2f4
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 1589cb7aa1fe954e075cb7bf1f4a4ec199ed3ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-enable-replication-for-hyper-v-vms-replicating-tooazure"></a><span data-ttu-id="44ef9-103">Étape 10 : Activer la réplication pour les ordinateurs virtuels Hyper-V en réplication tooAzure</span><span class="sxs-lookup"><span data-stu-id="44ef9-103">Step 10: Enable replication for Hyper-V VMs replicating tooAzure</span></span>


<span data-ttu-id="44ef9-104">Cet article décrit comment la réplication pour tooenable locaux virtuels Hyper-V (ne pas gérés par System Center VMM) tooAzure, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="44ef9-104">This article describes how tooenable replication for on-premises Hyper-V virtual machines (not managed by System Center VMM) tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="44ef9-105">Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="44ef9-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="before-you-start"></a><span data-ttu-id="44ef9-106">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="44ef9-106">Before you start</span></span>

<span data-ttu-id="44ef9-107">Avant de commencer, assurez-vous que votre compte d’utilisateur Azure a hello requis [autorisations](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable la réplication d’un nouveau tooAzure d’ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="44ef9-107">Before you start, ensure that your Azure user account has hello required [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of a new virtual machine tooAzure.</span></span>

## <a name="exclude-disks-from-replication"></a><span data-ttu-id="44ef9-108">Exclure les disques de la réplication</span><span class="sxs-lookup"><span data-stu-id="44ef9-108">Exclude disks from replication</span></span>

<span data-ttu-id="44ef9-109">Par défaut, tous les disques d’une machine sont répliqués.</span><span class="sxs-lookup"><span data-stu-id="44ef9-109">By default all disks on a machine are replicated.</span></span> <span data-ttu-id="44ef9-110">Vous pouvez exclure des disques de la réplication.</span><span class="sxs-lookup"><span data-stu-id="44ef9-110">You can exclude disks from replication.</span></span> <span data-ttu-id="44ef9-111">Par exemple, vous pouvez tooreplicate les disques avec les données temporaires ou des données a actualisé chaque fois qu’un ordinateur ou redémarrage de l’application (par exemple pagefile.sys ou tempdb de SQL Server).</span><span class="sxs-lookup"><span data-stu-id="44ef9-111">For example you might not want tooreplicate disks with temporary data, or data that's refreshed each time a machine or application restarts (for example pagefile.sys or SQL Server tempdb).</span></span> [<span data-ttu-id="44ef9-112">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="44ef9-112">Learn more</span></span>](site-recovery-exclude-disk.md)


## <a name="replicate-vms"></a><span data-ttu-id="44ef9-113">Répliquer des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="44ef9-113">Replicate VMs</span></span>

<span data-ttu-id="44ef9-114">Activez la réplication des machines virtuelles comme suit :</span><span class="sxs-lookup"><span data-stu-id="44ef9-114">Enable replication for VMs as follows:</span></span>          

1. <span data-ttu-id="44ef9-115">Cliquez sur **Répliquer l’application** > **Source**.</span><span class="sxs-lookup"><span data-stu-id="44ef9-115">Click **Replicate application** > **Source**.</span></span> <span data-ttu-id="44ef9-116">Après avoir configuré la réplication pour hello la première fois, vous pouvez cliquer sur **+ répliquer** tooenable la réplication pour des ordinateurs supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="44ef9-116">After you've set up replication for hello first time, you can click **+Replicate** tooenable replication for additional machines.</span></span>

    ![Activer la réplication](./media/hyper-v-site-walkthrough-enable-replication/enable-replication.png)
2. <span data-ttu-id="44ef9-118">Dans **Source**, sélectionnez les sites hello Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="44ef9-118">In **Source**, select hello Hyper-V site.</span></span> <span data-ttu-id="44ef9-119">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="44ef9-119">Then click **OK**.</span></span>
3. <span data-ttu-id="44ef9-120">Dans **cible**, sélectionnez l’abonnement de coffre hello et hello basculement modèle toouse dans Azure (classique ou ressource management) après le basculement.</span><span class="sxs-lookup"><span data-stu-id="44ef9-120">In **Target**, select hello vault subscription, and hello failover model you want toouse in Azure (classic or resource management) after failover.</span></span>
4. <span data-ttu-id="44ef9-121">Sélectionnez le compte de stockage hello souhaité toouse.</span><span class="sxs-lookup"><span data-stu-id="44ef9-121">Select hello storage account you want toouse.</span></span> <span data-ttu-id="44ef9-122">Si vous n’avez pas un compte que vous souhaitez toouse, vous pouvez [créer un](#set-up-an-azure-storage-account).</span><span class="sxs-lookup"><span data-stu-id="44ef9-122">If you don't have an account you want toouse, you can [create one](#set-up-an-azure-storage-account).</span></span> <span data-ttu-id="44ef9-123">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="44ef9-123">Then click **OK**.</span></span>
5. <span data-ttu-id="44ef9-124">Sélectionnez hello toowhich réseau et le sous-réseau Azure machines virtuelles Azure se connecte lorsqu’elles sont créées avec basculement.</span><span class="sxs-lookup"><span data-stu-id="44ef9-124">Select hello Azure network and subnet toowhich Azure VMs will connect when they're created failover.</span></span>

    - <span data-ttu-id="44ef9-125">tooapply hello paramètres tooall ordinateurs du réseau vous activez pour la réplication, sélectionnez **configurer maintenant pour les ordinateurs sélectionnés**.</span><span class="sxs-lookup"><span data-stu-id="44ef9-125">tooapply hello network settings tooall machines you enable for replication, select **Configure now for selected machines**.</span></span>
    - <span data-ttu-id="44ef9-126">Sélectionnez **configurer ultérieurement** tooselect hello réseau Azure par ordinateur.</span><span class="sxs-lookup"><span data-stu-id="44ef9-126">Select **Configure later** tooselect hello Azure network per machine.</span></span>
    - <span data-ttu-id="44ef9-127">Si vous n’avez pas un réseau de toouse, vous pouvez [créer un](#set-up-an-azure-network).</span><span class="sxs-lookup"><span data-stu-id="44ef9-127">If you don't have a network you want toouse, you can [create one](#set-up-an-azure-network).</span></span> <span data-ttu-id="44ef9-128">Sélectionnez un sous-réseau, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="44ef9-128">Select a subnet if applicable.</span></span> <span data-ttu-id="44ef9-129">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="44ef9-129">Then click **OK**.</span></span>

   ![Activer la réplication](./media/hyper-v-site-walkthrough-enable-replication/enable-replication11.png)

6. <span data-ttu-id="44ef9-131">Dans **virtuels** > **sélectionner des machines virtuelles**, cliquez sur et sélectionnez chaque ordinateur que vous souhaitez tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="44ef9-131">In **Virtual Machines** > **Select virtual machines**, click and select each machine you want tooreplicate.</span></span> <span data-ttu-id="44ef9-132">Vous pouvez uniquement sélectionner les machines pour lesquelles la réplication peut être activée.</span><span class="sxs-lookup"><span data-stu-id="44ef9-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="44ef9-133">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="44ef9-133">Then click **OK**.</span></span>

    ![Activer la réplication](./media/hyper-v-site-walkthrough-enable-replication/enable-replication5-for-exclude-disk.png)

7. <span data-ttu-id="44ef9-135">Dans **propriétés** > **configurer les propriétés**, sélectionnez le système d’exploitation de hello pour les machines virtuelles hello sélectionné et hello disque de système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="44ef9-135">In **Properties** > **Configure properties**, select hello operating system for hello selected VMs, and hello OS disk.</span></span>
8. <span data-ttu-id="44ef9-136">Vérifiez que ce nom de machine virtuelle Azure hello (nom de la cible) est conforme à [spécifications de la machine virtuelle Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="44ef9-136">Verify that hello Azure VM name (target name) complies with [Azure virtual machine requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
9. <span data-ttu-id="44ef9-137">Par défaut, tous les disques hello Hello machine virtuelle sont sélectionnés pour la réplication.</span><span class="sxs-lookup"><span data-stu-id="44ef9-137">By default all hello disks of hello VM are selected for replication.</span></span> <span data-ttu-id="44ef9-138">Disques effacer tooexclude les.</span><span class="sxs-lookup"><span data-stu-id="44ef9-138">Clear disks tooexclude them.</span></span>
10. <span data-ttu-id="44ef9-139">Cliquez sur **OK** toosave modifications.</span><span class="sxs-lookup"><span data-stu-id="44ef9-139">Click **OK** toosave changes.</span></span> <span data-ttu-id="44ef9-140">Vous pouvez opter pour une définition ultérieure des propriétés.</span><span class="sxs-lookup"><span data-stu-id="44ef9-140">You can set additional properties later.</span></span>

    ![Activer la réplication](./media/hyper-v-site-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

11. <span data-ttu-id="44ef9-142">Dans **les paramètres de réplication** > **configurer les paramètres de réplication**, sélectionnez hello réplication stratégie tooapply pour hello protégé des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="44ef9-142">In **Replication settings** > **Configure replication settings**, select hello replication policy you want tooapply for hello protected VMs.</span></span> <span data-ttu-id="44ef9-143">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="44ef9-143">Then click **OK**.</span></span> <span data-ttu-id="44ef9-144">Vous pouvez modifier la stratégie de réplication hello dans **stratégies de réplication** > nom de la stratégie > **modifier les paramètres**.</span><span class="sxs-lookup"><span data-stu-id="44ef9-144">You can modify hello replication policy in **Replication policies** > policy-name > **Edit Settings**.</span></span> <span data-ttu-id="44ef9-145">Les modifications que vous appliquez seront utilisées pour les nouvelles machines et les machines dont la réplication est déjà en cours.</span><span class="sxs-lookup"><span data-stu-id="44ef9-145">Changes you apply will be used for machines that are already replicating, and new machines.</span></span>


   ![Activer la réplication](./media/hyper-v-site-walkthrough-enable-replication/enable-replication7.png)

<span data-ttu-id="44ef9-147">Vous pouvez suivre la progression de hello **activer la Protection** de la tâche dans **travaux** > **les tâches de récupération de Site**.</span><span class="sxs-lookup"><span data-stu-id="44ef9-147">You can track progress of hello **Enable Protection** job in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="44ef9-148">Après avoir hello **finaliser la Protection** s’exécute la tâche machine de hello est prête pour le basculement.</span><span class="sxs-lookup"><span data-stu-id="44ef9-148">After hello **Finalize Protection** job runs hello machine is ready for failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="44ef9-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="44ef9-149">Next steps</span></span>


<span data-ttu-id="44ef9-150">Accédez trop[étape 11 : exécuter un test de basculement](hyper-v-site-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="44ef9-150">Go too[Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>
