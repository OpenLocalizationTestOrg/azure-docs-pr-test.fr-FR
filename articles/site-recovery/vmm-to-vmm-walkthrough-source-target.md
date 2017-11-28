---
title: "aaaSet hello source et un cible pour le site secondaire tooa réplication Hyper-V avec Azure Site Recovery | Documents Microsoft"
description: "Décrit comment tooset jusqu'à la source de hello et cibler lorsque des ordinateurs virtuels Hyper-V de réplication de site toosecondary VMM avec Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: fa7809f1-7633-425f-b25d-d10d004e8d0b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 451cb4413ca5c09777a7faf512b1c8ea43e695f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-hello-replication-source-and-target"></a><span data-ttu-id="1c32a-103">Étape 6 : Configurer la cible et source de réplication hello</span><span class="sxs-lookup"><span data-stu-id="1c32a-103">Step 6: Set up hello replication source and target</span></span>


<span data-ttu-id="1c32a-104">Après avoir créé un Services de récupération de coffre pour Hyper-V réplication tooa site VMM secondaire avec [Azure Site Recovery](site-recovery-overview.md), utiliser cette tooset article source de hello et cibler des emplacements de réplication.</span><span class="sxs-lookup"><span data-stu-id="1c32a-104">After creating a Recovery Services vault for Hyper-V replication tooa secondary VMM site with [Azure Site Recovery](site-recovery-overview.md), use this article tooset up hello source and target replication locations.</span></span> 

<span data-ttu-id="1c32a-105">Après avoir lu cet article, validez les commentaires au bas de hello, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="1c32a-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="set-up-hello-source-environment"></a><span data-ttu-id="1c32a-106">Configurer l’environnement source hello</span><span class="sxs-lookup"><span data-stu-id="1c32a-106">Set up hello source environment</span></span>

<span data-ttu-id="1c32a-107">Installer hello fournisseur Azure Site Recovery sur les serveurs VMM et découvrir et inscrire les serveurs dans le coffre hello.</span><span class="sxs-lookup"><span data-stu-id="1c32a-107">Install hello Azure Site Recovery Provider on VMM servers, and discover and register servers in hello vault.</span></span>

1. <span data-ttu-id="1c32a-108">Cliquez sur **Étape 1 : Préparer l’infrastructure** > **Source**.</span><span class="sxs-lookup"><span data-stu-id="1c32a-108">Click **Step 1: Prepare Infrastructure** > **Source**.</span></span>

    ![Configurer la source](./media/vmm-to-vmm-walkthrough-source-target/goals-source.png)
2. <span data-ttu-id="1c32a-110">Dans **Prepare source**, cliquez sur **+ VMM** tooadd un serveur VMM.</span><span class="sxs-lookup"><span data-stu-id="1c32a-110">In **Prepare source**, click **+ VMM** tooadd a VMM server.</span></span>

    ![Configurer la source](./media/vmm-to-vmm-walkthrough-source-target/set-source1.png)
3. <span data-ttu-id="1c32a-112">Dans **ajouter un serveur**, vérifiez que **serveur System Center VMM** s’affiche dans **type de serveur** et le serveur VMM hello satisfont à hello [conditions préalables](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="1c32a-112">In **Add Server**, check that **System Center VMM server** appears in **Server type** and that hello VMM server meets hello [prerequisites](#prerequisites).</span></span>
4. <span data-ttu-id="1c32a-113">Téléchargez le fichier d’installation hello fournisseur Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="1c32a-113">Download hello Azure Site Recovery Provider installation file.</span></span>
5. <span data-ttu-id="1c32a-114">Téléchargez la clé d’inscription de hello.</span><span class="sxs-lookup"><span data-stu-id="1c32a-114">Download hello registration key.</span></span> <span data-ttu-id="1c32a-115">Vous en aurez besoin lorsque vous exécuterez le programme d’installation.</span><span class="sxs-lookup"><span data-stu-id="1c32a-115">You need this when you run setup.</span></span> <span data-ttu-id="1c32a-116">clé de Hello est valide pendant cinq jours après que l’avoir généré.</span><span class="sxs-lookup"><span data-stu-id="1c32a-116">hello key is valid for five days after you generate it.</span></span>

    ![Configurer la source](./media/vmm-to-vmm-walkthrough-source-target/set-source3.png)
6. <span data-ttu-id="1c32a-118">Installez hello fournisseur Azure Site Recovery sur le serveur VMM de hello.</span><span class="sxs-lookup"><span data-stu-id="1c32a-118">Install hello Azure Site Recovery Provider on hello VMM server.</span></span> <span data-ttu-id="1c32a-119">Vous n’avez pas besoin tooexplicitly installer quoi que ce soit sur des serveurs hôtes Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="1c32a-119">You don't need tooexplicitly install anything on Hyper-V host servers.</span></span>


## <a name="install-hello-azure-site-recovery-provider"></a><span data-ttu-id="1c32a-120">Installer hello fournisseur Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="1c32a-120">Install hello Azure Site Recovery Provider</span></span>

1. <span data-ttu-id="1c32a-121">Exécutez le fichier de configuration de fournisseur hello sur chaque serveur VMM.</span><span class="sxs-lookup"><span data-stu-id="1c32a-121">Run hello Provider setup file on each VMM server.</span></span> <span data-ttu-id="1c32a-122">Si VMM est déployé dans un cluster, procédez comme suit de hello hello première fois que vous installez :</span><span class="sxs-lookup"><span data-stu-id="1c32a-122">If VMM is deployed in a cluster, do hello following hello first time you install:</span></span>
    -  <span data-ttu-id="1c32a-123">Installer le fournisseur de hello sur un nœud actif et de fin hello installation tooregister hello serveur VMM dans le coffre hello.</span><span class="sxs-lookup"><span data-stu-id="1c32a-123">Install hello provider on an active node, and finish hello installation tooregister hello VMM server in hello vault.</span></span>
    - <span data-ttu-id="1c32a-124">Ensuite, installez hello fournisseur sur hello autres nœuds.</span><span class="sxs-lookup"><span data-stu-id="1c32a-124">Then, install hello Provider on hello other nodes.</span></span> <span data-ttu-id="1c32a-125">Nœuds de cluster doivent tous exécuter hello même version de hello fournisseur.</span><span class="sxs-lookup"><span data-stu-id="1c32a-125">Cluster nodes should all run hello same version of hello Provider.</span></span>
2. <span data-ttu-id="1c32a-126">Le programme d’installation exécute quelques vérifications et demandes de service d’autorisation toostop hello VMM.</span><span class="sxs-lookup"><span data-stu-id="1c32a-126">Setup runs a few prerequisite checks, and requests permission toostop hello VMM service.</span></span> <span data-ttu-id="1c32a-127">Hello service VMM va redémarrer automatiquement lorsque le programme d’installation se termine.</span><span class="sxs-lookup"><span data-stu-id="1c32a-127">hello VMM service will be restarted automatically when setup finishes.</span></span> <span data-ttu-id="1c32a-128">Si vous installez sur un cluster VMM, vous êtes le rôle de Cluster hello toostop demandées.</span><span class="sxs-lookup"><span data-stu-id="1c32a-128">If you install on a VMM cluster, you're prompted toostop hello Cluster role.</span></span>
3. <span data-ttu-id="1c32a-129">Dans **Microsoft Update**, vous pouvez la choisir toospecify que les mises à jour du fournisseur sont installées conformément à votre stratégie Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="1c32a-129">In **Microsoft Update**, you can opt in toospecify that provider updates are installed in accordance with your Microsoft Update policy.</span></span>
4. <span data-ttu-id="1c32a-130">Dans **Installation**, acceptez ou modifiez l’emplacement d’installation par défaut hello et cliquez sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="1c32a-130">In **Installation**, accept or modify hello default installation location, and click **Install**.</span></span>

    ![Emplacement d’installation](./media/vmm-to-vmm-walkthrough-source-target/provider-location.png)
5. <span data-ttu-id="1c32a-132">Une fois l’installation terminée, cliquez sur **inscrire** serveur hello de tooregister dans le coffre hello.</span><span class="sxs-lookup"><span data-stu-id="1c32a-132">After installation is complete, click **Register** tooregister hello server in hello vault.</span></span>

    ![Emplacement d’installation](./media/vmm-to-vmm-walkthrough-source-target/provider-register.png)
6. <span data-ttu-id="1c32a-134">Dans **nom du coffre**, vérifier nom hello de coffre hello dans le hello serveur sera inscrit.</span><span class="sxs-lookup"><span data-stu-id="1c32a-134">In **Vault name**, verify hello name of hello vault in which hello server will be registered.</span></span> <span data-ttu-id="1c32a-135">Cliquez sur *Suivant*.</span><span class="sxs-lookup"><span data-stu-id="1c32a-135">Click *Next*.</span></span>

    ![Enregistrement du serveur](./media/vmm-to-vmm-walkthrough-source-target/vaultcred.png)
7. <span data-ttu-id="1c32a-137">Dans **connexion Internet**, spécifiez comment hello fournisseur en cours d’exécution sur le serveur VMM de hello connecte tooAzure.</span><span class="sxs-lookup"><span data-stu-id="1c32a-137">In **Internet Connection**, specify how hello provider running on hello VMM server connects tooAzure.</span></span>

    ![Paramètres Internet](./media/vmm-to-vmm-walkthrough-source-target/proxydetails.png)

   - <span data-ttu-id="1c32a-139">Vous pouvez spécifier que le fournisseur hello doit se connecter directement toohello internet, ou via un proxy.</span><span class="sxs-lookup"><span data-stu-id="1c32a-139">You can specify that hello provider should connect directly toohello internet, or via a proxy.</span></span>
   - <span data-ttu-id="1c32a-140">Spécifiez les paramètres de proxy, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="1c32a-140">Specify proxy settings if needed.</span></span>
   - <span data-ttu-id="1c32a-141">Si vous utilisez un proxy, un compte RunAs VMM (DRAProxyAccount) est créé automatiquement à l’aide de hello spécifié les informations d’identification de proxy.</span><span class="sxs-lookup"><span data-stu-id="1c32a-141">If you use a proxy, a VMM RunAs account (DRAProxyAccount) is created automatically using hello specified proxy credentials.</span></span> <span data-ttu-id="1c32a-142">Configurer le serveur de proxy hello afin que ce compte peut s’authentifier avec succès.</span><span class="sxs-lookup"><span data-stu-id="1c32a-142">Configure hello proxy server so that this account can authenticate successfully.</span></span> <span data-ttu-id="1c32a-143">Hello les paramètres de compte d’identification peuvent être modifiés dans la console VMM hello > **paramètres** > **sécurité** > **exécuter en tant que comptes**.</span><span class="sxs-lookup"><span data-stu-id="1c32a-143">hello RunAs account settings can be modified in hello VMM console > **Settings** > **Security** > **Run As Accounts**.</span></span> <span data-ttu-id="1c32a-144">Redémarrez les modifications de tooupdate service hello VMM.</span><span class="sxs-lookup"><span data-stu-id="1c32a-144">Restart hello VMM service tooupdate changes.</span></span>
8. <span data-ttu-id="1c32a-145">Dans **clé d’inscription**, sélectionnez clé hello téléchargés à partir d’Azure Site Recovery et copiée serveur VMM de toohello.</span><span class="sxs-lookup"><span data-stu-id="1c32a-145">In **Registration Key**, select hello key that you downloaded from Azure Site Recovery and copied toohello VMM server.</span></span>
9. <span data-ttu-id="1c32a-146">paramètre de chiffrement Hello est uniquement utilisé lorsque vous répliquez des ordinateurs virtuels Hyper-V dans VMM clouds tooAzure.</span><span class="sxs-lookup"><span data-stu-id="1c32a-146">hello encryption setting is only used when you're replicating Hyper-V VMs in VMM clouds tooAzure.</span></span> <span data-ttu-id="1c32a-147">Si vous effectuez une réplication site secondaire de tooa n’est pas utilisé.</span><span class="sxs-lookup"><span data-stu-id="1c32a-147">If you're replicating tooa secondary site it's not used.</span></span>
10. <span data-ttu-id="1c32a-148">Dans **nom du serveur**, spécifiez un serveur VMM à hello tooidentify nom convivial dans le coffre hello.</span><span class="sxs-lookup"><span data-stu-id="1c32a-148">In **Server name**, specify a friendly name tooidentify hello VMM server in hello vault.</span></span> <span data-ttu-id="1c32a-149">Dans une configuration de cluster spécifier le nom de rôle de cluster VMM hello.</span><span class="sxs-lookup"><span data-stu-id="1c32a-149">In a cluster configuration specify hello VMM cluster role name.</span></span>
11. <span data-ttu-id="1c32a-150">Dans **synchroniser les métadonnées du cloud**, sélectionnez si vous souhaitez toosynchronize métadonnées pour tous les clouds sur le serveur VMM de hello avec le coffre de hello.</span><span class="sxs-lookup"><span data-stu-id="1c32a-150">In **Synchronize cloud metadata**, select whether you want toosynchronize metadata for all clouds on hello VMM server with hello vault.</span></span> <span data-ttu-id="1c32a-151">Cette action ne doit toohappen qu’une seule fois sur chaque serveur.</span><span class="sxs-lookup"><span data-stu-id="1c32a-151">This action only needs toohappen once on each server.</span></span> <span data-ttu-id="1c32a-152">Si vous ne souhaitez pas toosynchronize tous les clouds, vous pouvez laisser ce paramètre désactivé et synchroniser chaque cloud individuellement dans les propriétés du cloud hello dans la console VMM hello.</span><span class="sxs-lookup"><span data-stu-id="1c32a-152">If you don't want toosynchronize all clouds, you can leave this setting unchecked, and synchronize each cloud individually in hello cloud properties in hello VMM console.</span></span>
12. <span data-ttu-id="1c32a-153">Cliquez sur **suivant** processus de hello toocomplete.</span><span class="sxs-lookup"><span data-stu-id="1c32a-153">Click **Next** toocomplete hello process.</span></span> <span data-ttu-id="1c32a-154">Après l’inscription, les métadonnées d’un serveur hello VMM sont récupérées par Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="1c32a-154">After registration, metadata from hello VMM server is retrieved by Azure Site Recovery.</span></span> <span data-ttu-id="1c32a-155">serveur de Hello est affiché sur hello **serveurs VMM** onglet hello **serveurs** page dans le coffre hello.</span><span class="sxs-lookup"><span data-stu-id="1c32a-155">hello server is displayed on hello **VMM Servers** tab on hello **Servers** page in hello vault.</span></span>

    ![Serveur](./media/vmm-to-vmm-walkthrough-source-target/provider13.png)
13. <span data-ttu-id="1c32a-157">Une fois le serveur de hello est disponible dans la console de récupération de Site hello dans **Source** > **Prepare source** sélectionnez hello VMM server et nuage hello sélectionnez quels Bonjour Hyper-V se trouve.</span><span class="sxs-lookup"><span data-stu-id="1c32a-157">After hello server is available in hello Site Recovery console, in **Source** > **Prepare source** select hello VMM server, and select hello cloud in which hello Hyper-V host is located.</span></span> <span data-ttu-id="1c32a-158">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="1c32a-158">Then click **OK**.</span></span>

<span data-ttu-id="1c32a-159">Vous pouvez également installer le fournisseur de hello à partir de la ligne de commande hello :</span><span class="sxs-lookup"><span data-stu-id="1c32a-159">You can also install hello provider from hello command line:</span></span>

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="1c32a-160">Configuration d’environnement cible de hello</span><span class="sxs-lookup"><span data-stu-id="1c32a-160">Set up hello target environment</span></span>

<span data-ttu-id="1c32a-161">Sélectionner le cloud et le serveur VMM de hello cible :</span><span class="sxs-lookup"><span data-stu-id="1c32a-161">Select hello target VMM server and cloud:</span></span>

1. <span data-ttu-id="1c32a-162">Cliquez sur **Prepare infrastructure** > **cible**et sélectionnez hello cible VMM serveur toouse.</span><span class="sxs-lookup"><span data-stu-id="1c32a-162">Click **Prepare infrastructure** > **Target**, and select hello target VMM server you want toouse.</span></span>
2. <span data-ttu-id="1c32a-163">Les clouds sur le serveur hello qui sont synchronisés avec la récupération de Site seront affiche.</span><span class="sxs-lookup"><span data-stu-id="1c32a-163">Clouds on hello server that are synchronized with Site Recovery will be displayed.</span></span> <span data-ttu-id="1c32a-164">Sélectionnez le cloud cible de hello.</span><span class="sxs-lookup"><span data-stu-id="1c32a-164">Select hello target cloud.</span></span>

   ![Cible](./media/vmm-to-vmm-walkthrough-source-target/target-vmm.png)



## <a name="next-steps"></a><span data-ttu-id="1c32a-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1c32a-166">Next steps</span></span>

<span data-ttu-id="1c32a-167">Accédez trop[étape 7 : configurer le mappage réseau](vmm-to-vmm-walkthrough-network-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="1c32a-167">Go too[Step 7: Configure network mapping](vmm-to-vmm-walkthrough-network-mapping.md).</span></span>
