---
title: "Configurer la source et la cible pour la réplication de Hyper-V vers Azure (sans System Center VMM) avec Azure Site Recovery | Microsoft Docs"
description: "Résume les étapes à suivre pour configurer les paramètres de source et de cible pour la réplication de machines virtuelles Hyper-V vers le stockage Azure avec Azure Site Recovery."
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
ms.openlocfilehash: b38eb3a011d46f2239891ea1d1bcac2a4059a866
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="step-8-set-up-the-source-and-target-for-hyper-v-replication-to-azure"></a><span data-ttu-id="85e31-103">Étape 8 : configurer la source et la cible pour la réplication de Hyper-V vers Azure</span><span class="sxs-lookup"><span data-stu-id="85e31-103">Step 8: Set up the source and target for Hyper-V replication to Azure</span></span>

<span data-ttu-id="85e31-104">Cet article explique comment configurer les paramètres de source et de cible pour la réplication de machines virtuelles Hyper-V (sans System Center VMM) vers Azure à l’aide du service [Azure Site Recovery](site-recovery-overview.md) dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="85e31-104">This article describes how to configure source and target settings when replicating on-premises Hyper-V virtual machines (without System Center VMM) to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="85e31-105">Publiez des commentaires et des questions au bas de cet article, ou sur le [Forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="85e31-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-the-source-environment"></a><span data-ttu-id="85e31-106">Configurer l’environnement source</span><span class="sxs-lookup"><span data-stu-id="85e31-106">Set up the source environment</span></span>

<span data-ttu-id="85e31-107">Configurez le site Hyper-V, installez le fournisseur Azure Site Recovery et l’agent Azure Recovery Services sur les hôtes Hyper-V et inscrivez le site dans le coffre.</span><span class="sxs-lookup"><span data-stu-id="85e31-107">Set up the Hyper-V site, install the Azure Site Recovery Provider and the Azure Recovery Services agent on Hyper-V hosts, and register the site in the vault.</span></span>

1. <span data-ttu-id="85e31-108">Dans **Préparer l’infrastructure**, cliquez sur **Source**.</span><span class="sxs-lookup"><span data-stu-id="85e31-108">In **Prepare Infrastructure**, click **Source**.</span></span> <span data-ttu-id="85e31-109">Pour ajouter un nouveau site Hyper-V en tant que conteneur pour vos hôtes ou clusters Hyper-V, cliquez sur **+Site Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="85e31-109">To add a new Hyper-V site as a container for your Hyper-V hosts or clusters, click **+Hyper-V Site**.</span></span>

    ![Configurer la source](./media/hyper-v-site-walkthrough-source-target/set-source1.png)
2. <span data-ttu-id="85e31-111">Dans **Créer un site Hyper-V**, spécifiez un nom pour le site.</span><span class="sxs-lookup"><span data-stu-id="85e31-111">In **Create Hyper-V site**, specify a name for the site.</span></span> <span data-ttu-id="85e31-112">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="85e31-112">Then click **OK**.</span></span> <span data-ttu-id="85e31-113">Sélectionnez le site que vous avez créé, puis cliquez sur **+Serveur Hyper-V** pour ajouter un serveur au site.</span><span class="sxs-lookup"><span data-stu-id="85e31-113">Now, select the site you created, and click **+Hyper-V Server** to add a server to the site.</span></span>

    ![Configurer la source](./media/hyper-v-site-walkthrough-source-target/set-source2.png)

3. <span data-ttu-id="85e31-115">Dans **Ajouter un serveur** > **Type de serveur**, vérifiez que **Serveur Hyper-V** est affiché.</span><span class="sxs-lookup"><span data-stu-id="85e31-115">In **Add Server** > **Server type**, check that **Hyper-V server** is displayed.</span></span>

    - <span data-ttu-id="85e31-116">Assurez-vous que le serveur Hyper-V à ajouter est conforme à la [configuration requise](#on-premises-prerequisites) et est en mesure d’accéder aux URL spécifiées.</span><span class="sxs-lookup"><span data-stu-id="85e31-116">Make sure that the Hyper-V server you want to add complies with the [prerequisites](#on-premises-prerequisites), and is able to access the specified URLs.</span></span>
    - <span data-ttu-id="85e31-117">Téléchargez le fichier d’installation du fournisseur Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="85e31-117">Download the Azure Site Recovery Provider installation file.</span></span> <span data-ttu-id="85e31-118">Vous allez exécuter ce fichier pour installer le fournisseur et l’agent Recovery Services sur chaque hôte Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="85e31-118">You run this file to install the Provider and the Recovery Services agent on each Hyper-V host.</span></span>

    ![Configurer la source](./media/hyper-v-site-walkthrough-source-target/set-source3.png)


## <a name="install-the-provider-and-agent"></a><span data-ttu-id="85e31-120">Installer le fournisseur et l’agent</span><span class="sxs-lookup"><span data-stu-id="85e31-120">Install the Provider and agent</span></span>

1. <span data-ttu-id="85e31-121">Exécutez le fichier d’installation du fournisseur sur chaque hôte que vous avez ajouté au site Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="85e31-121">Run the Provider setup file on each host you added to the Hyper-V site.</span></span> <span data-ttu-id="85e31-122">Si vous effectuez l’installation sur un cluster Hyper-V, exécutez le programme d’installation sur chaque nœud du cluster.</span><span class="sxs-lookup"><span data-stu-id="85e31-122">If you're installing on a Hyper-V cluster, run setup on each cluster node.</span></span> <span data-ttu-id="85e31-123">L’installation et l’inscription de chaque nœud de cluster Hyper-V permettent de s’assurer que les machines virtuelles sont protégées, même si elles migrent entre les nœuds.</span><span class="sxs-lookup"><span data-stu-id="85e31-123">Installing and registering each Hyper-V cluster node ensures that VMs are protected, even if they migrate across nodes.</span></span>
2. <span data-ttu-id="85e31-124">Dans **Microsoft Update**, vous pouvez choisir des mises à jour, pour que celles du fournisseur soient installées conformément à votre stratégie Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="85e31-124">In **Microsoft Update**, you can opt in for updates so that Provider updates are installed in accordance with your Microsoft Update policy.</span></span>
3. <span data-ttu-id="85e31-125">Dans le champ **Installation**, acceptez ou modifiez l’emplacement d’installation du fournisseur par défaut et cliquez sur **Installer**.</span><span class="sxs-lookup"><span data-stu-id="85e31-125">In **Installation**, accept or modify the default Provider installation location and click **Install**.</span></span>
4. <span data-ttu-id="85e31-126">Dans **Paramètres du coffre**, cliquez sur **Parcourir** pour sélectionner le fichier de clé du coffre que vous avez téléchargé.</span><span class="sxs-lookup"><span data-stu-id="85e31-126">In **Vault Settings**, click **Browse** to select the vault key file that you downloaded.</span></span> <span data-ttu-id="85e31-127">Spécifiez l’abonnement Azure Site Recovery, le nom du coffre et le site Hyper-V auquel appartient le serveur Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="85e31-127">Specify the Azure Site Recovery subscription, the vault name, and the Hyper-V site to which the Hyper-V server belongs.</span></span>

    ![Enregistrement du serveur](./media/hyper-v-site-walkthrough-source-target/provider3.png)

5. <span data-ttu-id="85e31-129">Dans **Paramètres du proxy**, indiquez de quelle manière le fournisseur qui s’exécute sur les hôtes Hyper-V doit se connecter à Azure Site Recovery par le biais d’Internet.</span><span class="sxs-lookup"><span data-stu-id="85e31-129">In **Proxy Settings**, specify how the Provider running on Hyper-V hosts connects to Azure Site Recovery over the internet.</span></span>

    * <span data-ttu-id="85e31-130">Si vous voulez que le fournisseur se connecte directement, sélectionnez **Se connecter directement à Azure Site Recovery sans serveur proxy**.</span><span class="sxs-lookup"><span data-stu-id="85e31-130">If you want the Provider to connect directly select **Connect directly to Azure Site Recovery without a proxy**.</span></span>
    * <span data-ttu-id="85e31-131">Si votre proxy nécessite une authentification ou si vous voulez utiliser un proxy personnalisé pour la connexion du fournisseur, sélectionnez **Se connecter directement à Azure Site Recovery avec un serveur proxy**.</span><span class="sxs-lookup"><span data-stu-id="85e31-131">If your existing proxy requires authentication, or you want to use a custom proxy for the Provider connection, select **Connect to Azure Site Recovery using a proxy server**.</span></span>
    * <span data-ttu-id="85e31-132">Si vous utilisez un proxy :</span><span class="sxs-lookup"><span data-stu-id="85e31-132">If you use a proxy:</span></span>
        - <span data-ttu-id="85e31-133">Spécifiez l’adresse, le port et les informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="85e31-133">Specify the address, port, and credentials</span></span>
        - <span data-ttu-id="85e31-134">Vérifiez que les URL décrites dans la [configuration requise](#prerequisites) sont autorisées via le proxy.</span><span class="sxs-lookup"><span data-stu-id="85e31-134">Make sure the URLs described in the [prerequisites](#prerequisites) are allowed through the proxy.</span></span>

    ![Internet](./media/hyper-v-site-walkthrough-source-target/provider7.png)

6. <span data-ttu-id="85e31-136">Une fois l’installation terminée, cliquez sur **Inscrire** pour inscrire le serveur dans le coffre.</span><span class="sxs-lookup"><span data-stu-id="85e31-136">After installation finishes, click **Register** to register the server in the vault.</span></span>

    ![Emplacement d’installation](./media/hyper-v-site-walkthrough-source-target/provider2.png)

7. <span data-ttu-id="85e31-138">Une fois l’inscription terminée, les métadonnées du serveur Hyper-V sont récupérées par Azure Site Recovery et le serveur s’affiche dans **Infrastructure Site Recovery** > **Hôtes Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="85e31-138">After registration finishes, metadata from the Hyper-V server is retrieved by Azure Site Recovery, and the server is displayed in **Site Recovery Infrastructure** > **Hyper-V Hosts**.</span></span>


## <a name="set-up-the-target-environment"></a><span data-ttu-id="85e31-139">Configurer l’environnement cible</span><span class="sxs-lookup"><span data-stu-id="85e31-139">Set up the target environment</span></span>

<span data-ttu-id="85e31-140">Spécifiez le compte Azure Storage à utiliser pour la réplication, ainsi que le réseau Azure auquel les machines virtuelles Azure se connecteront après le basculement.</span><span class="sxs-lookup"><span data-stu-id="85e31-140">Specify the Azure storage account for replication, and the Azure network to which Azure VMs will connect after failover.</span></span>

1. <span data-ttu-id="85e31-141">Cliquez sur **Préparer l’infrastructure** > **Cible**.</span><span class="sxs-lookup"><span data-stu-id="85e31-141">Click **Prepare infrastructure** > **Target**.</span></span>
2. <span data-ttu-id="85e31-142">Sélectionnez l’abonnement et le groupe de ressources dans lesquels vous voulez créer les machines virtuelles Azure après le basculement.</span><span class="sxs-lookup"><span data-stu-id="85e31-142">Select the subscription and the resource group in which you want to create the Azure VMs after failover.</span></span> <span data-ttu-id="85e31-143">Choisissez le modèle de déploiement que vous souhaitez utiliser dans Azure (classique ou gestion des ressources) pour les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="85e31-143">Choose the deployment model that you want to use in Azure (classic or resource management) for the VMs.</span></span>

3. <span data-ttu-id="85e31-144">Site Recovery vérifie que vous disposez d’un ou de plusieurs réseaux et comptes Azure Storage compatibles.</span><span class="sxs-lookup"><span data-stu-id="85e31-144">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

    - <span data-ttu-id="85e31-145">Si vous n’avez pas de compte de stockage, cliquez sur **+Stockage** pour créer un compte basé sur Resource Manager en ligne.</span><span class="sxs-lookup"><span data-stu-id="85e31-145">If you don't have a storage account, click **+Storage** to create a Resource Manager-based account inline.</span></span> 
    - <span data-ttu-id="85e31-146">Si vous n’avez pas de réseau Azure, cliquez sur **+Réseau** pour créer un compte basé sur Resource Manager en ligne.</span><span class="sxs-lookup"><span data-stu-id="85e31-146">If you don't have a Azure network, click **+Network** to create a Resource Manager-based network inline.</span></span>






## <a name="next-steps"></a><span data-ttu-id="85e31-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="85e31-147">Next steps</span></span>

<span data-ttu-id="85e31-148">Aller à [Étape 9 : configurer une stratégie de réplication](hyper-v-site-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="85e31-148">Go to [Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>
