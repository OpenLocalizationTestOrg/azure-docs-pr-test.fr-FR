---
title: "aaaSet une stratégie de réplication pour tooAzure de réplication d’ordinateur virtuel d’Hyper-V (avec VMM) avec Azure Site Recovery | Documents Microsoft"
description: "Décrit comment tooset une stratégie de réplication pour tooAzure de réplication d’ordinateur virtuel d’Hyper-V (avec VMM) avec Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ee808b20-324b-4198-b831-edb65b95e8b7
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: e1579fde559ca34eca19a01e740fec28a0df2f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-set-up-a-replication-policy-for-hyper-v-vm-replication-with-vmm-tooazure"></a><span data-ttu-id="28f7a-103">Étape 10 : Définir une stratégie de réplication pour tooAzure de réplication (avec VMM) d’un ordinateur virtuel Hyper-V</span><span class="sxs-lookup"><span data-stu-id="28f7a-103">Step 10: Set up a replication policy for Hyper-V VM replication (with VMM) tooAzure</span></span>


<span data-ttu-id="28f7a-104">Après avoir configuré [le mappage réseau](vmm-to-azure-walkthrough-network-mapping.md), utilisez cette tooconfigure article une stratégie de réplication T\tooreplicate locaux virtuels Hyper-V gérés dans tooAzure des clouds System Center Virtual Machine Manager (VMM), à l’aide de hello [ Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="28f7a-104">After setting up [network mapping](vmm-to-azure-walkthrough-network-mapping.md), use this article tooconfigure a replication policy T\tooreplicate on-premises Hyper-V virtual machines managed in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="28f7a-105">Après avoir lu cet article, validez les commentaires au bas de hello, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="28f7a-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="create-a-policy"></a><span data-ttu-id="28f7a-106">Création d’une stratégie</span><span class="sxs-lookup"><span data-stu-id="28f7a-106">Create a policy</span></span>

1. <span data-ttu-id="28f7a-107">toocreate une stratégie de réplication, cliquez sur **Prepare infrastructure** > **les paramètres de réplication** > **+ créer et associer**.</span><span class="sxs-lookup"><span data-stu-id="28f7a-107">toocreate a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![Réseau](./media/vmm-to-azure-walkthrough-replication/gs-replication.png)
2. <span data-ttu-id="28f7a-109">Dans **Créer et associer une stratégie**, indiquez le nom de la stratégie.</span><span class="sxs-lookup"><span data-stu-id="28f7a-109">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="28f7a-110">Dans **fréquence de copie**, spécifiez la fréquence à laquelle vous souhaitez tooreplicate d’éventuelles données delta après la réplication initiale de hello (toutes les 30 secondes, 5 ou 15 minutes).</span><span class="sxs-lookup"><span data-stu-id="28f7a-110">In **Copy frequency**, specify how often you want tooreplicate delta data after hello initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    >  <span data-ttu-id="28f7a-111">Une fréquence de deuxième 30 n’est pas pris en charge lors de la réplication de stockage de toopremium.</span><span class="sxs-lookup"><span data-stu-id="28f7a-111">A 30 second frequency isn't supported when replicating toopremium storage.</span></span> <span data-ttu-id="28f7a-112">limitation de Hello est déterminée par le nombre de hello d’instantanés par l’objet blob (100) pris en charge par le stockage premium.</span><span class="sxs-lookup"><span data-stu-id="28f7a-112">hello limitation is determined by hello number of snapshots per blob (100) supported by premium storage.</span></span> [<span data-ttu-id="28f7a-113">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="28f7a-113">Learn more</span></span>](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. <span data-ttu-id="28f7a-114">Dans **rétention du point de récupération**, spécifiez, en heures, la durée de conservation hello sera être pour chaque point de récupération.</span><span class="sxs-lookup"><span data-stu-id="28f7a-114">In **Recovery point retention**, specify in hours how long hello retention window will be for each recovery point.</span></span> <span data-ttu-id="28f7a-115">Les ordinateurs protégés peuvent être récupérées point tooany dans une fenêtre.</span><span class="sxs-lookup"><span data-stu-id="28f7a-115">Protected machines can be recovered tooany point within a window.</span></span>
5. <span data-ttu-id="28f7a-116">Dans **Fréquence des captures instantanées cohérentes de l’application**, spécifiez la fréquence de création des points de récupération contenant des instantanés cohérents au niveau des applications (entre 1 et 12 heures).</span><span class="sxs-lookup"><span data-stu-id="28f7a-116">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="28f7a-117">Hyper-V utilise deux types de captures instantanées, un instantané standard qui fournit un instantané incrémentiel de la machine virtuelle hello et un instantané cohérent de l’application qui prend un instantané de point-à-temps hello des données d’application à l’intérieur de machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="28f7a-117">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of hello entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of hello application data inside hello virtual machine.</span></span> <span data-ttu-id="28f7a-118">Instantanés cohérents au niveau de l’application utilisent tooensure Volume Shadow Copy Service (VSS) que les applications sont dans un état cohérent lors de l’instantané hello.</span><span class="sxs-lookup"><span data-stu-id="28f7a-118">Application-consistent snapshots use Volume Shadow Copy Service (VSS) tooensure that applications are in a consistent state when hello snapshot is taken.</span></span> <span data-ttu-id="28f7a-119">Notez que si vous activez les instantanés cohérents au niveau de l’application, il affecte les performances de hello des applications s’exécutant sur des machines virtuelles sources.</span><span class="sxs-lookup"><span data-stu-id="28f7a-119">Note that if you enable application-consistent snapshots, it will affect hello performance of applications running on source virtual machines.</span></span> <span data-ttu-id="28f7a-120">Assurez-vous que la valeur hello que vous définissez est inférieur au nombre de hello de points de récupération supplémentaires que vous configurez.</span><span class="sxs-lookup"><span data-stu-id="28f7a-120">Ensure that hello value you set is less than hello number of additional recovery points you configure.</span></span>
6. <span data-ttu-id="28f7a-121">Dans **heure de début de la réplication initiale**, indiquer quand toostart hello la réplication initiale.</span><span class="sxs-lookup"><span data-stu-id="28f7a-121">In **Initial replication start time**, indicate when toostart hello initial replication.</span></span> <span data-ttu-id="28f7a-122">la réplication Hello se produit sur votre bande passante internet, vous pouvez donc tooschedule il en dehors des heures occupés.</span><span class="sxs-lookup"><span data-stu-id="28f7a-122">hello replication occurs over your internet bandwidth so you might want tooschedule it outside your busy hours.</span></span>
7. <span data-ttu-id="28f7a-123">Dans **chiffrer les données stockées sur Azure**, spécifiez si tooencrypt données reste dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="28f7a-123">In **Encrypt data stored on Azure**, specify whether tooencrypt at rest data in Azure storage.</span></span> <span data-ttu-id="28f7a-124">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="28f7a-124">Then click **OK**.</span></span>

    ![Stratégie de réplication](./media/vmm-to-azure-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="28f7a-126">Lorsque vous créez une nouvelle stratégie, il est automatiquement associé hello cloud VMM.</span><span class="sxs-lookup"><span data-stu-id="28f7a-126">When you create a new policy it's automatically associated with hello VMM cloud.</span></span> <span data-ttu-id="28f7a-127">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="28f7a-127">Click **OK**.</span></span> <span data-ttu-id="28f7a-128">Vous pouvez associer clouds VMM supplémentaires (et hello machines virtuelles dans les) cette stratégie de réplication dans **réplication** > nom de la stratégie > **associer le Cloud VMM**.</span><span class="sxs-lookup"><span data-stu-id="28f7a-128">You can associate additional VMM clouds (and hello VMs in them) with this replication policy in **Replication** > policy name > **Associate VMM Cloud**.</span></span>

    ![Stratégie de réplication](./media/vmm-to-azure-walkthrough-replication/policy-associate.png)



## <a name="next-steps"></a><span data-ttu-id="28f7a-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="28f7a-130">Next steps</span></span>

<span data-ttu-id="28f7a-131">Accédez trop[étape 11 : activer la réplication](vmm-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="28f7a-131">Go too[Step 11: Enable replication](vmm-to-azure-walkthrough-enable-replication.md)</span></span>
