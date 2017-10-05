---
title: "Répliquer des machines virtuelles Azure entre des régions Azure à des fins de récupération d’urgence : Azure vers Azure | Microsoft Docs"
description: "Résume les étapes nécessaires pour répliquer des machines virtuelles Azure entre des régions Azure (Azure vers Azure) avec le service Azure Site Recovery à des fins de récupération d’urgence."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: raynew
ms.openlocfilehash: 9ca33057f6030fdcc233f6053fdc392d62f8f9f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a><span data-ttu-id="77369-103">Répliquer des machines virtuelles Azure entre des régions avec Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="77369-103">Replicate Azure VMs between regions with Azure Site Recovery</span></span>

>[!NOTE]
>
> <span data-ttu-id="77369-104">La réplication Azure Site Recovery pour les machines virtuelles Azure est actuellement en préversion.</span><span class="sxs-lookup"><span data-stu-id="77369-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

<span data-ttu-id="77369-105">Cet article explique comment répliquer des machines virtuelles Azure entre des régions Azure à l’aide du service [Site Recovery](site-recovery-overview.md) dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="77369-105">This article describes how to replicate Azure VMs between Azure regions by using the [Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="77369-106">Publiez des commentaires et des questions au bas de cet article ou sur le [forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="77369-106">Post comments and questions at the bottom of this article or on the [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="disaster-recovery-in-azure"></a><span data-ttu-id="77369-107">Récupération d’urgence dans Azure</span><span class="sxs-lookup"><span data-stu-id="77369-107">Disaster recovery in Azure</span></span>

<span data-ttu-id="77369-108">Les fonctionnalités d’infrastructure Azure intégrées permettent de mettre en place une stratégie de disponibilité solide et fiable pour les charges de travail qui s’exécutent sur des machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="77369-108">Built-in Azure infrastructure capabilities and features contribute to a robust and resilient availability strategy for workloads that run on Azure VMs.</span></span> <span data-ttu-id="77369-109">Toutefois, il existe de nombreuses raisons pour lesquelles vous devez planifier vous-même la récupération d’urgence entre des régions Azure :</span><span class="sxs-lookup"><span data-stu-id="77369-109">However, there are many reasons why you need to plan for disaster recovery between Azure regions yourself:</span></span>

- <span data-ttu-id="77369-110">Vous devez respecter les critères de conformité des applications et des charges de travail spécifiques qui nécessitent une stratégie de continuité des activités et de récupération d’urgence.</span><span class="sxs-lookup"><span data-stu-id="77369-110">You need to meet compliance guidelines for specific apps and workloads that require a business continuity and disaster recovery (BCDR) strategy.</span></span>
- <span data-ttu-id="77369-111">Vous souhaitez pouvoir protéger et récupérer des machines virtuelles Azure en fonction de vos décisions professionnelles, et pas uniquement en fonction des fonctionnalités Azure intégrées.</span><span class="sxs-lookup"><span data-stu-id="77369-111">You want the ability to protect and recover Azure VMs based on your business decisions, and not only based on inbuilt Azure functionality.</span></span>
- <span data-ttu-id="77369-112">Vous devez tester le basculement et la récupération conformément à vos besoins professionnels et de conformité, sans aucun impact sur la production.</span><span class="sxs-lookup"><span data-stu-id="77369-112">You need to test failover and recovery in accordance with your business and compliance needs, with no impact on production.</span></span>
- <span data-ttu-id="77369-113">Vous devez basculer vers la région de récupération en cas de sinistre, puis rebasculer vers la région source d’origine sans interruption.</span><span class="sxs-lookup"><span data-stu-id="77369-113">You need to fail over to the recovery region in the event of a disaster and fail back to the original source region seamlessly.</span></span>

<span data-ttu-id="77369-114">Utilisez Site Recovery pour la réplication des machines virtuelles Azure vers Azure pour vous aider à effectuer toutes ces tâches.</span><span class="sxs-lookup"><span data-stu-id="77369-114">Use Site Recovery for Azure-to-Azure VM replication to help you do all these tasks.</span></span>


## <a name="why-use-site-recovery"></a><span data-ttu-id="77369-115">Pourquoi utiliser Azure Site Recovery ?</span><span class="sxs-lookup"><span data-stu-id="77369-115">Why use Site Recovery?</span></span>      

<span data-ttu-id="77369-116">Site Recovery fournit un moyen simple de répliquer des machines virtuelles Azure d’une région à une autre :</span><span class="sxs-lookup"><span data-stu-id="77369-116">Site Recovery provides a simple way to replicate Azure VMs between regions:</span></span>

- <span data-ttu-id="77369-117">**Déploiement automatique**.</span><span class="sxs-lookup"><span data-stu-id="77369-117">**Automatic deployment**.</span></span> <span data-ttu-id="77369-118">Contrairement à un modèle de réplication actif-actif, aucune infrastructure coûteuse et complexe n’est nécessaire dans la région secondaire.</span><span class="sxs-lookup"><span data-stu-id="77369-118">Unlike an active-active replication model, there's no need for an expensive and complex infrastructure in the secondary region.</span></span> <span data-ttu-id="77369-119">Quand vous activez la réplication, Site Recovery crée automatiquement les ressources nécessaires dans la région cible en fonction des paramètres de la région source.</span><span class="sxs-lookup"><span data-stu-id="77369-119">When you enable replication, Site Recovery automatically creates the required resources in the target region, based on source region settings.</span></span>
- <span data-ttu-id="77369-120">**Contrôle des régions**.</span><span class="sxs-lookup"><span data-stu-id="77369-120">**Control regions**.</span></span> <span data-ttu-id="77369-121">Avec Site Recovery, vous pouvez répliquer de n’importe quelle région vers n’importe quelle région d’un même continent.</span><span class="sxs-lookup"><span data-stu-id="77369-121">With Site Recovery, you can replicate from any region to any region within a continent.</span></span> <span data-ttu-id="77369-122">Comparez ceci au stockage géoredondant avec accès en lecture, qui réplique uniquement de façon asynchrone entre des [régions jumelées](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) standard.</span><span class="sxs-lookup"><span data-stu-id="77369-122">Compare this with read-access geo-redundant storage, which replicates asynchronously between standard [paired regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) only.</span></span> <span data-ttu-id="77369-123">Le stockage géoredondant avec accès en lecture fournit un accès en lecture seule aux données de la région cible.</span><span class="sxs-lookup"><span data-stu-id="77369-123">Read-access geo-redundant storage provides read-only access to the data in the target region.</span></span>
- <span data-ttu-id="77369-124">**Réplication automatisée**.</span><span class="sxs-lookup"><span data-stu-id="77369-124">**Automated replication**.</span></span> <span data-ttu-id="77369-125">Site Recovery fournit une réplication continue automatisée.</span><span class="sxs-lookup"><span data-stu-id="77369-125">Site Recovery provides automated continuous replication.</span></span> <span data-ttu-id="77369-126">Le basculement et la restauration automatique peuvent être déclenchés en un seul clic.</span><span class="sxs-lookup"><span data-stu-id="77369-126">Failover and failback can be triggered with a single click.</span></span>
- <span data-ttu-id="77369-127">**RTO et RPO**.</span><span class="sxs-lookup"><span data-stu-id="77369-127">**RTO and RPO**.</span></span> <span data-ttu-id="77369-128">Site Recovery tire parti de l’infrastructure réseau Azure qui connecte les régions pour maintenir les valeurs RTO (Objectif de délai de récupération) et RPO (Objectif de point de récupération) à un niveau très faible.</span><span class="sxs-lookup"><span data-stu-id="77369-128">Site Recovery takes advantage of the Azure network infrastructure that connects regions to keep RTO and RPO very low.</span></span>
- <span data-ttu-id="77369-129">**Test**.</span><span class="sxs-lookup"><span data-stu-id="77369-129">**Testing**.</span></span> <span data-ttu-id="77369-130">Vous pouvez exécuter des exercices de récupération d’urgence avec des tests de basculement à la demande en fonction de vos besoins, sans affecter vos charges de travail de production ou la réplication continue.</span><span class="sxs-lookup"><span data-stu-id="77369-130">You can run disaster-recovery drills with on-demand test failovers, as and when needed, without affecting your production workloads or ongoing replication.</span></span>
- <span data-ttu-id="77369-131">**Plans de récupération**.</span><span class="sxs-lookup"><span data-stu-id="77369-131">**Recovery plans**.</span></span> <span data-ttu-id="77369-132">Vous pouvez utiliser des plans de récupération pour orchestrer le basculement et la restauration automatique de l’application en cours d’exécution sur plusieurs machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="77369-132">You can use recovery plans to orchestrate failover and failback of the entire application running on multiple VMs.</span></span> <span data-ttu-id="77369-133">La fonctionnalité de plan de récupération offre une parfaite intégration avec les runbooks d’automation Azure.</span><span class="sxs-lookup"><span data-stu-id="77369-133">The recovery plan feature has rich first-class integration with Azure automation runbooks.</span></span>


## <a name="deployment-summary"></a><span data-ttu-id="77369-134">Résumé du déploiement</span><span class="sxs-lookup"><span data-stu-id="77369-134">Deployment summary</span></span>

<span data-ttu-id="77369-135">Voici un résumé de ce que vous devez faire pour configurer la réplication des machines virtuelles entre des régions Azure :</span><span class="sxs-lookup"><span data-stu-id="77369-135">Here's a summary of what you need to do to set up replication of VMs between Azure regions:</span></span>

1. <span data-ttu-id="77369-136">Créez un coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="77369-136">Create a Recovery Services vault.</span></span> <span data-ttu-id="77369-137">Le coffre contient les paramètres de configuration et orchestre la réplication.</span><span class="sxs-lookup"><span data-stu-id="77369-137">The vault contains configuration settings and orchestrates replication.</span></span>
2. <span data-ttu-id="77369-138">Activez la réplication des machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="77369-138">Enable replication for the Azure VMs.</span></span>
3. <span data-ttu-id="77369-139">Exécutez un test de basculement pour vérifier que tout fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="77369-139">Run a test failover to make sure that everything's working as expected.</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="77369-140">Vous pouvez vérifier la [matrice de prise en charge pour la réplication de machines virtuelles Azure](./site-recovery-support-matrix-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="77369-140">You can check the [support matrix for Azure VM replication](./site-recovery-support-matrix-azure-to-azure.md).</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="77369-141">Pour plus d’informations sur la façon de configurer la connectivité réseau sortante nécessaire pour les machines virtuelles Azure pour la réplication Site Recovery, consultez le [document d’aide à la mise en réseau](./site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="77369-141">For information on how to configure the required network outbound connectivity for Azure VMs for Site Recovery replication, see the [networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md).</span></span>

### <a name="before-you-start"></a><span data-ttu-id="77369-142">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="77369-142">Before you start</span></span>

* <span data-ttu-id="77369-143">Pour pouvoir activer la réplication d’une machine virtuelle Azure, votre compte d’utilisateur Azure doit disposer de certaines [autorisations](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="77369-143">Your Azure user account needs to have certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to enable replication of an Azure virtual machine.</span></span>
* <span data-ttu-id="77369-144">Votre abonnement Azure doit être activé pour créer des machines virtuelles à l’emplacement cible que vous souhaitez utiliser en tant que région de récupération d’urgence.</span><span class="sxs-lookup"><span data-stu-id="77369-144">Your Azure subscription should be enabled to create VMs in the target location that you want to use as the disaster recovery region.</span></span> <span data-ttu-id="77369-145">Contactez le support pour activer le quota requis.</span><span class="sxs-lookup"><span data-stu-id="77369-145">Contact support to enable the required quota.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="77369-146">Créer un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="77369-146">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="77369-147">Nous vous recommandons de créer le coffre Recovery Services à l’emplacement où vous souhaitez répliquer vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="77369-147">We recommend that you create the Recovery Services vault in the location where you want your VMs to replicate.</span></span> <span data-ttu-id="77369-148">Par exemple, si votre emplacement cible est la région États-Unis du Centre, créez le coffre dans **États-Unis du Centre**.</span><span class="sxs-lookup"><span data-stu-id="77369-148">For example, if your target location is the central US, create the vault in **Central US**.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="77369-149">Activer la réplication</span><span class="sxs-lookup"><span data-stu-id="77369-149">Enable replication</span></span>

<span data-ttu-id="77369-150">Dans **Coffres Recovery Services**, cliquez sur le nom du coffre.</span><span class="sxs-lookup"><span data-stu-id="77369-150">In **Recovery Services vaults**, click the vault name.</span></span> <span data-ttu-id="77369-151">Dans le coffre, cliquez sur le bouton **+Répliquer**.</span><span class="sxs-lookup"><span data-stu-id="77369-151">In the vault, click the **+Replicate** button.</span></span>

### <a name="step-1-configure-the-source"></a><span data-ttu-id="77369-152">Étape 1.</span><span class="sxs-lookup"><span data-stu-id="77369-152">Step 1.</span></span> <span data-ttu-id="77369-153">Configurer la source</span><span class="sxs-lookup"><span data-stu-id="77369-153">Configure the source</span></span>
1. <span data-ttu-id="77369-154">Dans **Source**, sélectionnez **Azure - PREVIEW**.</span><span class="sxs-lookup"><span data-stu-id="77369-154">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="77369-155">Dans **Emplacement source**, sélectionnez la région Azure source où vos machines virtuelles s’exécutent actuellement.</span><span class="sxs-lookup"><span data-stu-id="77369-155">In **Source location**, select the source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="77369-156">Sélectionnez le modèle de déploiement de vos machines virtuelles : **Resource Manager** ou **Classique**.</span><span class="sxs-lookup"><span data-stu-id="77369-156">Select the deployment model of your VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="77369-157">Sélectionnez le **Groupe de ressources source** pour les machines virtuelles Resource Manager, ou **service cloud** pour les machines virtuelles classiques.</span><span class="sxs-lookup"><span data-stu-id="77369-157">Select the **Source resource group** for Resource Manager VMs or **cloud service** for classic VMs.</span></span>

    ![Configurer la source](./media/site-recovery-azure-to-azure/source.png)

### <a name="step-2-select-virtual-machines"></a><span data-ttu-id="77369-159">Étape 2.</span><span class="sxs-lookup"><span data-stu-id="77369-159">Step 2.</span></span> <span data-ttu-id="77369-160">Sélectionner les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="77369-160">Select virtual machines</span></span>

* <span data-ttu-id="77369-161">Sélectionnez les machines virtuelles à répliquer, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="77369-161">Select the VMs you want to replicate, and then click **OK**.</span></span>

    ![Sélectionner les machines virtuelles](./media/site-recovery-azure-to-azure/vms.png)

### <a name="step-3-configure-settings"></a><span data-ttu-id="77369-163">Étape 3.</span><span class="sxs-lookup"><span data-stu-id="77369-163">Step 3.</span></span> <span data-ttu-id="77369-164">Configurer les paramètres</span><span class="sxs-lookup"><span data-stu-id="77369-164">Configure settings</span></span>

1. <span data-ttu-id="77369-165">Pour remplacer les paramètres cibles par défaut et spécifier les paramètres de votre choix, cliquez sur **Personnaliser**.</span><span class="sxs-lookup"><span data-stu-id="77369-165">To override the default target settings and specify the settings of your choice, click **Customize**.</span></span> <span data-ttu-id="77369-166">Pour plus d’informations, consultez [Personnaliser les ressources cibles](site-recovery-replicate-azure-to-azure.md##customize-target-resources).</span><span class="sxs-lookup"><span data-stu-id="77369-166">For more information, see [Customize target resources](site-recovery-replicate-azure-to-azure.md##customize-target-resources).</span></span>

    ![Configurer les paramètres](./media/site-recovery-azure-to-azure/settings.png)


2. <span data-ttu-id="77369-168">Par défaut, Site Recovery crée une stratégie de réplication qui effectue des captures instantanées de cohérence des applications toutes les quatre heures et conserve les points de récupération pendant 24 heures.</span><span class="sxs-lookup"><span data-stu-id="77369-168">By default, Site Recovery creates a replication policy that takes app-consistent snapshots every 4 hours and retains recovery points for 24 hours.</span></span> <span data-ttu-id="77369-169">Pour créer une stratégie avec des paramètres différents, cliquez sur **Personnaliser** en regard de **Stratégie de réplication**.</span><span class="sxs-lookup"><span data-stu-id="77369-169">To create a policy with different settings, click **Customize** next to **Replication Policy**.</span></span>

    ![Personnaliser la stratégie](./media/site-recovery-azure-to-azure/customize-policy.png)

3. <span data-ttu-id="77369-171">Pour commencer l’approvisionnement des ressources de cibles, cliquez sur **Créer des ressources cibles**.</span><span class="sxs-lookup"><span data-stu-id="77369-171">To start provisioning the target resources, click **Create target resources**.</span></span> <span data-ttu-id="77369-172">L’approvisionnement prend environ une minute.</span><span class="sxs-lookup"><span data-stu-id="77369-172">Provisioning takes a minute or so.</span></span> <span data-ttu-id="77369-173">Ne fermez pas le panneau pendant l’approvisionnement, sinon vous devrez recommencer.</span><span class="sxs-lookup"><span data-stu-id="77369-173">Don't close the blade during provisioning, or you need to start over.</span></span>

4. <span data-ttu-id="77369-174">Pour déclencher la réplication de la machine virtuelle sélectionnée, cliquez sur **Activer la réplication**.</span><span class="sxs-lookup"><span data-stu-id="77369-174">To trigger replication of the selected VM, click **Enable replication**.</span></span>

5. <span data-ttu-id="77369-175">Vous pouvez suivre la progression du travail **Activer la protection** dans **Paramètres** > **Travaux** > **Travaux Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="77369-175">You can track progress of the **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

6. <span data-ttu-id="77369-176">Dans **Paramètres** > **Éléments répliqués**, vous pouvez afficher l’état des machines virtuelles et la progression de la réplication initiale.</span><span class="sxs-lookup"><span data-stu-id="77369-176">In **Settings** > **Replicated Items**, you can view the status of VMs and the initial replication progress.</span></span> <span data-ttu-id="77369-177">Cliquez sur la machine virtuelle pour explorer ses paramètres.</span><span class="sxs-lookup"><span data-stu-id="77369-177">Click the VM to drill down into its settings.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="77369-178">Exécution d’un test de basculement</span><span class="sxs-lookup"><span data-stu-id="77369-178">Run a test failover</span></span>

<span data-ttu-id="77369-179">Après avoir terminé la configuration, exécutez un test de basculement pour vérifier que tout fonctionne comme prévu :</span><span class="sxs-lookup"><span data-stu-id="77369-179">After you set up everything, run a test failover to make sure everything's working as expected:</span></span>

1. <span data-ttu-id="77369-180">Pour effectuer le basculement d’une seule machine, dans **Paramètres** > **Éléments répliqués**, cliquez sur la machine virtuelle, puis sur l’icône **+Tester le basculement**.</span><span class="sxs-lookup"><span data-stu-id="77369-180">To fail over a single machine, in **Settings** > **Replicated Items**, click the VM **+Test Failover** icon.</span></span>

2. <span data-ttu-id="77369-181">Pour effectuer le basculement d’un plan de récupération, dans **Paramètres** > **Plans de récupération**, cliquez avec le bouton droit sur le plan et sélectionnez **Tester le basculement**.</span><span class="sxs-lookup"><span data-stu-id="77369-181">To fail over a recovery plan, in **Settings** > **Recovery Plans**, right-click the plan **Test Failover**.</span></span> <span data-ttu-id="77369-182">Pour créer un plan de récupération, suivez [ces instructions](site-recovery-create-recovery-plans.md).</span><span class="sxs-lookup"><span data-stu-id="77369-182">To create a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span> 

3. <span data-ttu-id="77369-183">Dans **Tester le basculement**, sélectionnez le réseau virtuel Azure cible auquel les machines virtuelles Azure sont connectées après le basculement.</span><span class="sxs-lookup"><span data-stu-id="77369-183">In **Test Failover**, select the target Azure virtual network to which Azure VMs are connected after the failover occurs.</span></span>

4. <span data-ttu-id="77369-184">Pour démarrer le basculement, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="77369-184">To start the failover, click **OK**.</span></span> <span data-ttu-id="77369-185">Pour suivre la progression, cliquez sur la machine virtuelle pour ouvrir ses propriétés.</span><span class="sxs-lookup"><span data-stu-id="77369-185">To track progress, click the VM to open its properties.</span></span> <span data-ttu-id="77369-186">Vous pouvez également cliquer sur le travail **Test de basculement** dans le nom du coffre > **Paramètres** > **Travaux** > **Travaux Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="77369-186">Or you can click the **Test Failover** job in the vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>

5. <span data-ttu-id="77369-187">Une fois le basculement terminé, le réplica de machine Azure apparaît dans le portail Azure > **Machines virtuelles**.</span><span class="sxs-lookup"><span data-stu-id="77369-187">After the failover finishes, the replica Azure machine appears in the Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="77369-188">Assurez-vous que la machine virtuelle présente la taille appropriée, qu’elle est bien connectée au réseau approprié et qu’elle s’exécute.</span><span class="sxs-lookup"><span data-stu-id="77369-188">Make sure that the VM is the appropriate size, that it's connected to the appropriate network, and that it's running.</span></span>

6. <span data-ttu-id="77369-189">Pour supprimer les machines virtuelles qui ont été créées pendant le test de basculement, cliquez sur **Nettoyer le test de basculement** sur l’élément répliqué ou le plan de récupération.</span><span class="sxs-lookup"><span data-stu-id="77369-189">To delete the VMs that were created during the test failover, click **Cleanup test failover** on the replicated item or the recovery plan.</span></span> <span data-ttu-id="77369-190">Cliquez sur **Notes** pour consigner et enregistrer d’éventuelles observations sur le test de basculement.</span><span class="sxs-lookup"><span data-stu-id="77369-190">In **Notes**, record and save any observations associated with the test failover.</span></span> 

<span data-ttu-id="77369-191">Pour plus d’informations sur les tests de basculement, cliquez [ici](site-recovery-test-failover-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="77369-191">[Learn more](site-recovery-test-failover-to-azure.md) about test failovers.</span></span>


## <a name="next-steps"></a><span data-ttu-id="77369-192">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="77369-192">Next steps</span></span>

<span data-ttu-id="77369-193">Après avoir testé le déploiement :</span><span class="sxs-lookup"><span data-stu-id="77369-193">After you test the deployment:</span></span>

- <span data-ttu-id="77369-194">[Apprenez-en davantage](site-recovery-failover.md) sur les différents types de basculement et leur mode exécution.</span><span class="sxs-lookup"><span data-stu-id="77369-194">[Learn more](site-recovery-failover.md) about different types of failovers and how to run them.</span></span>
- <span data-ttu-id="77369-195">En savoir plus sur l’[utilisation des plans de récupération](site-recovery-create-recovery-plans.md) afin de réduire l’objectif de délai de récupération (RTO).</span><span class="sxs-lookup"><span data-stu-id="77369-195">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) to reduce RTO.</span></span>
