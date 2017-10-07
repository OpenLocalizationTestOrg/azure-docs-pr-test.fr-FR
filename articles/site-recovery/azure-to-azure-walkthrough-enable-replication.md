---
title: "la réplication de machines virtuelles Azure tooanother région Azure avec Azure Site Recovery aaaEnable | Documents Microsoft"
description: "Résume les étapes hello vous devez tooenable réplication tooanother région Azure pour les machines virtuelles Azure, à l’aide du service d’Azure Site Recovery hello"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a309644f-d36b-4188-bba7-ad45a2d9bede
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 8/01/2017
ms.author: raynew
ms.openlocfilehash: 2fa03db45a18ccb8b9f31ed05589be0dd6d5f031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-enable-replication-for-azure-vms"></a><span data-ttu-id="40aa9-103">Étape 5 : Activer la réplication des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="40aa9-103">Step 5: Enable replication for Azure VMs</span></span>


<span data-ttu-id="40aa9-104">Après avoir configuré un [de coffre Recovery Services](azure-to-azure-walkthrough-vault.md), utilisez cette réplication tooenable de l’article de machines virtuelles (VM), tooanother région Azure, avec [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="40aa9-104">After setting up a [Recovery Services vault](azure-to-azure-walkthrough-vault.md), use this article tooenable replication of virtual machines (VMs), tooanother Azure region, with [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="40aa9-105">tooenable la réplication, vous avez configuré les paramètres source et cible, vérifiez la stratégie de réplication hello et sélectionnez les machines virtuelles que vous souhaitez tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="40aa9-105">tooenable replication, you set up source and target settings, verify hello replication policy, and select VMs you want tooreplicate.</span></span>

- <span data-ttu-id="40aa9-106">Lorsque vous avez terminé l’article hello, vos machines virtuelles Azure doit être réplication toohello de région Azure secondaire.</span><span class="sxs-lookup"><span data-stu-id="40aa9-106">When you finish hello article, your Azure VMs should be replicating toohello secondary Azure region.</span></span>
- <span data-ttu-id="40aa9-107">Valider les commentaires en bas de hello de cet article, ou poser des questions dans hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="40aa9-107">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

>[!NOTE]
>
> <span data-ttu-id="40aa9-108">La réplication de machines virtuelles Azure est actuellement disponible en préversion.</span><span class="sxs-lookup"><span data-stu-id="40aa9-108">Azure VM replication is currently in preview.</span></span>


## <a name="select-hello-source"></a><span data-ttu-id="40aa9-109">Sélectionnez la source de hello</span><span class="sxs-lookup"><span data-stu-id="40aa9-109">Select hello source</span></span> 

1. <span data-ttu-id="40aa9-110">Dans les coffres des Services de récupération, cliquez sur le nom du coffre hello > **+ répliquer**.</span><span class="sxs-lookup"><span data-stu-id="40aa9-110">In Recovery Services vaults, click hello vault name > **+Replicate**.</span></span>
2. <span data-ttu-id="40aa9-111">Dans **Source**, sélectionnez **Azure - PREVIEW**.</span><span class="sxs-lookup"><span data-stu-id="40aa9-111">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="40aa9-112">Dans **emplacement Source**, sélectionnez la source de hello région Azure où vos machines virtuelles en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="40aa9-112">In **Source location**, select hello source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="40aa9-113">Sélectionnez hello **modèle de déploiement de machine virtuelle Azure** pour les ordinateurs virtuels : **le Gestionnaire de ressources** ou **classique**.</span><span class="sxs-lookup"><span data-stu-id="40aa9-113">Select hello **Azure virtual machine deployment model** for VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="40aa9-114">Sélectionnez hello **groupe de ressources Source** pour les machines virtuelles du Gestionnaire de ressources, ou **service de cloud computing** pour les machines virtuelles classiques.</span><span class="sxs-lookup"><span data-stu-id="40aa9-114">Select hello **Source resource group** for Resource Manager VMs, or **cloud service** for classic VMs.</span></span>
5. <span data-ttu-id="40aa9-115">Cliquez sur **OK** toosave les paramètres hello.</span><span class="sxs-lookup"><span data-stu-id="40aa9-115">Click **OK** toosave hello settings.</span></span>

    ![Configurer la source de hello](./media/azure-to-azure-walkthrough-enable-replication/source.png)

## <a name="select-hello-vms"></a><span data-ttu-id="40aa9-117">Sélectionnez les ordinateurs virtuels de hello</span><span class="sxs-lookup"><span data-stu-id="40aa9-117">Select hello VMs</span></span>

<span data-ttu-id="40aa9-118">Site Recovery récupère une liste de hello que machines virtuelles associées à l’abonnement de hello et ressource groupe/service cloud.</span><span class="sxs-lookup"><span data-stu-id="40aa9-118">Site Recovery retrieves a list of hello VMs associated with hello subscription and resource group/cloud service.</span></span>

1. <span data-ttu-id="40aa9-119">Dans **virtuels**, sélectionnez hello machines virtuelles tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="40aa9-119">In **Virtual Machines**, select hello VMs you want tooreplicate.</span></span>
2. <span data-ttu-id="40aa9-120">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="40aa9-120">Click **OK**.</span></span>

    ![Sélectionner les machines virtuelles](./media/azure-to-azure-walkthrough-enable-replication/vms.png)


## <a name="configure-settings"></a><span data-ttu-id="40aa9-122">Configurer les paramètres</span><span class="sxs-lookup"><span data-stu-id="40aa9-122">Configure settings</span></span>

<span data-ttu-id="40aa9-123">Récupération de site configure les paramètres par défaut pour la région cible hello (selon les paramètres de région de code source hello) et la stratégie de réplication hello :</span><span class="sxs-lookup"><span data-stu-id="40aa9-123">Site Recovery provisions default settings for hello target region (based on hello source region settings), and hello replication policy:</span></span>

   - <span data-ttu-id="40aa9-124">**Emplacement cible**: hello cible la région toouse pour la récupération d’urgence.</span><span class="sxs-lookup"><span data-stu-id="40aa9-124">**Target location**: hello target region you want toouse for disaster recovery.</span></span> <span data-ttu-id="40aa9-125">Nous recommandons qu’emplacement cible de hello correspond à emplacement hello de coffre de récupération de Site hello.</span><span class="sxs-lookup"><span data-stu-id="40aa9-125">We recommend that hello target location matches hello location of hello Site Recovery vault.</span></span>
   - <span data-ttu-id="40aa9-126">**Groupe de ressources cible**: groupe de ressources toowhich machines virtuelles Azure dans la région cible hello appartiendra après le basculement.</span><span class="sxs-lookup"><span data-stu-id="40aa9-126">**Target resource group**: Resource group toowhich Azure VMs in hello target region will belong after failover.</span></span> <span data-ttu-id="40aa9-127">Par défaut, Site Recovery crée un nouveau groupe de ressources dans la région cible hello avec un suffixe « asr ».</span><span class="sxs-lookup"><span data-stu-id="40aa9-127">By default, Site Recovery creates a new resource group in hello target region with an "asr" suffix.</span></span> 
   - <span data-ttu-id="40aa9-128">**Réseau virtuel cible**: réseau hello dans les machines virtuelles Azure hello région cible se trouve après le basculement.</span><span class="sxs-lookup"><span data-stu-id="40aa9-128">**Target virtual network**: hello network in which Azure VMs in hello target region will be located after failover.</span></span> <span data-ttu-id="40aa9-129">Par défaut, la récupération de Site crée un nouveau réseau virtuel (et des sous-réseaux) dans la région cible hello avec un suffixe « asr ».</span><span class="sxs-lookup"><span data-stu-id="40aa9-129">By default, Site Recovery creates a new virtual network (and subnets) in hello target region with an "asr" suffix.</span></span> <span data-ttu-id="40aa9-130">Ce réseau est mappé tooyour source réseau.</span><span class="sxs-lookup"><span data-stu-id="40aa9-130">This network is mapped tooyour source network.</span></span> <span data-ttu-id="40aa9-131">Notez que vous pouvez affecter une adresse IP spécifique après le basculement d’un ordinateur virtuel, si vous avez besoin de tooretain hello même adresse IP dans les emplacements source et cible hello.</span><span class="sxs-lookup"><span data-stu-id="40aa9-131">Note that you can assign a specific IP address after failover of a VM, if you need tooretain hello same IP address in hello source and target locations.</span></span> 
   - <span data-ttu-id="40aa9-132">**Comptes de stockage de cache**: récupération de Site utilise un compte de stockage dans la région de la source hello.</span><span class="sxs-lookup"><span data-stu-id="40aa9-132">**Cache storage accounts**: Site Recovery uses a storage account in hello source region.</span></span> <span data-ttu-id="40aa9-133">Modifications sur des machines virtuelles source sont envoyées toothis compte, avant que l’emplacement de la réplication toohello cible.</span><span class="sxs-lookup"><span data-stu-id="40aa9-133">Changes on source VMs are sent toothis account, before replication toohello target location.</span></span> 
   - <span data-ttu-id="40aa9-134">**Cibler des comptes de stockage**: par défaut, Site Recovery crée un nouveau compte de stockage dans la région cible hello, source de hello toomirror compte de stockage de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="40aa9-134">**Target storage accounts**: By default, Site Recovery creates a new storage account in hello target region, toomirror hello source VM storage account.</span></span>
   -  <span data-ttu-id="40aa9-135">**Cibler des groupes à haute disponibilité**: par défaut, Site Recovery crée un nouveau groupe à haute disponibilité région cible hello, avec le suffixe « asr » de hello.</span><span class="sxs-lookup"><span data-stu-id="40aa9-135">**Target availability sets**: By default, Site Recovery creates a new availability set in hello target region, with hello "asr" suffix.</span></span> 
   - <span data-ttu-id="40aa9-136">**Nom de la stratégie de réplication** : nom de la stratégie.</span><span class="sxs-lookup"><span data-stu-id="40aa9-136">**Replication policy name**: Policy name.</span></span>
   - <span data-ttu-id="40aa9-137">**Rétention des points de récupération** : par défaut, Site Recovery conserve les points de récupération pendant 24 heures.</span><span class="sxs-lookup"><span data-stu-id="40aa9-137">**Recovery point retention**: By default Site Recovery keeps recovery points for 24 hours.</span></span> <span data-ttu-id="40aa9-138">Vous pouvez configurer une valeur comprise entre 1 et 72 heures.</span><span class="sxs-lookup"><span data-stu-id="40aa9-138">You can configure a value between 1 and 72 hours.</span></span>
   - <span data-ttu-id="40aa9-139">**Fréquence des instantanés de cohérence des applications** : par défaut, Site Recovery prend un instantané de cohérence des applications toutes les 4 heures.</span><span class="sxs-lookup"><span data-stu-id="40aa9-139">**App-consistent snapshot frequency**: By default Site Recovery takes an app-consistent snapshot every 4 hours.</span></span> <span data-ttu-id="40aa9-140">Vous pouvez configurer une valeur comprise entre 1 et 12 heures.</span><span class="sxs-lookup"><span data-stu-id="40aa9-140">You can configure any value between 1 and 12 hours.</span></span> <span data-ttu-id="40aa9-141">Les données sont répliquées en continu :</span><span class="sxs-lookup"><span data-stu-id="40aa9-141">Data is replicated continuously:</span></span>
    - <span data-ttu-id="40aa9-142">Des points de récupération cohérents d’incident conservent un ordre d’écriture cohérent des données lors de leur création.</span><span class="sxs-lookup"><span data-stu-id="40aa9-142">Crash-consistent recovery points maintain consistent data write-order when created.</span></span> <span data-ttu-id="40aa9-143">Ce type de point de récupération est généralement suffisant si votre application est conçue toorecover à partir d’un incident sans des incohérences de données</span><span class="sxs-lookup"><span data-stu-id="40aa9-143">This type of recovery point is usually sufficient if your app is designed toorecover from a crash without data inconsistencies</span></span>
    - <span data-ttu-id="40aa9-144">Des points de récupération cohérents d’incident sont générés toutes les quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="40aa9-144">Crash-consistent recovery points are generated every few minutes.</span></span> <span data-ttu-id="40aa9-145">À l’aide de ces toofail de points de récupération sur et récupérer vos machines virtuelles fournit un objectif de Point de récupération (RPO) dans l’ordre de hello de minutes.</span><span class="sxs-lookup"><span data-stu-id="40aa9-145">Using these recovery points toofail over and recover your VMs provides a Recovery Point Objective (RPO) in hello order of minutes.</span></span>
    - <span data-ttu-id="40aa9-146">Des points de récupération cohérents au niveau de l’application (dans la cohérence de l’ordre toowrite ajout) assurent que des applications en cours d’exécution terminer toutes les opérations et vider les mémoires tampons toodisk (suspension de l’application).</span><span class="sxs-lookup"><span data-stu-id="40aa9-146">App-consistent recovery points (in addition toowrite-order consistency) ensure that running apps complete all operations and flush buffers toodisk (application quiescing).</span></span> <span data-ttu-id="40aa9-147">Nous vous recommandons d’utiliser ces points de récupération pour les applications de base de données comme SQL Server, Oracle et Exchange.</span><span class="sxs-lookup"><span data-stu-id="40aa9-147">We recommend you use these recovery points for database apps such as SQL Server, Oracle, and Exchange.</span></span>
        
    ![Configurer les paramètres](./media/azure-to-azure-walkthrough-enable-replication/settings.png)


### <a name="modify-settings"></a><span data-ttu-id="40aa9-149">Modifier les paramètres</span><span class="sxs-lookup"><span data-stu-id="40aa9-149">Modify settings</span></span>

<span data-ttu-id="40aa9-150">Si vous souhaitez que les paramètres de stratégie de toomodify cible et la réplication, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="40aa9-150">If you want toomodify target and replication policy settings, do hello following:</span></span>

1. <span data-ttu-id="40aa9-151">tooview ou modifier les paramètres de la cible, cliquez sur **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="40aa9-151">tooview or modify target settings, click **Settings**.</span></span>
2. <span data-ttu-id="40aa9-152">Cliquez sur les paramètres de cible par défaut toooverride hello, **personnaliser**.</span><span class="sxs-lookup"><span data-stu-id="40aa9-152">toooverride hello default target settings, click **Customize**.</span></span> <span data-ttu-id="40aa9-153">Vous pouvez spécifier un groupe de ressources cible, un réseau virtuel, un groupe à haute disponibilité et un compte de stockage cible.</span><span class="sxs-lookup"><span data-stu-id="40aa9-153">You can specify a target resource group, virtual network, availability set, and target storage account.</span></span> <span data-ttu-id="40aa9-154">Vous pouvez uniquement ajouter des groupes à haute disponibilité si les machines virtuelles font partie d’un jeu dans la région de la source hello.</span><span class="sxs-lookup"><span data-stu-id="40aa9-154">You can only add availability sets if VMs are part of a set in hello source region.</span></span>

    ![Configurer les paramètres](./media/azure-to-azure-walkthrough-enable-replication/customize-target.png)

3. <span data-ttu-id="40aa9-156">toooverride les paramètres de réplication pour les points de récupération et des instantanés cohérents au niveau de l’application, cliquez sur **personnaliser** suivant trop**stratégie de réplication**.</span><span class="sxs-lookup"><span data-stu-id="40aa9-156">toooverride replication settings for recovery points and app-consistent snapshots, click **Customize** next too**Replication Policy**.</span></span>
 
    ![Configurer les paramètres](./media/azure-to-azure-walkthrough-enable-replication/customize-policy.png)

4. <span data-ttu-id="40aa9-158">toostart configurer hello cible les ressources, cliquez sur **créer des ressources de la cible**.</span><span class="sxs-lookup"><span data-stu-id="40aa9-158">toostart provisioning hello target resources, click **Create target resources**.</span></span> <span data-ttu-id="40aa9-159">L’approvisionnement prend environ une minute.</span><span class="sxs-lookup"><span data-stu-id="40aa9-159">Provisioning takes a minute or so.</span></span> <span data-ttu-id="40aa9-160">Ne fermez pas les lames hello lors de la configuration, ou vous avez toostart sur.</span><span class="sxs-lookup"><span data-stu-id="40aa9-160">Don't close hello blade during provisioning, or you'll have toostart over.</span></span>




## <a name="enable-replication"></a><span data-ttu-id="40aa9-161">Activer la réplication</span><span class="sxs-lookup"><span data-stu-id="40aa9-161">Enable replication</span></span>

1. <span data-ttu-id="40aa9-162">Dans **Paramètres**, cliquez sur **Activer la réplication**.</span><span class="sxs-lookup"><span data-stu-id="40aa9-162">In **Settings**, click **Enable replication**.</span></span> <span data-ttu-id="40aa9-163">Ainsi, la réplication initiale de hello machines virtuelles que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="40aa9-163">This enables initial replication of hello VMs you selected.</span></span> <span data-ttu-id="40aa9-164">État de réplication initiale peut prendre quelques toorefresh de temps.</span><span class="sxs-lookup"><span data-stu-id="40aa9-164">Initial replication status might take some time toorefresh.</span></span> <span data-ttu-id="40aa9-165">Cliquez sur **Actualiser** état le plus récent tooget hello.</span><span class="sxs-lookup"><span data-stu-id="40aa9-165">Click **Refresh** tooget hello latest status.</span></span>

2. <span data-ttu-id="40aa9-166">Vous pouvez suivre la progression de hello **activer la protection** de la tâche dans **paramètres** > **travaux** > **tâches de récupération de Site**.</span><span class="sxs-lookup"><span data-stu-id="40aa9-166">You can track progress of hello **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

3. <span data-ttu-id="40aa9-167">Dans **paramètres** > **répliquées des éléments**, vous pouvez afficher l’état de hello de machines virtuelles et hello la progression de la réplication initiale.</span><span class="sxs-lookup"><span data-stu-id="40aa9-167">In **Settings** > **Replicated Items**, you can view hello status of VMs and hello initial replication progress.</span></span> <span data-ttu-id="40aa9-168">Cliquez sur hello VM toodrill vers le bas dans ses paramètres.</span><span class="sxs-lookup"><span data-stu-id="40aa9-168">Click hello VM toodrill down into its settings.</span></span>



## <a name="next-steps"></a><span data-ttu-id="40aa9-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="40aa9-169">Next steps</span></span>

<span data-ttu-id="40aa9-170">Accédez trop[étape 6 : exécuter un test de basculement](azure-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="40aa9-170">Go too[Step 6: Run a test failover](azure-to-azure-walkthrough-test-failover.md)</span></span>
