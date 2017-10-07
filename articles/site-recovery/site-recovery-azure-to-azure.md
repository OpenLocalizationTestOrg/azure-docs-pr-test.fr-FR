---
title: "Répliquer les machines virtuelles Azure entre les régions Azure pour la récupération d’urgence doit : tooAzure Azure | Documents Microsoft"
description: "Résume les étapes hello vous avez besoin de machines virtuelles Azure de tooreplicate entre les régions Azure (Azure pour Azure) avec le service d’Azure Site Recovery hello pour les besoins de récupération d’urgence."
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
ms.openlocfilehash: c4c425af260a9bcc3dd4dcc13da26109e20f03bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a><span data-ttu-id="31cef-103">Répliquer des machines virtuelles Azure entre des régions avec Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="31cef-103">Replicate Azure VMs between regions with Azure Site Recovery</span></span>

>[!NOTE]
>
> <span data-ttu-id="31cef-104">La réplication Azure Site Recovery pour les machines virtuelles Azure est actuellement en préversion.</span><span class="sxs-lookup"><span data-stu-id="31cef-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

<span data-ttu-id="31cef-105">Cet article décrit comment tooreplicate machines virtuelles Azure entre des régions Azure à l’aide de hello [Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="31cef-105">This article describes how tooreplicate Azure VMs between Azure regions by using hello [Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="31cef-106">Ajouter des commentaires et questions bas hello de cet article ou sur hello [forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="31cef-106">Post comments and questions at hello bottom of this article or on hello [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="disaster-recovery-in-azure"></a><span data-ttu-id="31cef-107">Récupération d’urgence dans Azure</span><span class="sxs-lookup"><span data-stu-id="31cef-107">Disaster recovery in Azure</span></span>

<span data-ttu-id="31cef-108">Fonctionnalités et fonctions d’infrastructure Azure intégrée contribuent tooa stratégie de disponibilité solide et fiable pour les charges de travail qui s’exécutent sur des machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="31cef-108">Built-in Azure infrastructure capabilities and features contribute tooa robust and resilient availability strategy for workloads that run on Azure VMs.</span></span> <span data-ttu-id="31cef-109">Toutefois, il existe de nombreuses raisons pour lesquelles vous devez tooplan pour la récupération d’urgence entre les régions Azure vous-même :</span><span class="sxs-lookup"><span data-stu-id="31cef-109">However, there are many reasons why you need tooplan for disaster recovery between Azure regions yourself:</span></span>

- <span data-ttu-id="31cef-110">Vous avez besoin en matière de conformité toomeet pour des applications spécifiques et les charges de travail qui nécessitent une continuité des activités et la stratégie de récupération d’urgence.</span><span class="sxs-lookup"><span data-stu-id="31cef-110">You need toomeet compliance guidelines for specific apps and workloads that require a business continuity and disaster recovery (BCDR) strategy.</span></span>
- <span data-ttu-id="31cef-111">Hello capacité tooprotect et de récupérer les machines virtuelles de Azure en fonction de vos décisions professionnelles et pas uniquement basée sur la fonctionnalité Azure intégrée.</span><span class="sxs-lookup"><span data-stu-id="31cef-111">You want hello ability tooprotect and recover Azure VMs based on your business decisions, and not only based on inbuilt Azure functionality.</span></span>
- <span data-ttu-id="31cef-112">Vous devez tootest basculement et récupération conformément à vos besoins commerciaux et de conformité, sans aucun impact sur la production.</span><span class="sxs-lookup"><span data-stu-id="31cef-112">You need tootest failover and recovery in accordance with your business and compliance needs, with no impact on production.</span></span>
- <span data-ttu-id="31cef-113">Vous devez toofail de région de récupération toohello dans les cas de hello d’urgence et que vous échouer de région de la source d’origine toohello arrière en toute transparence.</span><span class="sxs-lookup"><span data-stu-id="31cef-113">You need toofail over toohello recovery region in hello event of a disaster and fail back toohello original source region seamlessly.</span></span>

<span data-ttu-id="31cef-114">Utilisez la récupération de Site pour la machine virtuelle Azure à Azure réplication toohelp vous effectuer toutes ces tâches.</span><span class="sxs-lookup"><span data-stu-id="31cef-114">Use Site Recovery for Azure-to-Azure VM replication toohelp you do all these tasks.</span></span>


## <a name="why-use-site-recovery"></a><span data-ttu-id="31cef-115">Pourquoi utiliser Azure Site Recovery ?</span><span class="sxs-lookup"><span data-stu-id="31cef-115">Why use Site Recovery?</span></span>      

<span data-ttu-id="31cef-116">Récupération de site fournit un moyen simple de tooreplicate machines virtuelles Azure entre les régions :</span><span class="sxs-lookup"><span data-stu-id="31cef-116">Site Recovery provides a simple way tooreplicate Azure VMs between regions:</span></span>

- <span data-ttu-id="31cef-117">**Déploiement automatique**.</span><span class="sxs-lookup"><span data-stu-id="31cef-117">**Automatic deployment**.</span></span> <span data-ttu-id="31cef-118">Contrairement à un modèle de réplication d’actif-actif, il est inutile d’une infrastructure coûteuse et complexe dans la région secondaire hello.</span><span class="sxs-lookup"><span data-stu-id="31cef-118">Unlike an active-active replication model, there's no need for an expensive and complex infrastructure in hello secondary region.</span></span> <span data-ttu-id="31cef-119">Lorsque vous activez la réplication, Site Recovery crée automatiquement les ressources de hello requis dans la région cible hello, selon les paramètres de région de code source.</span><span class="sxs-lookup"><span data-stu-id="31cef-119">When you enable replication, Site Recovery automatically creates hello required resources in hello target region, based on source region settings.</span></span>
- <span data-ttu-id="31cef-120">**Contrôle des régions**.</span><span class="sxs-lookup"><span data-stu-id="31cef-120">**Control regions**.</span></span> <span data-ttu-id="31cef-121">Site Recovery, vous pouvez répliquer à partir de n’importe quelle région tooany de région sur un continent.</span><span class="sxs-lookup"><span data-stu-id="31cef-121">With Site Recovery, you can replicate from any region tooany region within a continent.</span></span> <span data-ttu-id="31cef-122">Comparez ceci au stockage géoredondant avec accès en lecture, qui réplique uniquement de façon asynchrone entre des [régions jumelées](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) standard.</span><span class="sxs-lookup"><span data-stu-id="31cef-122">Compare this with read-access geo-redundant storage, which replicates asynchronously between standard [paired regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) only.</span></span> <span data-ttu-id="31cef-123">Un stockage géo-redondant avec accès en lecture fournit des données de toohello d’accès en lecture seule dans la région cible hello.</span><span class="sxs-lookup"><span data-stu-id="31cef-123">Read-access geo-redundant storage provides read-only access toohello data in hello target region.</span></span>
- <span data-ttu-id="31cef-124">**Réplication automatisée**.</span><span class="sxs-lookup"><span data-stu-id="31cef-124">**Automated replication**.</span></span> <span data-ttu-id="31cef-125">Site Recovery fournit une réplication continue automatisée.</span><span class="sxs-lookup"><span data-stu-id="31cef-125">Site Recovery provides automated continuous replication.</span></span> <span data-ttu-id="31cef-126">Le basculement et la restauration automatique peuvent être déclenchés en un seul clic.</span><span class="sxs-lookup"><span data-stu-id="31cef-126">Failover and failback can be triggered with a single click.</span></span>
- <span data-ttu-id="31cef-127">**RTO et RPO**.</span><span class="sxs-lookup"><span data-stu-id="31cef-127">**RTO and RPO**.</span></span> <span data-ttu-id="31cef-128">Récupération de site tire parti de l’infrastructure réseau Azure hello se connecte régions tookeep RTO et le RPO très faible.</span><span class="sxs-lookup"><span data-stu-id="31cef-128">Site Recovery takes advantage of hello Azure network infrastructure that connects regions tookeep RTO and RPO very low.</span></span>
- <span data-ttu-id="31cef-129">**Test**.</span><span class="sxs-lookup"><span data-stu-id="31cef-129">**Testing**.</span></span> <span data-ttu-id="31cef-130">Vous pouvez exécuter des exercices de récupération d’urgence avec des tests de basculement à la demande en fonction de vos besoins, sans affecter vos charges de travail de production ou la réplication continue.</span><span class="sxs-lookup"><span data-stu-id="31cef-130">You can run disaster-recovery drills with on-demand test failovers, as and when needed, without affecting your production workloads or ongoing replication.</span></span>
- <span data-ttu-id="31cef-131">**Plans de récupération**.</span><span class="sxs-lookup"><span data-stu-id="31cef-131">**Recovery plans**.</span></span> <span data-ttu-id="31cef-132">Vous pouvez utiliser le basculement de tooorchestrate de plans de récupération et de restauration de hello ensemble de l’application en cours d’exécution sur plusieurs machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="31cef-132">You can use recovery plans tooorchestrate failover and failback of hello entire application running on multiple VMs.</span></span> <span data-ttu-id="31cef-133">fonctionnalité de plan de récupération Hello a riche integration de première classe aux runbooks Azure automation.</span><span class="sxs-lookup"><span data-stu-id="31cef-133">hello recovery plan feature has rich first-class integration with Azure automation runbooks.</span></span>


## <a name="deployment-summary"></a><span data-ttu-id="31cef-134">Résumé du déploiement</span><span class="sxs-lookup"><span data-stu-id="31cef-134">Deployment summary</span></span>

<span data-ttu-id="31cef-135">Voici un résumé de ce que vous devez tooset toodo la réplication des machines virtuelles entre les régions Azure :</span><span class="sxs-lookup"><span data-stu-id="31cef-135">Here's a summary of what you need toodo tooset up replication of VMs between Azure regions:</span></span>

1. <span data-ttu-id="31cef-136">Créez un coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="31cef-136">Create a Recovery Services vault.</span></span> <span data-ttu-id="31cef-137">coffre de Hello contient les paramètres de configuration et orchestre la réplication.</span><span class="sxs-lookup"><span data-stu-id="31cef-137">hello vault contains configuration settings and orchestrates replication.</span></span>
2. <span data-ttu-id="31cef-138">Activer la réplication pour hello machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="31cef-138">Enable replication for hello Azure VMs.</span></span>
3. <span data-ttu-id="31cef-139">Exécutez toomake d’un basculement test assurer que tout fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="31cef-139">Run a test failover toomake sure that everything's working as expected.</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="31cef-140">Vous pouvez vérifier hello [matrice de prise en charge pour la réplication de la machine virtuelle Azure](./site-recovery-support-matrix-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="31cef-140">You can check hello [support matrix for Azure VM replication](./site-recovery-support-matrix-azure-to-azure.md).</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="31cef-141">Pour plus d’informations sur comment tooconfigure hello requis connectivité sortante du réseau de machines virtuelles Azure pour la réplication de Site Recovery, consultez hello [document du Guide de mise en réseau](./site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="31cef-141">For information on how tooconfigure hello required network outbound connectivity for Azure VMs for Site Recovery replication, see hello [networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md).</span></span>

### <a name="before-you-start"></a><span data-ttu-id="31cef-142">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="31cef-142">Before you start</span></span>

* <span data-ttu-id="31cef-143">Votre compte d’utilisateur Azure doit toohave certaines [autorisations](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable la réplication d’une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="31cef-143">Your Azure user account needs toohave certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of an Azure virtual machine.</span></span>
* <span data-ttu-id="31cef-144">Votre abonnement Azure doit être VMs toocreate activée dans l’emplacement cible de hello que vous souhaitez toouse comme région de récupération d’urgence hello.</span><span class="sxs-lookup"><span data-stu-id="31cef-144">Your Azure subscription should be enabled toocreate VMs in hello target location that you want toouse as hello disaster recovery region.</span></span> <span data-ttu-id="31cef-145">Contactez le support technique tooenable hello quota requis.</span><span class="sxs-lookup"><span data-stu-id="31cef-145">Contact support tooenable hello required quota.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="31cef-146">Créer un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="31cef-146">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="31cef-147">Nous vous recommandons de créer le coffre Recovery Services hello dans hello emplacement où votre tooreplicate de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="31cef-147">We recommend that you create hello Recovery Services vault in hello location where you want your VMs tooreplicate.</span></span> <span data-ttu-id="31cef-148">Par exemple, si votre emplacement cible est hello central US, créer dans le coffre hello **du centre des États-Unis**.</span><span class="sxs-lookup"><span data-stu-id="31cef-148">For example, if your target location is hello central US, create hello vault in **Central US**.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="31cef-149">Activer la réplication</span><span class="sxs-lookup"><span data-stu-id="31cef-149">Enable replication</span></span>

<span data-ttu-id="31cef-150">Dans **les coffres de Services de récupération**, cliquez sur le nom du coffre hello.</span><span class="sxs-lookup"><span data-stu-id="31cef-150">In **Recovery Services vaults**, click hello vault name.</span></span> <span data-ttu-id="31cef-151">Dans le coffre de hello, cliquez sur hello **+ répliquer** bouton.</span><span class="sxs-lookup"><span data-stu-id="31cef-151">In hello vault, click hello **+Replicate** button.</span></span>

### <a name="step-1-configure-hello-source"></a><span data-ttu-id="31cef-152">Étape 1.</span><span class="sxs-lookup"><span data-stu-id="31cef-152">Step 1.</span></span> <span data-ttu-id="31cef-153">Configurer la source de hello</span><span class="sxs-lookup"><span data-stu-id="31cef-153">Configure hello source</span></span>
1. <span data-ttu-id="31cef-154">Dans **Source**, sélectionnez **Azure - PREVIEW**.</span><span class="sxs-lookup"><span data-stu-id="31cef-154">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="31cef-155">Dans **emplacement Source**, sélectionnez la source de hello région Azure où vos machines virtuelles en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="31cef-155">In **Source location**, select hello source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="31cef-156">Modèle de déploiement sélectionnez hello de vos machines virtuelles : **le Gestionnaire de ressources** ou **classique**.</span><span class="sxs-lookup"><span data-stu-id="31cef-156">Select hello deployment model of your VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="31cef-157">Sélectionnez hello **groupe de ressources Source** pour les machines virtuelles du Gestionnaire de ressources ou **service de cloud computing** pour les machines virtuelles classiques.</span><span class="sxs-lookup"><span data-stu-id="31cef-157">Select hello **Source resource group** for Resource Manager VMs or **cloud service** for classic VMs.</span></span>

    ![Configurer la source de hello](./media/site-recovery-azure-to-azure/source.png)

### <a name="step-2-select-virtual-machines"></a><span data-ttu-id="31cef-159">Étape 2.</span><span class="sxs-lookup"><span data-stu-id="31cef-159">Step 2.</span></span> <span data-ttu-id="31cef-160">Sélectionner les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="31cef-160">Select virtual machines</span></span>

* <span data-ttu-id="31cef-161">Sélectionnez les machines virtuelles de hello vous souhaitez tooreplicate, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="31cef-161">Select hello VMs you want tooreplicate, and then click **OK**.</span></span>

    ![Sélectionner les machines virtuelles](./media/site-recovery-azure-to-azure/vms.png)

### <a name="step-3-configure-settings"></a><span data-ttu-id="31cef-163">Étape 3.</span><span class="sxs-lookup"><span data-stu-id="31cef-163">Step 3.</span></span> <span data-ttu-id="31cef-164">Configurer les paramètres</span><span class="sxs-lookup"><span data-stu-id="31cef-164">Configure settings</span></span>

1. <span data-ttu-id="31cef-165">par défaut de toooverride hello cibler des paramètres et spécifiez les paramètres de hello de votre choix, cliquez sur **personnaliser**.</span><span class="sxs-lookup"><span data-stu-id="31cef-165">toooverride hello default target settings and specify hello settings of your choice, click **Customize**.</span></span> <span data-ttu-id="31cef-166">Pour plus d’informations, consultez [Personnaliser les ressources cibles](site-recovery-replicate-azure-to-azure.md##customize-target-resources).</span><span class="sxs-lookup"><span data-stu-id="31cef-166">For more information, see [Customize target resources](site-recovery-replicate-azure-to-azure.md##customize-target-resources).</span></span>

    ![Configurer les paramètres](./media/site-recovery-azure-to-azure/settings.png)


2. <span data-ttu-id="31cef-168">Par défaut, Site Recovery crée une stratégie de réplication qui effectue des captures instantanées de cohérence des applications toutes les quatre heures et conserve les points de récupération pendant 24 heures.</span><span class="sxs-lookup"><span data-stu-id="31cef-168">By default, Site Recovery creates a replication policy that takes app-consistent snapshots every 4 hours and retains recovery points for 24 hours.</span></span> <span data-ttu-id="31cef-169">toocreate une stratégie avec des paramètres différents, cliquez sur **personnaliser** suivant trop**stratégie de réplication**.</span><span class="sxs-lookup"><span data-stu-id="31cef-169">toocreate a policy with different settings, click **Customize** next too**Replication Policy**.</span></span>

    ![Personnaliser la stratégie](./media/site-recovery-azure-to-azure/customize-policy.png)

3. <span data-ttu-id="31cef-171">toostart configurer hello cible les ressources, cliquez sur **créer des ressources de la cible**.</span><span class="sxs-lookup"><span data-stu-id="31cef-171">toostart provisioning hello target resources, click **Create target resources**.</span></span> <span data-ttu-id="31cef-172">L’approvisionnement prend environ une minute.</span><span class="sxs-lookup"><span data-stu-id="31cef-172">Provisioning takes a minute or so.</span></span> <span data-ttu-id="31cef-173">Ne fermez pas les lames hello lors de la configuration, ou vous devez toostart sur.</span><span class="sxs-lookup"><span data-stu-id="31cef-173">Don't close hello blade during provisioning, or you need toostart over.</span></span>

4. <span data-ttu-id="31cef-174">réplication tootrigger Hello sélectionné la machine virtuelle, cliquez sur **activer la réplication**.</span><span class="sxs-lookup"><span data-stu-id="31cef-174">tootrigger replication of hello selected VM, click **Enable replication**.</span></span>

5. <span data-ttu-id="31cef-175">Vous pouvez suivre la progression de hello **activer la protection** de la tâche dans **paramètres** > **travaux** > **tâches de récupération de Site**.</span><span class="sxs-lookup"><span data-stu-id="31cef-175">You can track progress of hello **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

6. <span data-ttu-id="31cef-176">Dans **paramètres** > **répliquées des éléments**, vous pouvez afficher l’état de hello de machines virtuelles et hello la progression de la réplication initiale.</span><span class="sxs-lookup"><span data-stu-id="31cef-176">In **Settings** > **Replicated Items**, you can view hello status of VMs and hello initial replication progress.</span></span> <span data-ttu-id="31cef-177">Cliquez sur hello VM toodrill vers le bas dans ses paramètres.</span><span class="sxs-lookup"><span data-stu-id="31cef-177">Click hello VM toodrill down into its settings.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="31cef-178">Exécution d’un test de basculement</span><span class="sxs-lookup"><span data-stu-id="31cef-178">Run a test failover</span></span>

<span data-ttu-id="31cef-179">Une fois que vous avez tout configuré, exécutez un toomake de basculement de test que tout fonctionne comme prévu :</span><span class="sxs-lookup"><span data-stu-id="31cef-179">After you set up everything, run a test failover toomake sure everything's working as expected:</span></span>

1. <span data-ttu-id="31cef-180">toofail sur un seul ordinateur, dans **paramètres** > **répliquées des éléments**, cliquez sur la machine virtuelle de hello **+ Test de basculement** icône.</span><span class="sxs-lookup"><span data-stu-id="31cef-180">toofail over a single machine, in **Settings** > **Replicated Items**, click hello VM **+Test Failover** icon.</span></span>

2. <span data-ttu-id="31cef-181">toofail sur la récupération d’un plan, en **paramètres** > **les Plans de récupération**, plan de hello avec le bouton **Test de basculement**.</span><span class="sxs-lookup"><span data-stu-id="31cef-181">toofail over a recovery plan, in **Settings** > **Recovery Plans**, right-click hello plan **Test Failover**.</span></span> <span data-ttu-id="31cef-182">toocreate un plan de récupération, [suivez ces instructions](site-recovery-create-recovery-plans.md).</span><span class="sxs-lookup"><span data-stu-id="31cef-182">toocreate a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span> 

3. <span data-ttu-id="31cef-183">Dans **Test de basculement**, sélectionnez toowhich de réseau virtuel Azure cible hello machines virtuelles Azure sont connectés après basculement hello.</span><span class="sxs-lookup"><span data-stu-id="31cef-183">In **Test Failover**, select hello target Azure virtual network toowhich Azure VMs are connected after hello failover occurs.</span></span>

4. <span data-ttu-id="31cef-184">toostart hello de basculement, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="31cef-184">toostart hello failover, click **OK**.</span></span> <span data-ttu-id="31cef-185">tootrack de progression, cliquez sur hello VM tooopen ses propriétés.</span><span class="sxs-lookup"><span data-stu-id="31cef-185">tootrack progress, click hello VM tooopen its properties.</span></span> <span data-ttu-id="31cef-186">Vous pouvez également cliquer sur hello **Test de basculement** travail dans le nom du coffre hello > **paramètres** > **travaux** > **les tâches de récupération de Site**.</span><span class="sxs-lookup"><span data-stu-id="31cef-186">Or you can click hello **Test Failover** job in hello vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>

5. <span data-ttu-id="31cef-187">Après avoir hello basculement se termine, le réplica de hello machine Azure s’affiche dans hello portail Azure > **virtuels**.</span><span class="sxs-lookup"><span data-stu-id="31cef-187">After hello failover finishes, hello replica Azure machine appears in hello Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="31cef-188">Assurez-vous que cette machine virtuelle hello est la taille appropriée de hello, que sa connexion réseau approprié de toohello, et qu’il s’exécute.</span><span class="sxs-lookup"><span data-stu-id="31cef-188">Make sure that hello VM is hello appropriate size, that it's connected toohello appropriate network, and that it's running.</span></span>

6. <span data-ttu-id="31cef-189">toodelete hello machines virtuelles qui ont été créés pendant le basculement de test hello, cliquez sur **basculement de test de nettoyage** sur hello répliquées élément hello ou un plan de récupération.</span><span class="sxs-lookup"><span data-stu-id="31cef-189">toodelete hello VMs that were created during hello test failover, click **Cleanup test failover** on hello replicated item or hello recovery plan.</span></span> <span data-ttu-id="31cef-190">Dans **Notes**, enregistrer et enregistrer toutes les observations associées au basculement de test hello.</span><span class="sxs-lookup"><span data-stu-id="31cef-190">In **Notes**, record and save any observations associated with hello test failover.</span></span> 

<span data-ttu-id="31cef-191">Pour plus d’informations sur les tests de basculement, cliquez [ici](site-recovery-test-failover-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="31cef-191">[Learn more](site-recovery-test-failover-to-azure.md) about test failovers.</span></span>


## <a name="next-steps"></a><span data-ttu-id="31cef-192">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="31cef-192">Next steps</span></span>

<span data-ttu-id="31cef-193">Après avoir tester le déploiement de hello :</span><span class="sxs-lookup"><span data-stu-id="31cef-193">After you test hello deployment:</span></span>

- <span data-ttu-id="31cef-194">[En savoir plus](site-recovery-failover.md) sur différents types de basculement et la manière dont toorun les.</span><span class="sxs-lookup"><span data-stu-id="31cef-194">[Learn more](site-recovery-failover.md) about different types of failovers and how toorun them.</span></span>
- <span data-ttu-id="31cef-195">En savoir plus sur [à l’aide de plans de récupération](site-recovery-create-recovery-plans.md) tooreduce RTO.</span><span class="sxs-lookup"><span data-stu-id="31cef-195">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) tooreduce RTO.</span></span>
