---
title: "aaaSet hello source et un cible pour tooAzure de réplication VMware avec Azure Site Recovery | Documents Microsoft"
description: "Résume les tooset d’étapes hello les paramètres source et cible pour la réplication de stockage de tooAzure les ordinateurs virtuels VMware avec Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99e422e-daf7-4fa8-af3c-af2340340136
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: ef33a44bc5da17afb0442be63f576925f5b9a8b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-vmware-replication-tooazure"></a><span data-ttu-id="72335-103">Étape 8 : Configurer la source de hello et cible pour VMware réplication tooAzure</span><span class="sxs-lookup"><span data-stu-id="72335-103">Step 8: Set up hello source and target for VMware replication tooAzure</span></span>

<span data-ttu-id="72335-104">Cet article décrit comment tooconfigure les paramètres de source et cible lors de la réplication locale tooAzure d’ordinateurs virtuels VMware, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="72335-104">This article describes how tooconfigure source and target settings when replicating on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="72335-105">Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="72335-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="72335-106">Configurer l’environnement source hello</span><span class="sxs-lookup"><span data-stu-id="72335-106">Set up hello source environment</span></span>

<span data-ttu-id="72335-107">Configurer le serveur de configuration hello, enregistrez-le dans le coffre hello et découvrir des ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="72335-107">Set up hello configuration server, register it in hello vault, and discover VMs.</span></span>

1. <span data-ttu-id="72335-108">Cliquez sur **Site Recovery** > **Étape 1 : Préparer l’infrastructure** > **Source**.</span><span class="sxs-lookup"><span data-stu-id="72335-108">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="72335-109">Si vous n’avez pas de serveur de configuration, cliquez sur **+Serveur de configuration**.</span><span class="sxs-lookup"><span data-stu-id="72335-109">If you don’t have a configuration server, click **+Configuration server**.</span></span>
3. <span data-ttu-id="72335-110">Dans **Ajouter un serveur**, vérifiez que **Serveur de configuration** s’affiche dans **Type de serveur**.</span><span class="sxs-lookup"><span data-stu-id="72335-110">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="72335-111">Télécharger le fichier d’installation le programme d’installation de Site Recovery unifiée hello.</span><span class="sxs-lookup"><span data-stu-id="72335-111">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="72335-112">Télécharger la clé d’inscription du coffre hello.</span><span class="sxs-lookup"><span data-stu-id="72335-112">Download hello vault registration key.</span></span> <span data-ttu-id="72335-113">Vous en aurez besoin lors de l’exécution du programme d’installation unifiée.</span><span class="sxs-lookup"><span data-stu-id="72335-113">You need this when you run Unified Setup.</span></span> <span data-ttu-id="72335-114">clé de Hello est valide pendant cinq jours après que l’avoir généré.</span><span class="sxs-lookup"><span data-stu-id="72335-114">hello key is valid for five days after you generate it.</span></span>

   ![Configurer la source](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a><span data-ttu-id="72335-116">Inscrire le serveur de configuration hello dans le coffre de hello</span><span class="sxs-lookup"><span data-stu-id="72335-116">Register hello configuration server in hello vault</span></span>

<span data-ttu-id="72335-117">Suit hello avant de démarrer, puis exécuter le programme d’installation unifiée serveur de configuration tooinstall hello, serveur de processus hello et serveur cible maître de hello.</span><span class="sxs-lookup"><span data-stu-id="72335-117">Do hello following before you start, then run Unified Setup tooinstall hello configuration server, hello process server, and hello master target server.</span></span>
    - <span data-ttu-id="72335-118">Visionnez une courte vidéo de présentation :</span><span class="sxs-lookup"><span data-stu-id="72335-118">Get a quick video overview</span></span>

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - <span data-ttu-id="72335-119">Sur le serveur de configuration hello machine virtuelle, assurez-vous que l’horloge système hello est synchronisée avec un [serveur de temps](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span><span class="sxs-lookup"><span data-stu-id="72335-119">On hello configuration server VM, make sure that hello system clock is synchronized with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="72335-120">Elles doivent correspondre.</span><span class="sxs-lookup"><span data-stu-id="72335-120">It should match.</span></span> <span data-ttu-id="72335-121">S’il y a 15 minutes d’avance ou de retard, le programme d’installation peut échouer.</span><span class="sxs-lookup"><span data-stu-id="72335-121">If it's 15 minutes in front or behind, setup might fail.</span></span>
    - <span data-ttu-id="72335-122">Exécutez le programme d’installation en tant qu’administrateur Local sur le serveur de configuration hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="72335-122">Run setup as a Local Administrator on hello configuration server VM.</span></span>
    - <span data-ttu-id="72335-123">Vérifiez que TLS 1.0 est activé sur la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="72335-123">Make sure TLS 1.0 is enabled on hello VM.</span></span>


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="72335-124">serveur de configuration Hello peut également être installé [à partir de la ligne de commande hello](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="72335-124">hello configuration server can also be installed [from hello command line](http://aka.ms/installconfigsrv).</span></span>



## <a name="connect-toovmware-servers"></a><span data-ttu-id="72335-125">Connecter les serveurs tooVMware</span><span class="sxs-lookup"><span data-stu-id="72335-125">Connect tooVMware servers</span></span>

<span data-ttu-id="72335-126">tooallow Azure Site Recovery toodiscover machines virtuelles en cours d’exécution dans votre environnement local, vous devez tooconnect votre serveur VMware vCenter ou les ordinateurs hôtes ESXi vSphere avec Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="72335-126">tooallow Azure Site Recovery toodiscover virtual machines running in your on-premises environment, you need tooconnect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span></span> <span data-ttu-id="72335-127">Notez les points suivants de hello avant de commencer :</span><span class="sxs-lookup"><span data-stu-id="72335-127">Note hello following before you start:</span></span>

- <span data-ttu-id="72335-128">Si vous ajoutez le serveur vCenter hello ou vSphere hôtes tooSite récupération avec un compte sans privilèges d’administrateur sur le serveur de hello, compte de hello a besoin de ces privilèges activés :</span><span class="sxs-lookup"><span data-stu-id="72335-128">If you add hello vCenter server or vSphere hosts tooSite Recovery with an account without administrator privileges on hello server, hello account needs these privileges enabled:</span></span>
    - <span data-ttu-id="72335-129">Centre de données, magasin de données, dossier, hôte, réseau, ressource, machine virtuelle, vSphere Distributed Switch.</span><span class="sxs-lookup"><span data-stu-id="72335-129">Datacenter, Datastore, Folder, Host, Network, Resource, Virtual machine, vSphere Distributed Switch.</span></span>
    - <span data-ttu-id="72335-130">le serveur vCenter Hello a besoin d’autorisations de vues de stockage.</span><span class="sxs-lookup"><span data-stu-id="72335-130">hello vCenter server needs Storage views permissions.</span></span>
- <span data-ttu-id="72335-131">Lorsque vous ajoutez des serveurs de VMware tooSite récupération, il peut prendre 15 minutes ou plus pour les tooappear dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="72335-131">When you add VMware servers tooSite Recovery, it can take 15 minutes or longer for them tooappear in hello portal.</span></span>

### <a name="add-hello-account-for-automatic-discovery"></a><span data-ttu-id="72335-132">Ajoutez le compte hello pour la découverte automatique</span><span class="sxs-lookup"><span data-stu-id="72335-132">Add hello account for automatic discovery</span></span>

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="set-up-a-connection"></a><span data-ttu-id="72335-133">Configurer une connexion</span><span class="sxs-lookup"><span data-stu-id="72335-133">Set up a connection</span></span>

<span data-ttu-id="72335-134">Se connecter tooservers comme suit :</span><span class="sxs-lookup"><span data-stu-id="72335-134">Connect tooservers as follows:</span></span>

1. <span data-ttu-id="72335-135">Sélectionnez **+ vCenter** toostart connecter un serveur VMware vCenter ou un hôte VMware vSphere ESXi.</span><span class="sxs-lookup"><span data-stu-id="72335-135">Select **+vCenter** toostart connecting a VMware vCenter server or a VMware vSphere ESXi host.</span></span>
2. <span data-ttu-id="72335-136">Dans **ajouter vCenter**, spécifiez un nom convivial pour le serveur hôte ou vCenter du vSphere hello, puis spécifiez l’adresse IP de hello ou nom de domaine complet du serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="72335-136">In **Add vCenter**, specify a friendly name for hello vSphere host or vCenter server, and then specify hello IP address or FQDN of hello server.</span></span>
3. <span data-ttu-id="72335-137">Conservez les port hello 443, sauf si vos serveurs VMware sont toolisten configurée pour les demandes sur un port différent.</span><span class="sxs-lookup"><span data-stu-id="72335-137">Leave hello port as 443 unless your VMware servers are configured toolisten for requests on a different port.</span></span> <span data-ttu-id="72335-138">Sélectionnez compte hello tooconnect toohello VMware vCenter ou vSphere ESXi Server.</span><span class="sxs-lookup"><span data-stu-id="72335-138">Select hello account that is tooconnect toohello VMware vCenter or vSphere ESXi server.</span></span> <span data-ttu-id="72335-139">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="72335-139">Click **OK**.</span></span>
4. <span data-ttu-id="72335-140">Récupération de site connecte tooVMware serveurs à l’aide de hello spécifié de paramètres et détecte les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="72335-140">Site Recovery connects tooVMware servers using hello specified settings, and discovers VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="72335-141">Si vous ajoutez un serveur ou un ordinateur hôte avec un compte qui ne dispose pas des privilèges d’administrateur sur le serveur vCenter ou un hôte de hello, assurez-vous que le compte de hello a ces privilèges activés : centre de données, magasin de données, dossier, hôte, réseau, ressources, l’ordinateur virtuel, et vSphere Distributed Switch.</span><span class="sxs-lookup"><span data-stu-id="72335-141">If you're adding a server or host with an account that doesn't have administrator privileges on hello vCenter or host server, make sure that hello account has these privileges enabled: Datacenter, Datastore, Folder, Host, Network, Resource, Virtual machine, and vSphere Distributed Switch.</span></span> <span data-ttu-id="72335-142">En outre, hello VMware vCenter server a besoin d’affichages de stockage hello privilège activé.</span><span class="sxs-lookup"><span data-stu-id="72335-142">In addition, hello VMware vCenter server needs hello Storage Views privilege enabled.</span></span>


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="72335-143">Configuration d’environnement cible de hello</span><span class="sxs-lookup"><span data-stu-id="72335-143">Set up hello target environment</span></span>

<span data-ttu-id="72335-144">Avant de configurer l’environnement cible de hello, assurez-vous que vous avez un compte de stockage Azure et le réseau virtuel configuré.</span><span class="sxs-lookup"><span data-stu-id="72335-144">Before you set up hello target environment, make sure you have an Azure storage account and virtual network set up.</span></span>

1. <span data-ttu-id="72335-145">Cliquez sur **Prepare infrastructure** > **cible**, et sélectionnez hello abonnement Azure que vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="72335-145">Click **Prepare infrastructure** > **Target**, and select hello Azure subscription you want toouse.</span></span>
2. <span data-ttu-id="72335-146">Spécifiez si votre modèle de déploiement cible est basé sur Resource Manager ou est de type classique.</span><span class="sxs-lookup"><span data-stu-id="72335-146">Specify whether your target deployment model is Resource Manager-based, or classic.</span></span>
3. <span data-ttu-id="72335-147">Site Recovery vérifie que vous disposez d’un ou de plusieurs réseaux et comptes Azure Storage compatibles.</span><span class="sxs-lookup"><span data-stu-id="72335-147">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![Cible](./media/vmware-walkthrough-source-target/gs-target.png)
4. <span data-ttu-id="72335-149">Si vous n’avez pas créé un compte de stockage ou un réseau, cliquez sur **+ compte de stockage** ou **+ réseau**, toocreate un gestionnaire de ressources du réseau ou le compte en ligne.</span><span class="sxs-lookup"><span data-stu-id="72335-149">If you haven't created a storage account or network, click **+Storage account** or **+Network**, toocreate a Resource Manager account or network inline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72335-150">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="72335-150">Next steps</span></span>

<span data-ttu-id="72335-151">Accédez trop[étape 9 : configurer une stratégie de réplication](vmware-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="72335-151">Go too[Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>
