---
title: "Configurer la stratégie de réplication pour la réplication des machines virtuelles VMware sur Azure à l’aide d’Azure Site Recovery | Microsoft Docs"
description: "Résume les étapes à suivre pour configurer une stratégie de réplication lors de la réplication des machines virtuelles VMware sur un stockage Azure"
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
ms.openlocfilehash: 3c4b7ad16e6a03fb605447def18f7475d502fdd1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="step-9-set-up-a-replication-policy-for-vmware-vm-replication-to-azure"></a><span data-ttu-id="e481d-103">Étape 9 : configurer une stratégie de réplication pour la réplication d’une machine virtuelle VMware sur Azure</span><span class="sxs-lookup"><span data-stu-id="e481d-103">Step 9: Set up a replication policy for VMware VM replication to Azure</span></span>


<span data-ttu-id="e481d-104">Cet article explique comment configurer une stratégie de réplication pour la réplication d’une machine virtuelle VMware sur Azure à l’aide du service [Azure Site Recovery](site-recovery-overview.md) dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e481d-104">This article describes how to set up a replication policy when you're replicating VMware VMs to Azure using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="e481d-105">Publiez des commentaires et des questions au bas de cet article, ou sur le [Forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="e481d-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="configure-a-policy"></a><span data-ttu-id="e481d-106">Configurer une stratégie</span><span class="sxs-lookup"><span data-stu-id="e481d-106">Configure a policy</span></span>

<span data-ttu-id="e481d-107">Visionnez une courte vidéo de présentation avant de commencer :</span><span class="sxs-lookup"><span data-stu-id="e481d-107">Get a quick video overview before you start:</span></span>
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. <span data-ttu-id="e481d-108">Pour créer une nouvelle stratégie de réplication, cliquez sur **Infrastructure de Site Recovery** > **Stratégies de réplication** > **+Stratégie de réplication**.</span><span class="sxs-lookup"><span data-stu-id="e481d-108">To create a new replication policy, click **Site Recovery infrastructure** > **Replication Policies** > **+Replication Policy**.</span></span>
2. <span data-ttu-id="e481d-109">Dans **Créer une stratégie de réplication**, indiquez le nom de la stratégie.</span><span class="sxs-lookup"><span data-stu-id="e481d-109">In **Create replication policy**, specify a policy name.</span></span>
3. <span data-ttu-id="e481d-110">Dans le champ **Seuil d’objectif de point de récupération**, spécifiez la limite de l’objectif de point de récupération.</span><span class="sxs-lookup"><span data-stu-id="e481d-110">In **RPO threshold**, specify the RPO limit.</span></span> <span data-ttu-id="e481d-111">Cette valeur spécifie la fréquence à laquelle les points de récupération des données sont créés.</span><span class="sxs-lookup"><span data-stu-id="e481d-111">This value specifies how often data recovery points are created.</span></span> <span data-ttu-id="e481d-112">Une alerte est générée lorsque la réplication continue dépasse cette limite.</span><span class="sxs-lookup"><span data-stu-id="e481d-112">An alert is generated if continuous replication exceeds this limit.</span></span>
4. <span data-ttu-id="e481d-113">Dans **Rétention des points de récupération**, spécifiez la durée de la fenêtre de rétention pour chaque point de récupération (en heures).</span><span class="sxs-lookup"><span data-stu-id="e481d-113">In **Recovery point retention**, specify (in hours) how long the retention window is for each recovery point.</span></span> <span data-ttu-id="e481d-114">Les machines virtuelles répliquées peuvent être récupérées à n’importe quel point dans une fenêtre.</span><span class="sxs-lookup"><span data-stu-id="e481d-114">Replicated VMs can be recovered to any point in a window.</span></span> <span data-ttu-id="e481d-115">Les machines virtuelles répliquées vers Premium Storage peuvent prendre en charge jusqu’à 24 heures de rétention et 72 heures en cas de stockage standard.</span><span class="sxs-lookup"><span data-stu-id="e481d-115">Up to 24 hours retention is supported for machines replicated to premium storage, and 72 hours for standard storage.</span></span>
5. <span data-ttu-id="e481d-116">Dans **Fréquence des captures instantanées de cohérence d’application**, spécifiez la fréquence de création des points de récupération contenant des captures instantanées cohérentes avec les applications (en minutes).</span><span class="sxs-lookup"><span data-stu-id="e481d-116">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="e481d-117">Cliquez sur **OK** pour créer la stratégie.</span><span class="sxs-lookup"><span data-stu-id="e481d-117">Click **OK** to create the policy.</span></span>

    ![Stratégie de réplication](./media/vmware-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="e481d-119">Lorsque vous créez une stratégie, cette dernière est automatiquement associée au serveur de configuration.</span><span class="sxs-lookup"><span data-stu-id="e481d-119">When you create a new policy it's automatically associated with the configuration server.</span></span> <span data-ttu-id="e481d-120">Par défaut, une stratégie de correspondance est automatiquement créée pour la restauration automatique.</span><span class="sxs-lookup"><span data-stu-id="e481d-120">By default, a matching policy is automatically created for failback.</span></span> <span data-ttu-id="e481d-121">Par exemple, si la stratégie de réplication est **rep-policy**, la stratégie de restauration automatique correspond alors à **rep-policy-failback**.</span><span class="sxs-lookup"><span data-stu-id="e481d-121">For example, if the replication policy is **rep-policy** then the failback policy will be **rep-policy-failback**.</span></span> <span data-ttu-id="e481d-122">Cette stratégie n’est utilisée qu’à partir du moment où vous initiez une restauration automatique à partir d’Azure.</span><span class="sxs-lookup"><span data-stu-id="e481d-122">This policy isn't used until you initiate a failback from Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e481d-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e481d-123">Next steps</span></span>

<span data-ttu-id="e481d-124">Aller à [Étape 10 : installer le service Mobilité](vmware-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="e481d-124">Go to [Step 10: Install the Mobility service](vmware-walkthrough-install-mobility.md)</span></span>
