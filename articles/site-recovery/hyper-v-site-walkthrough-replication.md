---
title: "aaaSet une stratégie de réplication pour tooAzure de réplication (sans System Center VMM) d’un ordinateur virtuel Hyper-V avec Azure Site Recovery | Documents Microsoft"
description: "Résume les étapes hello vous devez tooset une stratégie de réplication lors de la réplication des ordinateurs virtuels Hyper-V tooAzure stockage"
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
ms.openlocfilehash: 4bd7161f4a0f015da0ecf595fbc6861ede5d68b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-hyper-v-vm-replication-tooazure"></a><span data-ttu-id="b7c42-103">Étape 9 : Configurer une stratégie de réplication pour tooAzure de réplication de machine virtuelle Hyper-V</span><span class="sxs-lookup"><span data-stu-id="b7c42-103">Step 9: Set up a replication policy for Hyper-V VM replication tooAzure</span></span>

<span data-ttu-id="b7c42-104">Cet article décrit comment tooset une stratégie de réplication lorsque vous effectuez une réplication tooAzure d’ordinateurs virtuels Hyper-V (sans System Center VMM) à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b7c42-104">This article describes how tooset up a replication policy when you're replicating Hyper-V VMs tooAzure (without System Center VMM) using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="b7c42-105">Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="b7c42-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="about-snapshots"></a><span data-ttu-id="b7c42-106">Informations concernant les instantanés</span><span class="sxs-lookup"><span data-stu-id="b7c42-106">About snapshots</span></span>

<span data-ttu-id="b7c42-107">Hyper-V utilise deux types de captures instantanées, un instantané standard qui fournit un instantané incrémentiel de la machine virtuelle hello et un instantané cohérent de l’application qui prend un instantané de point-à-temps hello des données d’application à l’intérieur de machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="b7c42-107">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of hello entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of hello application data inside hello virtual machine.</span></span>
    - <span data-ttu-id="b7c42-108">Instantanés cohérents au niveau de l’application utilisent tooensure Volume Shadow Copy Service (VSS) que les applications sont dans un état cohérent lors de l’instantané hello.</span><span class="sxs-lookup"><span data-stu-id="b7c42-108">Application-consistent snapshots use Volume Shadow Copy Service (VSS) tooensure that applications are in a consistent state when hello snapshot is taken.</span></span>
    - <span data-ttu-id="b7c42-109">Si vous activez les instantanés cohérents au niveau de l’application, il affecte les performances de hello des applications exécutées sur des machines virtuelles sources.</span><span class="sxs-lookup"><span data-stu-id="b7c42-109">If you enable application-consistent snapshots, it will affect hello performance of applications running on source virtual machines.</span></span> <span data-ttu-id="b7c42-110">Assurez-vous que la valeur hello que vous définissez est inférieur au nombre de hello de points de récupération supplémentaires que vous configurez.</span><span class="sxs-lookup"><span data-stu-id="b7c42-110">Ensure that hello value you set is less than hello number of additional recovery points you configure.</span></span>

## <a name="set-up-a-replication-policy"></a><span data-ttu-id="b7c42-111">Configurer une stratégie de réplication</span><span class="sxs-lookup"><span data-stu-id="b7c42-111">Set up a replication policy</span></span>

1. <span data-ttu-id="b7c42-112">toocreate une stratégie de réplication, cliquez sur **Prepare infrastructure** > **les paramètres de réplication** > **+ créer et associer**.</span><span class="sxs-lookup"><span data-stu-id="b7c42-112">toocreate a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![Réseau](./media/hyper-v-site-walkthrough-replication/gs-replication.png)
2. <span data-ttu-id="b7c42-114">Dans **Créer et associer une stratégie**, indiquez le nom de la stratégie.</span><span class="sxs-lookup"><span data-stu-id="b7c42-114">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="b7c42-115">Dans **fréquence de copie**, spécifiez la fréquence à laquelle vous souhaitez tooreplicate d’éventuelles données delta après la réplication initiale de hello (toutes les 30 secondes, 5 ou 15 minutes).</span><span class="sxs-lookup"><span data-stu-id="b7c42-115">In **Copy frequency**, specify how often you want tooreplicate delta data after hello initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    > <span data-ttu-id="b7c42-116">Une fréquence de deuxième 30 n’est pas pris en charge lors de la réplication de stockage de toopremium.</span><span class="sxs-lookup"><span data-stu-id="b7c42-116">A 30 second frequency isn't supported when replicating toopremium storage.</span></span> <span data-ttu-id="b7c42-117">limitation de Hello est déterminée par le nombre de hello d’instantanés par l’objet blob (100) pris en charge par le stockage premium.</span><span class="sxs-lookup"><span data-stu-id="b7c42-117">hello limitation is determined by hello number of snapshots per blob (100) supported by premium storage.</span></span> <span data-ttu-id="b7c42-118">[En savoir plus](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).</span><span class="sxs-lookup"><span data-stu-id="b7c42-118">[Learn more](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).</span></span>

4. <span data-ttu-id="b7c42-119">Dans **rétention du point de récupération**, spécifiez combien d’heures de conservation hello est pour chaque point de récupération.</span><span class="sxs-lookup"><span data-stu-id="b7c42-119">In **Recovery point retention**, specify in hours how long hello retention window is for each recovery point.</span></span> <span data-ttu-id="b7c42-120">Machines virtuelles peuvent être récupérée point tooany dans une fenêtre.</span><span class="sxs-lookup"><span data-stu-id="b7c42-120">VMs can be recovered tooany point within a window.</span></span>
5. <span data-ttu-id="b7c42-121">Dans **Fréquence des captures instantanées cohérentes de l’application**, spécifiez la fréquence de création des points de récupération contenant des instantanés cohérents au niveau des applications (entre 1 et 12 heures).</span><span class="sxs-lookup"><span data-stu-id="b7c42-121">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots are created.</span></span>
6. <span data-ttu-id="b7c42-122">Dans **heure de début de la réplication initiale**, spécifiez quand toostart hello la réplication initiale.</span><span class="sxs-lookup"><span data-stu-id="b7c42-122">In **Initial replication start time**, specify when toostart hello initial replication.</span></span> <span data-ttu-id="b7c42-123">la réplication Hello se produit sur votre bande passante internet, vous pouvez donc tooschedule il en dehors des heures occupés.</span><span class="sxs-lookup"><span data-stu-id="b7c42-123">hello replication occurs over your internet bandwidth so you might want tooschedule it outside your busy hours.</span></span> <span data-ttu-id="b7c42-124">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b7c42-124">Then click **OK**.</span></span>

    ![Stratégie de réplication](./media/hyper-v-site-walkthrough-replication/gs-replication2.png)

<span data-ttu-id="b7c42-126">Lorsque vous créez une nouvelle stratégie, il est automatiquement associé site Hyper-V de hello.</span><span class="sxs-lookup"><span data-stu-id="b7c42-126">When you create a new policy, it's automatically associated with hello Hyper-V site.</span></span> <span data-ttu-id="b7c42-127">Vous pouvez associer un site Hyper-V (et hello machines virtuelles qu’il contient) à plusieurs stratégies de réplication dans **réplication** > nom de la stratégie > **associer le Site Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="b7c42-127">You can associate a Hyper-V site (and hello VMs in it) with multiple replication policies in **Replication** > policy-name > **Associate Hyper-V Site**.</span></span>



## <a name="next-steps"></a><span data-ttu-id="b7c42-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b7c42-128">Next steps</span></span>

<span data-ttu-id="b7c42-129">Accédez trop[étape 10 : activer la réplication](hyper-v-site-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="b7c42-129">Go too[Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>
