---
title: "Activer la réplication de machines virtuelles Hyper-V vers Azure (sans System Center VMM) avec Azure Site Recovery | Microsoft Docs"
description: "Résume les étapes requises pour activer la réplication de machines virtuelles Hyper-V vers Azure à l’aide du service Azure Site Recovery"
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
ms.openlocfilehash: aabe99dbd375b80e4a87ca7a067927008672b4ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="step-10-enable-replication-for-hyper-v-vms-replicating-to-azure"></a><span data-ttu-id="0585c-103">Étape 10 : activer la réplication de machines virtuelles Hyper-V vers Azure</span><span class="sxs-lookup"><span data-stu-id="0585c-103">Step 10: Enable replication for Hyper-V VMs replicating to Azure</span></span>


<span data-ttu-id="0585c-104">Cet article explique comment activer la réplication de machines virtuelles Hyper-V locales (non gérées par System Center VMM) à l’aide du service [Azure Site Recovery](site-recovery-overview.md) dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0585c-104">This article describes how to enable replication for on-premises Hyper-V virtual machines (not managed by System Center VMM) to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="0585c-105">Publiez des commentaires et des questions au bas de cet article, ou sur le [Forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="0585c-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="before-you-start"></a><span data-ttu-id="0585c-106">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="0585c-106">Before you start</span></span>

<span data-ttu-id="0585c-107">Avant de commencer, vérifiez que votre compte d’utilisateur Azure dispose des [autorisations](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) requises pour activer la réplication d’une nouvelle machine virtuelle dans Azure.</span><span class="sxs-lookup"><span data-stu-id="0585c-107">Before you start, ensure that your Azure user account has the required [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to enable replication of a new virtual machine to Azure.</span></span>

## <a name="exclude-disks-from-replication"></a><span data-ttu-id="0585c-108">Exclure les disques de la réplication</span><span class="sxs-lookup"><span data-stu-id="0585c-108">Exclude disks from replication</span></span>

<span data-ttu-id="0585c-109">Par défaut, tous les disques d’une machine sont répliqués.</span><span class="sxs-lookup"><span data-stu-id="0585c-109">By default all disks on a machine are replicated.</span></span> <span data-ttu-id="0585c-110">Vous pouvez exclure des disques de la réplication.</span><span class="sxs-lookup"><span data-stu-id="0585c-110">You can exclude disks from replication.</span></span> <span data-ttu-id="0585c-111">Par exemple, vous pouvez ne pas répliquer les disques comportant des données temporaires, ou des données actualisées à chaque redémarrage d’une machine ou d’une application (par exemple, pagefile.sys ou tempdb dans SQL Server).</span><span class="sxs-lookup"><span data-stu-id="0585c-111">For example you might not want to replicate disks with temporary data, or data that's refreshed each time a machine or application restarts (for example pagefile.sys or SQL Server tempdb).</span></span> [<span data-ttu-id="0585c-112">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="0585c-112">Learn more</span></span>](site-recovery-exclude-disk.md)


## <a name="replicate-vms"></a><span data-ttu-id="0585c-113">Répliquer des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="0585c-113">Replicate VMs</span></span>

<span data-ttu-id="0585c-114">Activez la réplication des machines virtuelles comme suit :</span><span class="sxs-lookup"><span data-stu-id="0585c-114">Enable replication for VMs as follows:</span></span>          

1. <span data-ttu-id="0585c-115">Cliquez sur **Répliquer l’application** > **Source**.</span><span class="sxs-lookup"><span data-stu-id="0585c-115">Click **Replicate application** > **Source**.</span></span> <span data-ttu-id="0585c-116">Après avoir configuré la réplication pour la première fois, vous pouvez cliquer sur l’option **+Répliquer** pour activer la réplication des machines supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="0585c-116">After you've set up replication for the first time, you can click **+Replicate** to enable replication for additional machines.</span></span>

    ![Activer la réplication](./media/hyper-v-site-walkthrough-enable-replication/enable-replication.png)
2. <span data-ttu-id="0585c-118">Dans **Source**, sélectionnez le site Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="0585c-118">In **Source**, select the Hyper-V site.</span></span> <span data-ttu-id="0585c-119">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0585c-119">Then click **OK**.</span></span>
3. <span data-ttu-id="0585c-120">Dans **Cible**, sélectionnez l’abonnement de coffre et le modèle de basculement que vous souhaitez utiliser dans Azure (gestion des ressources ou classique) après le basculement.</span><span class="sxs-lookup"><span data-stu-id="0585c-120">In **Target**, select the vault subscription, and the failover model you want to use in Azure (classic or resource management) after failover.</span></span>
4. <span data-ttu-id="0585c-121">Sélectionnez le compte de stockage que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="0585c-121">Select the storage account you want to use.</span></span> <span data-ttu-id="0585c-122">Si vous ne possédez pas de compte, vous pouvez en [créer un](#set-up-an-azure-storage-account).</span><span class="sxs-lookup"><span data-stu-id="0585c-122">If you don't have an account you want to use, you can [create one](#set-up-an-azure-storage-account).</span></span> <span data-ttu-id="0585c-123">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0585c-123">Then click **OK**.</span></span>
5. <span data-ttu-id="0585c-124">Sélectionnez le sous-réseau et le réseau Azure auxquels les machines virtuelles Azure se connectent lorsqu’elles sont créées après le basculement.</span><span class="sxs-lookup"><span data-stu-id="0585c-124">Select the Azure network and subnet to which Azure VMs will connect when they're created failover.</span></span>

    - <span data-ttu-id="0585c-125">Sélectionnez **Effectuez maintenant la configuration pour les machines sélectionnées** pour appliquer les paramètre réseau à l’ensemble des machines que vous activez pour la réplication.</span><span class="sxs-lookup"><span data-stu-id="0585c-125">To apply the network settings to all machines you enable for replication, select **Configure now for selected machines**.</span></span>
    - <span data-ttu-id="0585c-126">Sélectionnez **Configurer ultérieurement** pour sélectionner le réseau Azure pour chaque machine.</span><span class="sxs-lookup"><span data-stu-id="0585c-126">Select **Configure later** to select the Azure network per machine.</span></span>
    - <span data-ttu-id="0585c-127">Si vous ne possédez pas de réseau, vous pouvez en [créer un](#set-up-an-azure-network).</span><span class="sxs-lookup"><span data-stu-id="0585c-127">If you don't have a network you want to use, you can [create one](#set-up-an-azure-network).</span></span> <span data-ttu-id="0585c-128">Sélectionnez un sous-réseau, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="0585c-128">Select a subnet if applicable.</span></span> <span data-ttu-id="0585c-129">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0585c-129">Then click **OK**.</span></span>

   ![Activer la réplication](./media/hyper-v-site-walkthrough-enable-replication/enable-replication11.png)

6. <span data-ttu-id="0585c-131">Dans **Machines virtuelles** > **Sélectionner les machines virtuelles**, cliquez sur chaque machine à répliquer.</span><span class="sxs-lookup"><span data-stu-id="0585c-131">In **Virtual Machines** > **Select virtual machines**, click and select each machine you want to replicate.</span></span> <span data-ttu-id="0585c-132">Vous pouvez uniquement sélectionner les machines pour lesquelles la réplication peut être activée.</span><span class="sxs-lookup"><span data-stu-id="0585c-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="0585c-133">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0585c-133">Then click **OK**.</span></span>

    ![Activer la réplication](./media/hyper-v-site-walkthrough-enable-replication/enable-replication5-for-exclude-disk.png)

7. <span data-ttu-id="0585c-135">Dans **Propriétés** > **Configurer les propriétés**, choisissez le système d’exploitation des machines virtuelles sélectionnées, ainsi que le disque du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="0585c-135">In **Properties** > **Configure properties**, select the operating system for the selected VMs, and the OS disk.</span></span>
8. <span data-ttu-id="0585c-136">Vérifiez que le nom de la machine virtuelle Azure (nom de la cible) est conforme à la [configuration requise pour les machines virtuelles Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="0585c-136">Verify that the Azure VM name (target name) complies with [Azure virtual machine requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
9. <span data-ttu-id="0585c-137">Par défaut, tous les disques de la machine virtuelle sont sélectionnés pour la réplication.</span><span class="sxs-lookup"><span data-stu-id="0585c-137">By default all the disks of the VM are selected for replication.</span></span> <span data-ttu-id="0585c-138">Pour exclure des disques, décochez-les.</span><span class="sxs-lookup"><span data-stu-id="0585c-138">Clear disks to exclude them.</span></span>
10. <span data-ttu-id="0585c-139">Cliquez sur **OK** pour enregistrer les modifications.</span><span class="sxs-lookup"><span data-stu-id="0585c-139">Click **OK** to save changes.</span></span> <span data-ttu-id="0585c-140">Vous pouvez opter pour une définition ultérieure des propriétés.</span><span class="sxs-lookup"><span data-stu-id="0585c-140">You can set additional properties later.</span></span>

    ![Activer la réplication](./media/hyper-v-site-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

11. <span data-ttu-id="0585c-142">Dans **Paramètres de réplication** > **Configurer les paramètres de réplication**, sélectionnez la stratégie de réplication que vous souhaitez appliquer aux machines virtuelles protégées.</span><span class="sxs-lookup"><span data-stu-id="0585c-142">In **Replication settings** > **Configure replication settings**, select the replication policy you want to apply for the protected VMs.</span></span> <span data-ttu-id="0585c-143">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0585c-143">Then click **OK**.</span></span> <span data-ttu-id="0585c-144">Vous pouvez modifier la stratégie de réplication dans **Stratégies de réplication** > Nom de la stratégie > **Modifier les paramètres**.</span><span class="sxs-lookup"><span data-stu-id="0585c-144">You can modify the replication policy in **Replication policies** > policy-name > **Edit Settings**.</span></span> <span data-ttu-id="0585c-145">Les modifications que vous appliquez seront utilisées pour les nouvelles machines et les machines dont la réplication est déjà en cours.</span><span class="sxs-lookup"><span data-stu-id="0585c-145">Changes you apply will be used for machines that are already replicating, and new machines.</span></span>


   ![Activer la réplication](./media/hyper-v-site-walkthrough-enable-replication/enable-replication7.png)

<span data-ttu-id="0585c-147">Vous pouvez suivre la progression du travail **Activer la protection** dans **Travaux** > **Travaux Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="0585c-147">You can track progress of the **Enable Protection** job in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="0585c-148">Une fois le travail **Finaliser la protection** exécuté, la machine est prête pour le basculement.</span><span class="sxs-lookup"><span data-stu-id="0585c-148">After the **Finalize Protection** job runs the machine is ready for failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="0585c-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0585c-149">Next steps</span></span>


<span data-ttu-id="0585c-150">Accédez à [Étape 11 : exécuter un test de basculement](hyper-v-site-walkthrough-test-failover.md).</span><span class="sxs-lookup"><span data-stu-id="0585c-150">Go to [Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>
