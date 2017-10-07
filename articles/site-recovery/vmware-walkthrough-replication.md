---
title: "aaaSet une stratégie de réplication pour tooAzure de réplication VMware VM avec Azure Site Recovery | Documents Microsoft"
description: "Résume les étapes hello vous devez tooset une stratégie de réplication lors de la réplication des ordinateurs virtuels VMware tooAzure stockage"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d7874bd8-6626-4668-9ec9-dbd2d26f8f81
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 12870f3f98a4dd412221b817581403cd4bf7a76d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-vmware-vm-replication-tooazure"></a><span data-ttu-id="d10be-103">Étape 9 : Configurer une stratégie de réplication pour VMware VM réplication tooAzure</span><span class="sxs-lookup"><span data-stu-id="d10be-103">Step 9: Set up a replication policy for VMware VM replication tooAzure</span></span>


<span data-ttu-id="d10be-104">Cet article décrit comment tooset une stratégie de réplication lorsque vous effectuez une réplication tooAzure les ordinateurs virtuels VMware à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d10be-104">This article describes how tooset up a replication policy when you're replicating VMware VMs tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="d10be-105">Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="d10be-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="configure-a-policy"></a><span data-ttu-id="d10be-106">Configurer une stratégie</span><span class="sxs-lookup"><span data-stu-id="d10be-106">Configure a policy</span></span>

<span data-ttu-id="d10be-107">Visionnez une courte vidéo de présentation avant de commencer :</span><span class="sxs-lookup"><span data-stu-id="d10be-107">Get a quick video overview before you start:</span></span>
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. <span data-ttu-id="d10be-108">toocreate une stratégie de réplication, cliquez sur **infrastructure de Site Recovery** > **stratégies de réplication** > **+ la stratégie de réplication**.</span><span class="sxs-lookup"><span data-stu-id="d10be-108">toocreate a new replication policy, click **Site Recovery infrastructure** > **Replication Policies** > **+Replication Policy**.</span></span>
2. <span data-ttu-id="d10be-109">Dans **Créer une stratégie de réplication**, indiquez le nom de la stratégie.</span><span class="sxs-lookup"><span data-stu-id="d10be-109">In **Create replication policy**, specify a policy name.</span></span>
3. <span data-ttu-id="d10be-110">Dans **seuil RPO**, spécifiez la limite RPO hello.</span><span class="sxs-lookup"><span data-stu-id="d10be-110">In **RPO threshold**, specify hello RPO limit.</span></span> <span data-ttu-id="d10be-111">Cette valeur spécifie la fréquence à laquelle les points de récupération des données sont créés.</span><span class="sxs-lookup"><span data-stu-id="d10be-111">This value specifies how often data recovery points are created.</span></span> <span data-ttu-id="d10be-112">Une alerte est générée lorsque la réplication continue dépasse cette limite.</span><span class="sxs-lookup"><span data-stu-id="d10be-112">An alert is generated if continuous replication exceeds this limit.</span></span>
4. <span data-ttu-id="d10be-113">Dans **rétention du point de récupération**, spécifiez la durée (en heures) est d’une fenêtre de rétention hello pour chaque point de récupération.</span><span class="sxs-lookup"><span data-stu-id="d10be-113">In **Recovery point retention**, specify (in hours) how long hello retention window is for each recovery point.</span></span> <span data-ttu-id="d10be-114">Machines virtuelles répliquées peuvent être récupérées point tooany dans une fenêtre.</span><span class="sxs-lookup"><span data-stu-id="d10be-114">Replicated VMs can be recovered tooany point in a window.</span></span> <span data-ttu-id="d10be-115">Des too24 rétention d’heures est pris en charge pour les machines répliquées toopremium stockage et 72 heures pour le stockage standard.</span><span class="sxs-lookup"><span data-stu-id="d10be-115">Up too24 hours retention is supported for machines replicated toopremium storage, and 72 hours for standard storage.</span></span>
5. <span data-ttu-id="d10be-116">Dans **Fréquence des captures instantanées de cohérence d’application**, spécifiez la fréquence de création des points de récupération contenant des captures instantanées cohérentes avec les applications (en minutes).</span><span class="sxs-lookup"><span data-stu-id="d10be-116">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="d10be-117">Cliquez sur **OK** stratégie de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="d10be-117">Click **OK** toocreate hello policy.</span></span>

    ![Stratégie de réplication](./media/vmware-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="d10be-119">Lorsque vous créez une nouvelle stratégie, il est automatiquement associé serveur de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="d10be-119">When you create a new policy it's automatically associated with hello configuration server.</span></span> <span data-ttu-id="d10be-120">Par défaut, une stratégie de correspondance est automatiquement créée pour la restauration automatique.</span><span class="sxs-lookup"><span data-stu-id="d10be-120">By default, a matching policy is automatically created for failback.</span></span> <span data-ttu-id="d10be-121">Par exemple, si hello stratégie de réplication est **rep-policy** stratégie de restauration automatique hello sera **rep-stratégie de la restauration automatique**.</span><span class="sxs-lookup"><span data-stu-id="d10be-121">For example, if hello replication policy is **rep-policy** then hello failback policy will be **rep-policy-failback**.</span></span> <span data-ttu-id="d10be-122">Cette stratégie n’est utilisée qu’à partir du moment où vous initiez une restauration automatique à partir d’Azure.</span><span class="sxs-lookup"><span data-stu-id="d10be-122">This policy isn't used until you initiate a failback from Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d10be-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d10be-123">Next steps</span></span>

<span data-ttu-id="d10be-124">Accédez trop[étape 10 : installer le service de mobilité hello](vmware-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="d10be-124">Go too[Step 10: Install hello Mobility service](vmware-walkthrough-install-mobility.md)</span></span>
