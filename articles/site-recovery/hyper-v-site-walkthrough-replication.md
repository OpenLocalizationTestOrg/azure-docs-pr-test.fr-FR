---
title: "Configurer une stratégie de réplication pour la réplication de machines virtuelles Hyper-V (sans System Center VMM) vers Azure avec Azure Site Recovery | Microsoft Docs"
description: "Résume les étapes à suivre pour configurer une stratégie de réplication pour la réplication de machines virtuelles Hyper-V vers le stockage Azure."
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 1777e0eb-accb-42b5-a747-11272e131a52
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: ca5bec5cf1152e6259b9fe7a869edd2d62b88e1a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="step-9-set-up-a-replication-policy-for-hyper-v-vm-replication-to-azure"></a><span data-ttu-id="77c9d-103">Étape 9 : configurer une stratégie de réplication pour la réplication de machines virtuelles Hyper-V vers Azure</span><span class="sxs-lookup"><span data-stu-id="77c9d-103">Step 9: Set up a replication policy for Hyper-V VM replication to Azure</span></span>

<span data-ttu-id="77c9d-104">Cet article explique comment configurer une stratégie de réplication pour la réplication de machines virtuelles Hyper-V vers Azure (sans System Center VMM) à l’aide du service [Azure Site Recovery](site-recovery-overview.md) dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="77c9d-104">This article describes how to set up a replication policy when you're replicating Hyper-V VMs to Azure (without System Center VMM) using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="77c9d-105">Publiez des commentaires et des questions au bas de cet article, ou sur le [Forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="77c9d-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="about-snapshots"></a><span data-ttu-id="77c9d-106">Informations concernant les instantanés</span><span class="sxs-lookup"><span data-stu-id="77c9d-106">About snapshots</span></span>

<span data-ttu-id="77c9d-107">Hyper-V utilise deux types d’instantanés : un instantané standard qui fournit un instantané incrémentiel de la machine virtuelle complète et un instantané cohérent avec l'application qui prend un instantané des données d'application d'une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="77c9d-107">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of the entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of the application data inside the virtual machine.</span></span>
    - <span data-ttu-id="77c9d-108">Les instantanés cohérents avec l'application utilisent le service VSS (Volume Shadow Copy Service) pour s'assurer que les applications sont dans un état cohérent lors de la prise des instantanés.</span><span class="sxs-lookup"><span data-stu-id="77c9d-108">Application-consistent snapshots use Volume Shadow Copy Service (VSS) to ensure that applications are in a consistent state when the snapshot is taken.</span></span>
    - <span data-ttu-id="77c9d-109">Si vous activez les instantanés cohérents avec l'application, cela affecte les performances des applications exécutées sur les machines virtuelles sources.</span><span class="sxs-lookup"><span data-stu-id="77c9d-109">If you enable application-consistent snapshots, it will affect the performance of applications running on source virtual machines.</span></span> <span data-ttu-id="77c9d-110">Assurez-vous que la valeur définie est inférieure au nombre de points de récupération supplémentaires que vous configurez.</span><span class="sxs-lookup"><span data-stu-id="77c9d-110">Ensure that the value you set is less than the number of additional recovery points you configure.</span></span>

## <a name="set-up-a-replication-policy"></a><span data-ttu-id="77c9d-111">Configurer une stratégie de réplication</span><span class="sxs-lookup"><span data-stu-id="77c9d-111">Set up a replication policy</span></span>

1. <span data-ttu-id="77c9d-112">Pour créer une stratégie de réplication, cliquez sur **Préparer l’infrastructure** > **Paramètres de réplication** > **+Créer et associer**.</span><span class="sxs-lookup"><span data-stu-id="77c9d-112">To create a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![Réseau](./media/hyper-v-site-walkthrough-replication/gs-replication.png)
2. <span data-ttu-id="77c9d-114">Dans **Créer et associer une stratégie**, indiquez le nom de la stratégie.</span><span class="sxs-lookup"><span data-stu-id="77c9d-114">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="77c9d-115">Dans **Fréquence de copie**, spécifiez la fréquence selon laquelle répliquer les données delta après la réplication initiale (toutes les 30 secondes ou toutes les 5 ou 15 minutes).</span><span class="sxs-lookup"><span data-stu-id="77c9d-115">In **Copy frequency**, specify how often you want to replicate delta data after the initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    > <span data-ttu-id="77c9d-116">Une fréquence de 30 secondes n’est pas prise en charge lors de la réplication sur un Stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="77c9d-116">A 30 second frequency isn't supported when replicating to premium storage.</span></span> <span data-ttu-id="77c9d-117">La limitation est déterminée par le nombre de captures instantanées par objet blob (100) pris en charge par le Stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="77c9d-117">The limitation is determined by the number of snapshots per blob (100) supported by premium storage.</span></span> <span data-ttu-id="77c9d-118">[Plus d’informations](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)</span><span class="sxs-lookup"><span data-stu-id="77c9d-118">[Learn more](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).</span></span>

4. <span data-ttu-id="77c9d-119">Dans **Rétention des points de récupération**, spécifiez la durée (en heures) de la fenêtre de rétention pour chaque point de récupération.</span><span class="sxs-lookup"><span data-stu-id="77c9d-119">In **Recovery point retention**, specify in hours how long the retention window is for each recovery point.</span></span> <span data-ttu-id="77c9d-120">Les machines virtuelles peuvent être récupérées à tout moment pendant cette fenêtre temporelle.</span><span class="sxs-lookup"><span data-stu-id="77c9d-120">VMs can be recovered to any point within a window.</span></span>
5. <span data-ttu-id="77c9d-121">Dans **Fréquence des captures instantanées cohérentes de l’application**, spécifiez la fréquence de création des points de récupération contenant des instantanés cohérents au niveau des applications (entre 1 et 12 heures).</span><span class="sxs-lookup"><span data-stu-id="77c9d-121">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots are created.</span></span>
6. <span data-ttu-id="77c9d-122">Dans **Heure de début de la réplication initiale**, indiquez à quel moment démarrer la réplication initiale.</span><span class="sxs-lookup"><span data-stu-id="77c9d-122">In **Initial replication start time**, specify when to start the initial replication.</span></span> <span data-ttu-id="77c9d-123">La réplication se produit via votre bande passante Internet. Il est donc préférable de prévoir son exécution en dehors des heures de bureau.</span><span class="sxs-lookup"><span data-stu-id="77c9d-123">The replication occurs over your internet bandwidth so you might want to schedule it outside your busy hours.</span></span> <span data-ttu-id="77c9d-124">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="77c9d-124">Then click **OK**.</span></span>

    ![Stratégie de réplication](./media/hyper-v-site-walkthrough-replication/gs-replication2.png)

<span data-ttu-id="77c9d-126">Lorsque vous créez une stratégie, elle est automatiquement associée au site Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="77c9d-126">When you create a new policy, it's automatically associated with the Hyper-V site.</span></span> <span data-ttu-id="77c9d-127">Vous pouvez associer un site Hyper-V (et les machines virtuelles qu’il contient) à plusieurs stratégies de réplication dans **Réplication** > nom de la stratégie > **Associer le site Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="77c9d-127">You can associate a Hyper-V site (and the VMs in it) with multiple replication policies in **Replication** > policy-name > **Associate Hyper-V Site**.</span></span>



## <a name="next-steps"></a><span data-ttu-id="77c9d-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="77c9d-128">Next steps</span></span>

<span data-ttu-id="77c9d-129">Aller à [Étape 10 : activer la réplication](hyper-v-site-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="77c9d-129">Go to [Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>
