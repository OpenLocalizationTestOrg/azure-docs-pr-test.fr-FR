---
title: "Configurer la source et la cible pour la réplication de serveurs physiques vers Azure à l’aide d’Azure Site Recovery | Microsoft Docs"
description: "Résume les étapes à suivre pour configurer les paramètres sources et cibles liés à la réplication de serveurs physiques vers un stockage Azure à l’aide du service Azure Site Recovery"
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
ms.openlocfilehash: e89bbf5a2c1d71852e49da43d3106a05ebfc28a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="step-7-set-up-the-source-and-target-for-physical-server-replication-to-azure"></a><span data-ttu-id="09324-103">Étape 7 : Configurer la source et la cible pour la réplication de serveurs physiques vers Azure</span><span class="sxs-lookup"><span data-stu-id="09324-103">Step 7: Set up the source and target for physical server replication to Azure</span></span>

<span data-ttu-id="09324-104">Cet article explique comment configurer des paramètres sources et cibles lors de la réplication de serveurs physiques locaux vers Azure à l’aide du service [Azure Site Recovery](site-recovery-overview.md) dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="09324-104">This article describes how to configure source and target settings when replicating on-premises physical servers to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="09324-105">Publiez des commentaires et des questions au bas de cet article, ou sur le [Forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="09324-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-the-source-environment"></a><span data-ttu-id="09324-106">Configurer l’environnement source</span><span class="sxs-lookup"><span data-stu-id="09324-106">Set up the source environment</span></span>

<span data-ttu-id="09324-107">Configurez le serveur de configuration, inscrivez-le dans le coffre et découvrez les machines.</span><span class="sxs-lookup"><span data-stu-id="09324-107">Set up the configuration server, register it in the vault, and discover machines.</span></span>

1. <span data-ttu-id="09324-108">Cliquez sur **Site Recovery** > **Étape 1 : Préparer l’infrastructure** > **Source**.</span><span class="sxs-lookup"><span data-stu-id="09324-108">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="09324-109">Si vous n’avez pas de serveur de configuration, cliquez sur **+Serveur de configuration**.</span><span class="sxs-lookup"><span data-stu-id="09324-109">If you don’t have a configuration server, click **+Configuration server**.</span></span>
3. <span data-ttu-id="09324-110">Dans **Ajouter un serveur**, vérifiez que **Serveur de configuration** s’affiche dans **Type de serveur**.</span><span class="sxs-lookup"><span data-stu-id="09324-110">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="09324-111">Téléchargez le fichier d’installation unifiée de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="09324-111">Download the Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="09324-112">Téléchargez la clé d’inscription du coffre.</span><span class="sxs-lookup"><span data-stu-id="09324-112">Download the vault registration key.</span></span> <span data-ttu-id="09324-113">Vous en aurez besoin lors de l’exécution du programme d’installation unifiée.</span><span class="sxs-lookup"><span data-stu-id="09324-113">You need this when you run Unified Setup.</span></span> <span data-ttu-id="09324-114">Une fois générée, la clé reste valide pendant 5 jours.</span><span class="sxs-lookup"><span data-stu-id="09324-114">The key is valid for five days after you generate it.</span></span>

   ![Configurer la source](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-the-configuration-server-in-the-vault"></a><span data-ttu-id="09324-116">inscrire le serveur de configuration dans le coffre</span><span class="sxs-lookup"><span data-stu-id="09324-116">Register the configuration server in the vault</span></span>

<span data-ttu-id="09324-117">Suivez les étapes suivantes avant de commencer, puis exécutez le programme d’installation unifiée afin d’installer le serveur de configuration, le serveur de processus et le serveur cible maître.</span><span class="sxs-lookup"><span data-stu-id="09324-117">Do the following before you start, then run Unified Setup to install the configuration server, the process server, and the master target server.</span></span> <span data-ttu-id="09324-118">La vidéo décrit comment configurer les composants pour une réplication de machine virtuelle VMware vers Azure.</span><span class="sxs-lookup"><span data-stu-id="09324-118">The video describes setting up the components for VMware VM to Azure replication.</span></span> <span data-ttu-id="09324-119">Toutefois, le même processus vaut pour la réplication de serveurs physiques vers Azure.</span><span class="sxs-lookup"><span data-stu-id="09324-119">However, the same process is valid for physical server to Azure replication.</span></span>

- <span data-ttu-id="09324-120">Sur la machine virtuelle du serveur de configuration, assurez-vous que l’horloge système est synchronisée avec un [Serveur de temps](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span><span class="sxs-lookup"><span data-stu-id="09324-120">On the configuration server VM, make sure that the system clock is synchronized with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="09324-121">Elles doivent correspondre.</span><span class="sxs-lookup"><span data-stu-id="09324-121">It should match.</span></span> <span data-ttu-id="09324-122">S’il y a 15 minutes d’avance ou de retard, le programme d’installation peut échouer.</span><span class="sxs-lookup"><span data-stu-id="09324-122">If it's 15 minutes in front or behind, setup might fail.</span></span>
- <span data-ttu-id="09324-123">Exécutez le programme d’installation en tant qu’administrateur local sur la machine du serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="09324-123">Run setup as a Local Administrator on the configuration server machine.</span></span>
- <span data-ttu-id="09324-124">Assurez-vous que TLS 1.0 est activé sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="09324-124">Make sure TLS 1.0 is enabled on the VM.</span></span>


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="09324-125">Le serveur de configuration peut également être installé [en ligne de commande](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="09324-125">The configuration server can also be installed [from the command line](http://aka.ms/installconfigsrv).</span></span>




## <a name="set-up-the-target-environment"></a><span data-ttu-id="09324-126">Configurer l’environnement cible</span><span class="sxs-lookup"><span data-stu-id="09324-126">Set up the target environment</span></span>

<span data-ttu-id="09324-127">Avant de configurer l’environnement cible, assurez-vous de disposer d’un compte de stockage Azure et d’un réseau virtuel déjà configuré.</span><span class="sxs-lookup"><span data-stu-id="09324-127">Before you set up the target environment, make sure you have an Azure storage account and virtual network set up.</span></span>

1. <span data-ttu-id="09324-128">Cliquez sur **Préparer l’infrastructure** > **Cible** et sélectionnez l’abonnement Azure à utiliser.</span><span class="sxs-lookup"><span data-stu-id="09324-128">Click **Prepare infrastructure** > **Target**, and select the Azure subscription you want to use.</span></span>
2. <span data-ttu-id="09324-129">Spécifiez si votre modèle de déploiement cible est basé sur Resource Manager ou est de type classique.</span><span class="sxs-lookup"><span data-stu-id="09324-129">Specify whether your target deployment model is Resource Manager-based, or classic.</span></span>
3. <span data-ttu-id="09324-130">Site Recovery vérifie que vous disposez d’un ou de plusieurs réseaux et comptes Azure Storage compatibles.</span><span class="sxs-lookup"><span data-stu-id="09324-130">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![Cible](./media/physical-walkthrough-source-target/gs-target.png)

4. <span data-ttu-id="09324-132">Si vous n’avez pas créé de compte de stockage ou de réseau, cliquez sur **+Compte de stockage** ou **+Réseau** pour créer un compte Resource Manager ou un réseau en ligne.</span><span class="sxs-lookup"><span data-stu-id="09324-132">If you haven't created a storage account or network, click **+Storage account** or **+Network**, to create a Resource Manager account or network inline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09324-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="09324-133">Next steps</span></span>

<span data-ttu-id="09324-134">Aller à l’[Étape 8 : Configurer une stratégie de réplication](physical-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="09324-134">Go to [Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>
