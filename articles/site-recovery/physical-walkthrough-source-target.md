---
title: "aaaSet hello source et un cible pour tooAzure de réplication de serveur physique avec Azure Site Recovery | Documents Microsoft"
description: "Résume les tooset d’étapes hello les paramètres source et cible pour la réplication de stockage tooAzure de serveurs physiques avec hello service Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 2e3d03bc-4e53-4590-8a01-f702d3cc9500
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: e75ef23174d77509bf54380eba8f251a7337a45f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-hello-source-and-target-for-physical-server-replication-tooazure"></a><span data-ttu-id="75c6f-103">Étape 7 : Configurer la source de hello et cible pour tooAzure de réplication de serveur physique</span><span class="sxs-lookup"><span data-stu-id="75c6f-103">Step 7: Set up hello source and target for physical server replication tooAzure</span></span>

<span data-ttu-id="75c6f-104">Cet article décrit comment tooconfigure les paramètres de source et cible lors de la réplication locale tooAzure des serveurs physiques, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="75c6f-104">This article describes how tooconfigure source and target settings when replicating on-premises physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="75c6f-105">Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="75c6f-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="75c6f-106">Configurer l’environnement source hello</span><span class="sxs-lookup"><span data-stu-id="75c6f-106">Set up hello source environment</span></span>

<span data-ttu-id="75c6f-107">Configurer le serveur de configuration hello, enregistrez-le dans le coffre hello et découvrir les ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="75c6f-107">Set up hello configuration server, register it in hello vault, and discover machines.</span></span>

1. <span data-ttu-id="75c6f-108">Cliquez sur **Site Recovery** > **Étape 1 : Préparer l’infrastructure** > **Source**.</span><span class="sxs-lookup"><span data-stu-id="75c6f-108">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="75c6f-109">Si vous n’avez pas de serveur de configuration, cliquez sur **+Serveur de configuration**.</span><span class="sxs-lookup"><span data-stu-id="75c6f-109">If you don’t have a configuration server, click **+Configuration server**.</span></span>
3. <span data-ttu-id="75c6f-110">Dans **Ajouter un serveur**, vérifiez que **Serveur de configuration** s’affiche dans **Type de serveur**.</span><span class="sxs-lookup"><span data-stu-id="75c6f-110">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="75c6f-111">Télécharger le fichier d’installation le programme d’installation de Site Recovery unifiée hello.</span><span class="sxs-lookup"><span data-stu-id="75c6f-111">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="75c6f-112">Télécharger la clé d’inscription du coffre hello.</span><span class="sxs-lookup"><span data-stu-id="75c6f-112">Download hello vault registration key.</span></span> <span data-ttu-id="75c6f-113">Vous en aurez besoin lors de l’exécution du programme d’installation unifiée.</span><span class="sxs-lookup"><span data-stu-id="75c6f-113">You need this when you run Unified Setup.</span></span> <span data-ttu-id="75c6f-114">clé de Hello est valide pendant cinq jours après que l’avoir généré.</span><span class="sxs-lookup"><span data-stu-id="75c6f-114">hello key is valid for five days after you generate it.</span></span>

   ![Configurer la source](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a><span data-ttu-id="75c6f-116">Inscrire le serveur de configuration hello dans le coffre de hello</span><span class="sxs-lookup"><span data-stu-id="75c6f-116">Register hello configuration server in hello vault</span></span>

<span data-ttu-id="75c6f-117">Suit hello avant de démarrer, puis exécuter le programme d’installation unifiée serveur de configuration tooinstall hello, serveur de processus hello et serveur cible maître de hello.</span><span class="sxs-lookup"><span data-stu-id="75c6f-117">Do hello following before you start, then run Unified Setup tooinstall hello configuration server, hello process server, and hello master target server.</span></span> <span data-ttu-id="75c6f-118">Hello vidéo décrit comment configurer des composants hello pour la réplication tooAzure VMware VM.</span><span class="sxs-lookup"><span data-stu-id="75c6f-118">hello video describes setting up hello components for VMware VM tooAzure replication.</span></span> <span data-ttu-id="75c6f-119">Toutefois, hello même processus n’est valide pour la réplication tooAzure serveur physique.</span><span class="sxs-lookup"><span data-stu-id="75c6f-119">However, hello same process is valid for physical server tooAzure replication.</span></span>

- <span data-ttu-id="75c6f-120">Sur le serveur de configuration hello machine virtuelle, assurez-vous que l’horloge système hello est synchronisée avec un [serveur de temps](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span><span class="sxs-lookup"><span data-stu-id="75c6f-120">On hello configuration server VM, make sure that hello system clock is synchronized with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="75c6f-121">Elles doivent correspondre.</span><span class="sxs-lookup"><span data-stu-id="75c6f-121">It should match.</span></span> <span data-ttu-id="75c6f-122">S’il y a 15 minutes d’avance ou de retard, le programme d’installation peut échouer.</span><span class="sxs-lookup"><span data-stu-id="75c6f-122">If it's 15 minutes in front or behind, setup might fail.</span></span>
- <span data-ttu-id="75c6f-123">Exécutez le programme d’installation en tant qu’administrateur Local sur l’ordinateur de serveur de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="75c6f-123">Run setup as a Local Administrator on hello configuration server machine.</span></span>
- <span data-ttu-id="75c6f-124">Vérifiez que TLS 1.0 est activé sur la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="75c6f-124">Make sure TLS 1.0 is enabled on hello VM.</span></span>


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="75c6f-125">serveur de configuration Hello peut également être installé [à partir de la ligne de commande hello](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="75c6f-125">hello configuration server can also be installed [from hello command line](http://aka.ms/installconfigsrv).</span></span>




## <a name="set-up-hello-target-environment"></a><span data-ttu-id="75c6f-126">Configuration d’environnement cible de hello</span><span class="sxs-lookup"><span data-stu-id="75c6f-126">Set up hello target environment</span></span>

<span data-ttu-id="75c6f-127">Avant de configurer l’environnement cible de hello, assurez-vous que vous avez un compte de stockage Azure et le réseau virtuel configuré.</span><span class="sxs-lookup"><span data-stu-id="75c6f-127">Before you set up hello target environment, make sure you have an Azure storage account and virtual network set up.</span></span>

1. <span data-ttu-id="75c6f-128">Cliquez sur **Prepare infrastructure** > **cible**, et sélectionnez hello abonnement Azure que vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="75c6f-128">Click **Prepare infrastructure** > **Target**, and select hello Azure subscription you want toouse.</span></span>
2. <span data-ttu-id="75c6f-129">Spécifiez si votre modèle de déploiement cible est basé sur Resource Manager ou est de type classique.</span><span class="sxs-lookup"><span data-stu-id="75c6f-129">Specify whether your target deployment model is Resource Manager-based, or classic.</span></span>
3. <span data-ttu-id="75c6f-130">Site Recovery vérifie que vous disposez d’un ou de plusieurs réseaux et comptes Azure Storage compatibles.</span><span class="sxs-lookup"><span data-stu-id="75c6f-130">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![Cible](./media/physical-walkthrough-source-target/gs-target.png)

4. <span data-ttu-id="75c6f-132">Si vous n’avez pas créé un compte de stockage ou un réseau, cliquez sur **+ compte de stockage** ou **+ réseau**, toocreate un gestionnaire de ressources du réseau ou le compte en ligne.</span><span class="sxs-lookup"><span data-stu-id="75c6f-132">If you haven't created a storage account or network, click **+Storage account** or **+Network**, toocreate a Resource Manager account or network inline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="75c6f-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="75c6f-133">Next steps</span></span>

<span data-ttu-id="75c6f-134">Accédez trop[étape 8 : définir une stratégie de réplication](physical-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="75c6f-134">Go too[Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>
