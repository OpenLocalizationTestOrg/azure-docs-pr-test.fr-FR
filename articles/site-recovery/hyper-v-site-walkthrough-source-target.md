---
title: "aaaSet hello source et un cible pour tooAzure de réplication Hyper-V (sans System Center VMM) avec Azure Site Recovery | Documents Microsoft"
description: "Résume les tooset d’étapes hello les paramètres source et cible pour la réplication de stockage de tooAzure d’ordinateurs virtuels Hyper-V avec Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d2010d85-77fd-4dea-84f3-1c960ed4c63f
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 105b90e6ac053d5b842c54a36c460a26d0f5c2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-replication-tooazure"></a><span data-ttu-id="8814a-103">Étape 8 : Configurer la source de hello et cible pour tooAzure de réplication Hyper-V</span><span class="sxs-lookup"><span data-stu-id="8814a-103">Step 8: Set up hello source and target for Hyper-V replication tooAzure</span></span>

<span data-ttu-id="8814a-104">Cet article décrit comment tooconfigure les paramètres de source et cible lors de la réplication locale tooAzure d’ordinateurs virtuels (sans System Center VMM) Hyper-V, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8814a-104">This article describes how tooconfigure source and target settings when replicating on-premises Hyper-V virtual machines (without System Center VMM) tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="8814a-105">Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="8814a-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="8814a-106">Configurer l’environnement source hello</span><span class="sxs-lookup"><span data-stu-id="8814a-106">Set up hello source environment</span></span>

<span data-ttu-id="8814a-107">Configurer le site de hello Hyper-V, installer hello fournisseur Azure Site Recovery et hello Azure Recovery Services agent sur les ordinateurs hôtes Hyper-V et inscrire le site de hello dans le coffre hello.</span><span class="sxs-lookup"><span data-stu-id="8814a-107">Set up hello Hyper-V site, install hello Azure Site Recovery Provider and hello Azure Recovery Services agent on Hyper-V hosts, and register hello site in hello vault.</span></span>

1. <span data-ttu-id="8814a-108">Dans **Préparer l’infrastructure**, cliquez sur **Source**.</span><span class="sxs-lookup"><span data-stu-id="8814a-108">In **Prepare Infrastructure**, click **Source**.</span></span> <span data-ttu-id="8814a-109">tooadd un nouveau site Hyper-V en tant que conteneur pour vos ordinateurs hôtes Hyper-V ou des clusters, cliquez sur **+ Site Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="8814a-109">tooadd a new Hyper-V site as a container for your Hyper-V hosts or clusters, click **+Hyper-V Site**.</span></span>

    ![Configurer la source](./media/hyper-v-site-walkthrough-source-target/set-source1.png)
2. <span data-ttu-id="8814a-111">Dans **site Hyper-V créer**, spécifiez un nom pour le site de hello.</span><span class="sxs-lookup"><span data-stu-id="8814a-111">In **Create Hyper-V site**, specify a name for hello site.</span></span> <span data-ttu-id="8814a-112">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="8814a-112">Then click **OK**.</span></span> <span data-ttu-id="8814a-113">À présent, sélectionnez site hello vous créé, puis cliquez sur **+ Hyper-V Server** tooadd un site toohello du serveur.</span><span class="sxs-lookup"><span data-stu-id="8814a-113">Now, select hello site you created, and click **+Hyper-V Server** tooadd a server toohello site.</span></span>

    ![Configurer la source](./media/hyper-v-site-walkthrough-source-target/set-source2.png)

3. <span data-ttu-id="8814a-115">Dans **Ajouter un serveur** > **Type de serveur**, vérifiez que **Serveur Hyper-V** est affiché.</span><span class="sxs-lookup"><span data-stu-id="8814a-115">In **Add Server** > **Server type**, check that **Hyper-V server** is displayed.</span></span>

    - <span data-ttu-id="8814a-116">Assurez-vous que server hello Hyper-V que vous souhaitez tooadd est conforme à hello [conditions préalables](#on-premises-prerequisites), et est en mesure de tooaccess hello URL spécifiées.</span><span class="sxs-lookup"><span data-stu-id="8814a-116">Make sure that hello Hyper-V server you want tooadd complies with hello [prerequisites](#on-premises-prerequisites), and is able tooaccess hello specified URLs.</span></span>
    - <span data-ttu-id="8814a-117">Téléchargez le fichier d’installation hello fournisseur Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="8814a-117">Download hello Azure Site Recovery Provider installation file.</span></span> <span data-ttu-id="8814a-118">Vous exécutez cette hello tooinstall de fichier fournisseur et hello agent Recovery Services sur chaque ordinateur hôte Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="8814a-118">You run this file tooinstall hello Provider and hello Recovery Services agent on each Hyper-V host.</span></span>

    ![Configurer la source](./media/hyper-v-site-walkthrough-source-target/set-source3.png)


## <a name="install-hello-provider-and-agent"></a><span data-ttu-id="8814a-120">Installer hello fournisseur et l’agent</span><span class="sxs-lookup"><span data-stu-id="8814a-120">Install hello Provider and agent</span></span>

1. <span data-ttu-id="8814a-121">Exécutez le fichier de configuration de fournisseur hello sur chaque ordinateur hôte ajouté toohello Hyper-V site.</span><span class="sxs-lookup"><span data-stu-id="8814a-121">Run hello Provider setup file on each host you added toohello Hyper-V site.</span></span> <span data-ttu-id="8814a-122">Si vous effectuez l’installation sur un cluster Hyper-V, exécutez le programme d’installation sur chaque nœud du cluster.</span><span class="sxs-lookup"><span data-stu-id="8814a-122">If you're installing on a Hyper-V cluster, run setup on each cluster node.</span></span> <span data-ttu-id="8814a-123">L’installation et l’inscription de chaque nœud de cluster Hyper-V permettent de s’assurer que les machines virtuelles sont protégées, même si elles migrent entre les nœuds.</span><span class="sxs-lookup"><span data-stu-id="8814a-123">Installing and registering each Hyper-V cluster node ensures that VMs are protected, even if they migrate across nodes.</span></span>
2. <span data-ttu-id="8814a-124">Dans **Microsoft Update**, vous pouvez choisir des mises à jour, pour que celles du fournisseur soient installées conformément à votre stratégie Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="8814a-124">In **Microsoft Update**, you can opt in for updates so that Provider updates are installed in accordance with your Microsoft Update policy.</span></span>
3. <span data-ttu-id="8814a-125">Dans **Installation**, acceptez ou modifiez l’emplacement d’installation fournisseur hello par défaut et cliquez sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="8814a-125">In **Installation**, accept or modify hello default Provider installation location and click **Install**.</span></span>
4. <span data-ttu-id="8814a-126">Dans **paramètres du coffre**, cliquez sur **Parcourir** tooselect hello coffre fichier de clé que vous avez téléchargé.</span><span class="sxs-lookup"><span data-stu-id="8814a-126">In **Vault Settings**, click **Browse** tooselect hello vault key file that you downloaded.</span></span> <span data-ttu-id="8814a-127">Spécifier l’abonnement Azure Site Recovery de hello, nom du coffre hello, et hello Hyper-V site toowhich hello Hyper-V serveur appartient.</span><span class="sxs-lookup"><span data-stu-id="8814a-127">Specify hello Azure Site Recovery subscription, hello vault name, and hello Hyper-V site toowhich hello Hyper-V server belongs.</span></span>

    ![Enregistrement du serveur](./media/hyper-v-site-walkthrough-source-target/provider3.png)

5. <span data-ttu-id="8814a-129">Dans **paramètres Proxy**, spécifiez comment hello fournisseur en cours d’exécution sur les ordinateurs hôtes Hyper-V connecte tooAzure Site Recovery via hello internet.</span><span class="sxs-lookup"><span data-stu-id="8814a-129">In **Proxy Settings**, specify how hello Provider running on Hyper-V hosts connects tooAzure Site Recovery over hello internet.</span></span>

    * <span data-ttu-id="8814a-130">Si vous souhaitez sélectionner directement que hello fournisseur tooconnect **vous connecter directement tooAzure Site Recovery sans proxy**.</span><span class="sxs-lookup"><span data-stu-id="8814a-130">If you want hello Provider tooconnect directly select **Connect directly tooAzure Site Recovery without a proxy**.</span></span>
    * <span data-ttu-id="8814a-131">Si votre proxy existant nécessite une authentification, ou que vous souhaitez toouse un proxy personnalisé pour la connexion du fournisseur hello, sélectionnez **tooAzure Site Recovery à l’aide d’un serveur proxy de connexion**.</span><span class="sxs-lookup"><span data-stu-id="8814a-131">If your existing proxy requires authentication, or you want toouse a custom proxy for hello Provider connection, select **Connect tooAzure Site Recovery using a proxy server**.</span></span>
    * <span data-ttu-id="8814a-132">Si vous utilisez un proxy :</span><span class="sxs-lookup"><span data-stu-id="8814a-132">If you use a proxy:</span></span>
        - <span data-ttu-id="8814a-133">Spécifiez les informations d’identification, le port et adresse de hello</span><span class="sxs-lookup"><span data-stu-id="8814a-133">Specify hello address, port, and credentials</span></span>
        - <span data-ttu-id="8814a-134">Vérifiez que hello URL décrites dans hello [conditions préalables](#prerequisites) sont autorisées via le proxy hello.</span><span class="sxs-lookup"><span data-stu-id="8814a-134">Make sure hello URLs described in hello [prerequisites](#prerequisites) are allowed through hello proxy.</span></span>

    ![Internet](./media/hyper-v-site-walkthrough-source-target/provider7.png)

6. <span data-ttu-id="8814a-136">Une fois l’installation terminée, cliquez sur **inscrire** serveur hello de tooregister dans le coffre hello.</span><span class="sxs-lookup"><span data-stu-id="8814a-136">After installation finishes, click **Register** tooregister hello server in hello vault.</span></span>

    ![Emplacement d’installation](./media/hyper-v-site-walkthrough-source-target/provider2.png)

7. <span data-ttu-id="8814a-138">Une fois l’inscription terminée, les métadonnées à partir du serveur de hello Hyper-V sont récupérées par Azure Site Recovery et hello serveur s’affiche dans **Infrastructure Site Recovery** > **hôtes Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="8814a-138">After registration finishes, metadata from hello Hyper-V server is retrieved by Azure Site Recovery, and hello server is displayed in **Site Recovery Infrastructure** > **Hyper-V Hosts**.</span></span>


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="8814a-139">Configuration d’environnement cible de hello</span><span class="sxs-lookup"><span data-stu-id="8814a-139">Set up hello target environment</span></span>

<span data-ttu-id="8814a-140">Spécifiez le compte de stockage Azure hello pour la réplication et hello réseau Azure toowhich machines virtuelles Azure se connectera après le basculement.</span><span class="sxs-lookup"><span data-stu-id="8814a-140">Specify hello Azure storage account for replication, and hello Azure network toowhich Azure VMs will connect after failover.</span></span>

1. <span data-ttu-id="8814a-141">Cliquez sur **Préparer l’infrastructure** > **Cible**.</span><span class="sxs-lookup"><span data-stu-id="8814a-141">Click **Prepare infrastructure** > **Target**.</span></span>
2. <span data-ttu-id="8814a-142">Sélectionnez l’abonnement de hello et groupe de ressources hello dans lequel vous souhaitez toocreate hello machines virtuelles Azure après le basculement.</span><span class="sxs-lookup"><span data-stu-id="8814a-142">Select hello subscription and hello resource group in which you want toocreate hello Azure VMs after failover.</span></span> <span data-ttu-id="8814a-143">Choisissez le déploiement hello modèle que vous souhaitez toouse dans Azure (classique ou une ressource de gestion) pour les machines virtuelles de hello.</span><span class="sxs-lookup"><span data-stu-id="8814a-143">Choose hello deployment model that you want toouse in Azure (classic or resource management) for hello VMs.</span></span>

3. <span data-ttu-id="8814a-144">Site Recovery vérifie que vous disposez d’un ou de plusieurs réseaux et comptes Azure Storage compatibles.</span><span class="sxs-lookup"><span data-stu-id="8814a-144">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

    - <span data-ttu-id="8814a-145">Si vous n’avez pas un compte de stockage, cliquez sur **+ stockage** toocreate un inline compte basé sur le Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="8814a-145">If you don't have a storage account, click **+Storage** toocreate a Resource Manager-based account inline.</span></span> 
    - <span data-ttu-id="8814a-146">Si vous n’avez pas un réseau Azure, cliquez sur **+ réseau** toocreate un inline réseau basé sur le Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="8814a-146">If you don't have a Azure network, click **+Network** toocreate a Resource Manager-based network inline.</span></span>






## <a name="next-steps"></a><span data-ttu-id="8814a-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8814a-147">Next steps</span></span>

<span data-ttu-id="8814a-148">Accédez trop[étape 9 : configurer une stratégie de réplication](hyper-v-site-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="8814a-148">Go too[Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>
